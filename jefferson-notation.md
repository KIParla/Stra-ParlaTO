
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

## Rendering of code-switching markers (`# `, `#word`, `#_`) across outputs

- **Linear (Jefferson and orthographic `.txt`)**: both formats reconstruct the original marker as-is — `# `/`#_` prefixed once at the start of the transcription unit, `#word` on the individual word. In a `#_`-prefixed unit the words themselves are **not** additionally re-marked with `#`, since the unit-initial `#_` already covers every word.
- **HTML**: the same markers are highlighted with a dedicated color in both the Jefferson and orthographic views.
- **NoSketch Engine**: a `language_variation="yes"` attribute is set on the whole `transcription_unit` for `# ` and `#_` (and any unit containing a `#`/`#*`-marked word). At word level, a `variation` attribute is set to `yes` for a token carrying an explicit `#`, or belonging to a `#_`-prefixed unit (its `word` value is also prefixed with `#`, so `#_` reads exactly like an explicit per-word `#` once compiled). `#*` (doubtful) tokens are a separate convention and are not covered by this `variation` attribute for now.

**TODO**: `#*word` (doubtful) and `$word` (emerging) currently get no special treatment in linear/HTML output (no reconstructed marker, no color) and no NoSketch `variation`/`#`-prefixed word text — they should eventually be handled the same way `#word` is now, once we decide whether to fold them into the same `variation` attribute or track them separately (e.g. `variation=doubtful`/`variation=emerging`).