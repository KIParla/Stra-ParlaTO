# Stra-ParlaTO

[![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa]

- [Stra-ParlaTO](#stra-parlato)
	- [Repository organization](#repository-organization)
	- [Metadata](#metadata)
	- [Verticalized content](#verticalized-content)
	- [Translations](#translations)
	- [Data access](#data-access)
	- [How to cite](#how-to-cite)
	- [Changelog](#changelog)

The Stra-ParlaTO corpus is part of the larger [KIParla collection](https://www.kiparla.it),
which can be freely queried through the [NoSketch Engine interface](https://kiparla.it/search/).

The Stra-ParlaTO corpus was compiled within the framework of the “DiverSIta – Diversity in spoken Italian”
project (PI: Caterina Mauri), funded by the European Union – NextGenerationEU under the National Recovery
and Resilience Plan (PNRR) – Mission 4 Education and research (MUR project code P2022RFR8T, CUP J53D23017320001).

> Progetto finanziato dall’Unione Europea – NextGenerationEU a valere sul Piano Nazionale di Ripresa e
> Resilienza (PNRR) – Missione 4 Istruzione e ricerca.
> Progetto “DiverSIta – Diversity in spoken Italian”, PI: Caterina Mauri. Codice progetto MUR [P2022RFR8T] –
> CUP [J53D23017320001]

It consists of conversations and semi-structured interviews collected in Turin and
its province, involving speakers of Italian as a foreign or second language. Some
conversations include a `_trad` child tier with an Italian translation of tokens
originally produced in the speaker's other language(s) — see [Translations](#translations).

The transcriptions have been anonymized.

All files are encoded in UTF-8 (without BOM), use LF line endings, and are in Unicode Normalization Form C (NFC), following the conventions of Universal Dependencies.

Overall, the module is made up of 82 conversations and includes 139 speakers.

## Repository organization

This repository contains:

* metadata for both speakers and conversations, in the [`metadata`](./metadata/) subfolder (see [metadata](#metadata) section below)
* descriptions of the set of transcription conventions used for this module ([Transcription conventions](./jefferson-notation.md))
* statistical summaries of each conversation (token counts, speaking time per speaker, token/time rates, overlaps) are not in this repository: they are in the folder of this module in [KIParla-summaries](https://github.com/KIParla/KIParla-summaries)

For each conversation you will find:

* `.eaf` file in [`eaf/`](./eaf/) folder: time-aligned Jefferson-style transcriptions (open with [ELAN](https://archive.mpi.nl/tla/elan)). These files are regenerated from the verticalized `tsv/` files, so they contain the normalized transcription (see [Verticalized content](#verticalized-content)); the audio is linked by relative path (`<code>.mp3`).
* `.txt` file in [`linear-jefferson/`](./linear-jefferson/) folder: linearized Jefferson-style transcription.
* `.txt` file in [`linear-orthographic/`](./linear-orthographic/) folder: linearized transcription retaining only orthographic words.
* `.tsv` file in [`tsv/`](./tsv/) folder: verticalized version of the transcription, with Jefferson-style information decoupled from the text as features. See [Verticalized content](#verticalized-content) for more information.
* `.translations.tsv`/`.translations.json` files in [`translations/`](./translations/) folder, for conversations that include translated tiers. See [Translations](#translations) for more information.

Linear files in [`linear-jefferson/`](./linear-jefferson/) and [`linear-orthographic/`](./linear-orthographic/) contain one Transcription Unit (TU) per line. Each line has two columns: the first is the speaker code, and the second is the transcription. TUs are sorted by their start time.

## Metadata

Each participant and each conversation are associated to a series of metadata, that can be found in the
[`metadata/participants.tsv`](metadata/participants.tsv) and [`metadata/conversations.tsv`](metadata/conversations.tsv) files.
Metadata is to be interpreted as follows:

1. Participants metadata:
	- `code`: unique anonymized identifier for each participant. Unidentified, occasional participants
	 to conversations are transcribed with a `?`/`??`/`???` placeholder code instead and do not have a row here.
	- `occupation`: occupation of the participant, according to [ISTAT categories](https://professioni.istat.it/). For more information see [occupation label](./occupation-levels.md)
	- `gender`: either `M` for masculine or `F` for feminine
	- `conversations`: semicolon-separated list of conversation codes the participant appears in
	- `birth-region`: participant's country of birth (this module's participants are predominantly foreign-born, so — unlike other KIParla modules — actual countries are recorded here rather than Italian regions/`estero`)
	- `age-range`: 5 years range including the participant's age
	- `study-level`: highest completed level of education[^1]
	- `mothertongue`: participant's first language(s)
	- `age-of-arrival-italy`: age range at which the participant arrived in Italy
	- `years-in-italy`: number of years (range) the participant has lived in Italy

2. Conversations metadata:
   - `code`: unique identifier for conversation
   - `type`: type of interaction, either `free-conversation` or `semistructured-interview`
   - `duration`: duration of the conversation, expressed in `hh:mm:ss` format
   - `participants-number`: number of participants in the conversation
   - `participants`: semicolon-separated list of the codes of the participants to that conversation
   - `languages`: `italian` and/or `other`, depending on whether foreign-language speech is present
   - `collection-point`: two-letter code of the collection area: `TO` for Turin for this module
   - `topic`: `fixed` for `semistructured-interview`, `free` for `free-conversation`
   - `moderator`: presence of a moderator (`yes` for `semistructured-interview`, `no` for `free-conversation`)
   - `participants-relationship`: relation between participants, `asymmetric` for `semistructured-interview`, `symmetric` for `free-conversation`
   - `year`: year of collection (not available for this module; `_` where unknown)
   - `unknown-participant`: `yes` if the conversation's transcription contains one or more unidentified-speaker placeholder tiers (`?`, `??`, `???`, ...), `no` otherwise
   - `community`: migrant community the speakers belong to: `moroccan`, `romanian` or `peruvian` (corresponds to the fourth letter of the conversation code: `A`, `R`, `S`)

[^1]: `foreign-diploma`, `liceo-diploma`, `middle-school`, `none`, `phd`, `primary-school`, `technical-vocational-diploma`, `university-degree`, `university-degree-ongoing`

## CSVW metadata

The tabular files of this module are described by a [CSV on the Web (CSVW)](https://www.w3.org/TR/tabular-data-primer/) metadata document, [`csv-metadata.json`](./csv-metadata.json), placed at the root of the repository. It documents `metadata/conversations.tsv`, `metadata/participants.tsv` and every `tsv/<code>.vert.tsv` file, listing for each column its name, datatype (and format, where relevant) and a short description, together with the foreign key linking the `participants` column of the conversations table to the participants table. The file is generated from the shared schemas in the KIParla `tools` repository (`tools/csvw/generate_csvw.py`) and should not be edited by hand. CSVW-aware tools (e.g. the `csvw` Python package, `csvlint`, or R's `csvwr`) can use it to validate the data and load it with the correct types.

## Verticalized content

Conversations are also available in a vertical, pseudo-tokenized version in [`tsv/`](./tsv/).
Tokenization is obtained by validating the Jefferson transcription using custom [tools](https://github.com/LaboratorioSperimentale/kiparla-tools) and splitting on token boundaries: whitespaces, prosodic links (`=`), and apostrophes used for elision in Italian orthography. Each transcription-derived token is then documented on one row.

Each token is represented as 20 columns, as follows:

1. `token_id`: unique token identifier within the conversation (`<tu_id>-<token_index>`)
2. `speaker`: speaker `code` as it can be found in [`metadata/participants.tsv`](metadata/participants.tsv)
3. `tu_id`: progressive identifier assigned to transcription units
4. `id`: token index within the transcription unit (0-based)
5. `span`: portion of the original jefferson transcription containing the token, including any variation marker that precedes it (`#`, `#*`, `$`, a unit-initial `# ` or `#_ `, or a `#_ ` later in the unit), so the original text can be rebuilt from this column
6. `form`: orthographic form of the token. This differs from the `span` as special symbols are stripped out and represented as `jefferson_feats`. Moreover, shortpauses (`(.)` in the transcription) are represented as `[PAUSE]` and unintelligible tokens (sequences of `x` in the transcription) are represented as `x`
7. `lemma`: reserved for a future lemmatization step; `_` for now
8. `upos`: reserved for a future POS-tagging step; `_` for now
9. `xpos`: reserved; `_` for now
10. `feats`: reserved; `_` for now
11. `deprel`: reserved for a future dependency-parsing step; `_` for now
12. `type`: one of
    - `linguistic`: everything that is considered to be a content linguistic token
    - `nonverbalbehavior`: used for transcribed non verbal behaviors, such as laughing or sighing
    - `shortpause`: identifies pauses
    - `unknown`: identifies unintelligible spans in transcription
    - `error`: residual class to mark cases where the transcription is not well formed according to Jefferson format. Therefore, the token is not analyzed and transcription will be corrected in future releases.
13. `meta_label`: reserved; `_` for now
14. `code-variation`: all variation features of the token (having to do with code switching and nonce formations), as pipe-separated `Key=Value` pairs (never empty, as the first one is always present):
    - `ContainsVariation`: unit-level flag, repeated on every token of the unit. `Yes` if any token of the unit has a `Code`, `No` otherwise
    - `Code`: token-level code change (other than standard Italian). Values:
      - `Other`: the token is in another language — a `#word`, or any token after a `#_` marker (which covers the rest of the transcription unit, or the whole unit when it is unit-initial)
      - `Unsure`: the code of the token can be assigned to more than one language (e.g. `#*word`, compatible with Italian and Spanish)
      - `Underspecified`: the token is in a unit that starts with `# `, which means that at least one word of that unit is assignable to a different language
    - `Language=<ISO code>`: present on tokens marked as belonging to a different language (or `NO_ISO_CODE` when the specific variety wasn't identified)
    - `Nonce=Yes`: nonce form that is not assignable to a given language, marked with `$` in the transcription
    Example: `ContainsVariation=Yes|Code=Other|Language=NO_ISO_CODE`
15. `jefferson_feats`: pipe-separated list of word-level features derived from the transcription in Jefferson format. More specifically:
    - `SpaceAfter=No`: no whitespace between this token and the next (e.g., `l'` in `l'anno`)
    - `ProsodicLink=Yes`: a prosodic link (`=`) to the following token
    - `Intonation` can assume values `Falling`, `Rising` or `WeaklyRising` and translates word final punctuation sign in Jefferson transcriptions (i.e., `.`, `?` and `,` respectively)
    - `Interrupted=Yes`: words interrupted in speech, transcribed with final `~` or `-`
    - `Truncated=Yes`: truncated forms (e.g., `anda'` for `andare`, common in some Italian varieties)
    - `Volume` can assume values `High` or `Low` and translates Jefferson's uppercase and `°` respectively
    - `Syllables=N`: number of syllables for `unknown` tokens (sequences of `x`)
16. `align`: alignment features for the first and last token of each TU, through `Begin=` and `End=` features expressed as seconds
17. `prolongations`: positions of sound prolongations (colons `:`) within the word, encoded as a comma-separated list of `<char_id>x<count>` pairs
	- `char_id` is the zero-based index of the character in the token's orthographic form
	- `count` is the number of consecutive colons immediately following that character in the original span
	- example: for span = `ese::mpio:`, its orthographic form is `esempio` and the prolongations field would assume value `2x2,6x1` (the 3rd letter `e` has 2 colons; the 7th letter `o` has 1 colon)
18. `pace`: marks whether the token participates in a fast or slow paced span within the word
	- Format: `Fast=<char_id_start>-<char_id_end>` or `Slow=<char_id_start>-<char_id_end>`
	- Indices are zero-based, inclusive, and refer to character positions in `form`
19. `guesses`: character span(s) transcribed as uncertain (i.e., in round brackets in the Jefferson transcription)
	- Format: `<char_id_start>-<char_id_end>(<guess_id>)` (zero-based, inclusive, over `form`)
20. `overlaps`: comma-separated list of character spans participating in simultaneous speech, with an overlap group identifier
	- Format: `<char_id_start>-<char_id_end>(<overlap_id>)`, where indices are zero-based, inclusive indices over `form` and `overlap_id` is the progressive number of the overlapping group within the TU
	- Examples: the span `e[se]mp[i` would be encoded as `1-3(2),5-6(3)` meaning that characters from position one (inclusive) to three (exclusive) participate to span number 2 while the last character (with id 5) participates to the third overlapping span of the transcription unit. When the overlapping id was not decidable, a `?` is used

## Translations

Some conversations include one or more child tiers (named `<speaker>_trad`) carrying an Italian
translation of that speaker's foreign-language speech. The `environment` tier (non-speech material and speech from external sources such as a video) can have its own child tier, `environment_trad`, handled the same way. These tiers are excluded from the
verticalized `tsv/` output — they are not tokenized or normalized like regular transcription
units — and are instead collected separately in [`translations/`](./translations/):

* `<code>.translations.tsv`/`<code>.translations.json`: one row/object per translated
  transcription unit, with columns/fields:
  - `tu_id`: identifier of the translation unit itself
  - `speaker`: the `<speaker>_trad` tier name
  - `start`/`end`: timestamps in seconds (inherited from the source unit being translated)
  - `parent_tu_id`: `tu_id` of the original transcription unit (in `tsv/<code>.vert.tsv`) that this row translates
  - `text`: the Italian translation, as transcribed (not tokenized/normalized)

## Data access

Due to GDPR restrictions, pseudo-anonymized audio files (MP3) are available under a restricted-access license. To request access, please contact the corpus coordinators through the KIParla website and follow the provided procedure.

## How to cite

If you use the Stra-ParlaTO module in your research, please cite the corpus:

Bernasconi, Beatrice & Goria, Eugenio. 2026. Stra-ParlaTO. DOI: [https://doi.org/10.60760/unibo/stra-parlato](https://doi.org/10.60760/unibo/stra-parlato)

Please also reference the version (commit/tag) of this repository you used in your data statement or appendix.

## Changelog

* 2026-07-14 v1.0.0
  * First release

-----

This work is licensed under a
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].

<!-- [![CC BY-NC-SA 4.0][cc-by-nc-sa-image]][cc-by-nc-sa] -->

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/
[cc-by-nc-sa-image]: https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg
