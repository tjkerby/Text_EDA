# Talk data

`talks.csv` contains 52 selected short kickers from April and October conferences in 2020, 2023, and 2025. A kicker is the highlighted message before the main talk body. Only this text is embedded in the lesson; it is not a representation of every theme in the full talk.

This is a purposive teaching sample, not a census or random sample. Administrative messages, unavailable kickers, and kickers longer than 25 whitespace-delimited words were omitted during curation. The conferences contribute 7, 9, 10, 10, 10, and 6 records respectively. Do not use these counts to estimate historical trends or speaker emphasis across the archive.

The individual official English pages were consulted on 2026-11-14. Every row retains its source `url`. Whitespace was normalized, honorifics were removed from the speaker name for display, and recorded roles were grouped into broad categories. The full role text remains available. Roles describe the source talk page, not a speaker's current position.

| Column | Meaning |
|---|---|
| `talk_id` | Stable source URL path identifier |
| `title` | Talk title |
| `speaker` | Speaker name |
| `speaker_role` | Role recorded on the talk page |
| `role_group` | Broad display group derived from that role |
| `year`, `month` | Conference year and month, 4 or 10 |
| `kicker` | The text supplied to the embedding model |
| `url` | Official English source page |
| `kicker_words` | Whitespace-delimited word count |

The optional notebook section creates `talk_embeddings.npz` here after real Nomic inference. That single file stores the vectors, ordered IDs and kicker texts, model name, and task prefix. It is not included initially because a local Ollama model could not be run in the authoring environment.
