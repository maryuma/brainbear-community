# BrainBear content schemas

Every published item is a JSON file with a `schemaVersion` field. The app and the
publishing Function validate against these shapes. Fields marked *optional* may be
omitted or empty.

All text may contain inline math (LaTeX like `$x^2$`) and non-English text; these
are preserved verbatim.

---

## `brainbear.deck.v1` â€” flashcard deck

Path: `decks/<subject-slug>/<title-slug>-<shortid>.json`

```jsonc
{
  "schemaVersion": "brainbear.deck.v1",
  "id": "string",                 // stable unique id (also the file's shortid)
  "type": "deck",
  "title": "string",
  "subject": "string",
  "description": "string",        // optional
  "tags": ["string"],             // optional
  "cards": [
    { "front": "string", "back": "string" }
  ],
  "author": { "displayName": "string" },  // display name only â€” no email/PII
  "license": "CC-BY-4.0",
  "publishedAt": "ISO-8601 string",
  "ownerHash": "string"           // salted SHA-256 of the author's Google `sub`;
                                  // non-reversible, used only to authorize the
                                  // author's own edit/unpublish. Not PII.
}
```

## `brainbear.guide.v1` â€” study guide

Path: `guides/<subject-slug>/<title-slug>-<shortid>.json`

```jsonc
{
  "schemaVersion": "brainbear.guide.v1",
  "id": "string",
  "type": "guide",
  "title": "string",
  "subject": "string",
  "description": "string",        // optional
  "tags": ["string"],             // optional
  "body": "string",               // sanitized HTML or markdown
  "format": "html",               // "html" | "md"
  "author": { "displayName": "string" },
  "license": "CC-BY-4.0",
  "publishedAt": "ISO-8601 string",
  "ownerHash": "string"
}
```

> Guide bodies are **sanitized on publish** (server-side) and again on render in
> the app, to prevent stored-XSS from user-authored HTML.

---

## `index.json` â€” the catalog

A single top-level array of lightweight entries (one per published item). The app
fetches this to browse/search without downloading every file.

```jsonc
[
  {
    "id": "string",
    "type": "deck",               // "deck" | "guide"
    "title": "string",
    "subject": "string",
    "tags": ["string"],
    "author": "string",           // display name
    "path": "decks/biology/photosynthesis-a1b2c3.json",
    "cardCount": 20,              // decks only; omitted for guides
    "publishedAt": "ISO-8601 string"
  }
]
```

The catalog intentionally holds **no owner identifier** â€” `ownerHash` lives only in
the item file, keeping the browsable catalog free of any author-linkable data.

---

## Conventions

- **Slugs**: lowercase, spaces â†’ `-`, non-alphanumerics stripped.
- **`shortid`**: a random 6â€“8 char id appended to filenames to avoid collisions.
- **Attribution**: `author.displayName` only. Never store or publish emails or
  other personal information.
- **License**: all content is `CC-BY-4.0`.
