# UAV strike reports — shared domain rules

Shared knowledge for the report suite: `report-formatter`, `report-manager`, the signal bot. Copy this file into `docs/agent/` of each repo. Read it before you change any report parser, formatter, or munition classifier.

## Text hygiene
- Reports arrive from Telegram and Signal copy-paste. They carry invisible characters.
- In `clean()`, strip `U+200E` (LRM), `U+200F` (RLM), `U+200B` (ZWSP), and `U+FEFF` (BOM / ZWNBSP) before any parsing or matching. A stray bidi mark breaks token splitting and regex.

## Munition token (BK) — quantity vs name
- A trailing number on a BK munition token is ambiguous.
- Trailing `1`–`4` is a **quantity** (how many).
- Trailing `≥5` is **part of the name**, e.g. `МОА-900`.
- Classify on this rule before you sum or group munitions.

## Delta munitions
- A `Δ` prefix marks a delta (modified or special) munition; it comes from the signal bot.
- Preserve `Δ` through parsing and output. Do not strip or transliterate it.

## Encoding and filenames
- All report text and files are UTF-8. Declare the encoding explicitly on every read and write; never rely on the platform locale.
- Filenames may be Cyrillic. Do not assume ASCII paths.

## Testing
- Every parser fix gets a regression fixture built from a **real report** (anonymized). Add the fixture first, then fix.

## Secrets
- signal-cli data and raw report contents are sensitive. Never commit or log them.

---
Status: drafted from the project handoff. Verify the exact BK rule and the `clean()` character set against the real `report-formatter` code before relying on this.
