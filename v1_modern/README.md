# OUP Authoring Template — Typst Version

## Project Structure

```
oup-paper/
├── main.typ           ← Your paper (edit this)
├── oup-template.typ   ← Template engine (don't edit)
├── reference.bib      ← Your bibliography
├── Fig/               ← Put your images here
│   ├── figure1.png
│   └── figure2.pdf
└── README.md
```

## Compile

```bash
typst compile main.typ
# Opens main.pdf
open main.pdf
```

## Live Preview (Cursor / VS Code with Tinymist)

Save the file and Tinymist auto-compiles.

## How to Add Images

In `main.typ`, replace `rect(...)` placeholders with:

```typst
#figure(
  image("Fig/your-image.png", width: 100%),
  caption: [Your caption here.],
) <fig-label>
```

Supported formats: `.png`, `.jpg`, `.svg`, `.pdf`

## How to Cite

Add entries to `reference.bib`, then cite with `@key`:

```typst
As shown by @smith2023, the results confirm...
```

## Change Style

In `main.typ`, find `style: "contemporary"` and change to:
- `"contemporary"` — OUP Contemporary (sans-serif, compact)
- `"modern"`        — OUP Modern (sans-serif)
- `"traditional"`   — OUP Traditional (serif / Times)

## Change Bibliography Style

In `main.typ`:
```typst
#bibliography("reference.bib", style: "apa")
```

Change `"apa"` to:
- `"apa"`            — APA (author-year)
- `"ieee"`           — IEEE (numbered)
- `"chicago-author-date"` — Chicago
- `"oup-author-date.csl"` — OUP exact style (download from Zotero CSL repo)

## Download OUP CSL

```bash
curl -L "https://raw.githubusercontent.com/citation-style-language/styles/master/oxford-university-press-note.csl" -o oup.csl
```

Then in main.typ:
```typst
#bibliography("reference.bib", style: "oup.csl")
```

## Optional Packages (auto-downloaded on first compile)

No external Typst packages are required — the template is self-contained.
