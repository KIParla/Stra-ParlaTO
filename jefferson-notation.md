
# Jefferson Transcription System - adopted conventions

| Symbol   | meaning                                | explanation                                                                                                                                         |
| -------- | -------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| ,        | weakly rising intonation               | Used at the end of a token to mark the use of weakly rising intonation                                                                              |
| ?        | rising intonation                      | Used at the end of a token to mark the use of rising intonation                                                                                     |
| .        | falling intonation                     | Used at the end of a token to mark the use of falling intonation                                                                                    |
| :        | prolonged sound                        | Indicates a stretched sound, used after the prolonged vowel or consonant. The number of colons reflect the length of the sound prolongation         |
| =        | prosodically linked tokens             | No gap or pause between two tokens                                                                                                                  |
| (.)      | short pause                            | Brief interval, usually between 0.08 and 0.2 seconds                                                                                                |
| TEXT     | higher volume                          | Indicates that words are pronounced louder than surrounding speech                                                                                  |
| TEX~     | interrupted token                      | A final `~` indicated that the token is cut off, usually indicates a false start                                                                    |
| °TEXT°   | lower volume                           | Stretches of text surrounded by degree (`°`) signs indicate that the tokens are pronounced quieter than surrounding speech                          |
| >TEXT<   | faster paced span                      | Stretches of text surrounded by inwards pointing arrows (`>...<`) indicate that the pace of the speech has quickened                                |
| \<TEXT\> | slower paced span                      | Stretches of text surrounded by outwards pointing arrows (`<...>`) indicate that the pace of the speech has slowed down                             |
| [TEXT]   | overlapping span                       | Stretches of text surrounded by square brackets indicate overlapping speech                                                                         |
| (TEXT)   | hard to understand span                | Stretches of text surrounded by round brackets indicate unclear speech                                                                              |
| xxx      | non-comprehensible sequence            | Used for unintelligible tokens. The number of `x`s roughly correspond to the number of syllables                                                    |
| ((TEXT)) | non verbal behavior                    | Double parentheses indicate comments and non verbal behaviours such as laughs, sighs etc.                                                           |
| #word    | code-switching/code-mixing (word)      | Placed immediately before a single token to mark that word as belonging to another language or dialect                                              |
| #\*word  | doubtful code-switching (word)         | Placed immediately before a single token to mark it as *possibly* non-Italian/dialect, when the transcriber is unsure                                |
| # (unit-initial) | code-switching, not attributable | Placed at the very start of a transcription unit (`# `, followed by a space) to indicate the unit contains code-switching that cannot be attributed to specific words |
| #_ (unit-initial) | whole unit in another language/dialect | Placed at the very start of a transcription unit (`#_`) to indicate the entire unit is in a non-Italian language or dialect                     |
| $word    | emerging/non-standard form             | Placed immediately before a single token to mark it as a non-standard or emerging spelling — not code-switching, a distinct phenomenon               |

## Rendering of variation markers (`# `, `#word`, `#_`, `#*word`, `$word`) across outputs

- **Linear (Jefferson and orthographic `.txt`)**: both formats reconstruct the original marker as-is — `# `/`#_` prefixed once at the start of the transcription unit, `#word`/`#*word`/`$word` on the individual word. In a `#_`-prefixed unit the words themselves are **not** additionally re-marked with `#`, since the unit-initial `#_` already covers every word.
- **HTML**: `# `/`#_`/`#word`/`#*word` (code-switching, confirmed or doubtful) share one highlight color in both the Jefferson and orthographic views. `$word` (emerging — a non-standard/emerging spelling, *not* code-switching) gets its own, different color.
- **NoSketch Engine**: a `language_variation="yes"` attribute is set on the whole `transcription_unit` for `# `/`#_`/`#`/`#*` (any code-switching in the unit) — `$` never sets it, since it isn't code-switching. At word level, a `variation` attribute is set to `token` for a `#`-marked word or one belonging to a `#_`-prefixed unit (its `word` value is also prefixed with `#`, so `#_` reads exactly like an explicit per-word `#` once compiled), or `doubtful` for `#*` (its `word` value prefixed with `#*`). A separate `non_standard_form="yes"` attribute (and a `$`-prefixed `word` value) marks `$` tokens, kept apart from `variation` since it's a different phenomenon.