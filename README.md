# BrainBear Community Library

Public, community-contributed **flashcard decks** and **study guides** for
**BrainBear** â€” a free study app for highâ€‘school students.

## How content gets here

Content is published **from the BrainBear app** (Create â†’ *Publish to community*).
Students don't need a GitHub account. Every submission is automatically screened
for **safety** and basic **quality** before it's committed here.

> **Please don't open pull requests by hand.** Content is published through the
> app so each item is validated, attributed, and added to the catalog. Manual PRs
> that add content won't be accepted.

## Structure

```
index.json                 # catalog of everything published (metadata only)
decks/<subject>/*.json     # flashcard decks â€” schema: brainbear.deck.v1
guides/<subject>/*.json    # study guides    â€” schema: brainbear.guide.v1
schema/README.md           # schema documentation
```

The app reads `index.json` to browse the library, then fetches an individual
deck/guide file on demand.

## Attribution & privacy

Items are attributed by the author's **display name only** â€” never an email
address or any other personal information.

## License

All study content in this repository is licensed **CC BY 4.0**
(see [LICENSE](LICENSE)). You are free to share and adapt it with attribution.

## Reporting content

Found something inappropriate or inaccurate? Use **Report** in the BrainBear app
(or open an issue here). Flagged content is reviewed and removed.
