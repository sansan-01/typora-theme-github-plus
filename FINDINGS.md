# Security and robustness audit

Locations in existing files refer to the audited revision before edits. The audit covered both theme variants, bundled assets, and repository documentation. The tree contained no package manifests, CI workflows, or executable source. No suspected credentials were found in the reviewed tree.

| Severity | Location | One-line risk | Fix applied |
| --- | --- | --- | --- |
| medium | `github-plus.css:6`, `github-plus-watermark.css:6` | The export directive can make styled HTML exports fetch mutable third-party CSS and disclose viewer network metadata to the font host. | Removed the remote Open Sans directive from both variants. |
| low | `github-plus.css:13`, `github-plus-watermark.css:13` | Four Open Sans sources per variant depend on files outside the documented theme bundle and may fail to load on a standalone installation. | Removed the unbundled file URLs and retained the installed-font lookups. |
| low | `.gitignore:1` | Local environment files, editor settings, and OS metadata could be staged accidentally. | Added ignore rules that allow `.env` example files to be tracked. |
| low | `README.md:3`, `README.md:77` | Empty Google search links are unusable, and the license link sends readers to a search page for the terms. | Removed the empty links and linked directly to the local `LICENSE` file. |
| low | `README.md:7`, `README.md:13` | The font description promises uniform Chinese rendering even though both bundled fonts lack Han glyphs. | Documented the fonts used for prose and code and the system fallback for Chinese glyphs. |
| low | `README.md:23` | The watermark wording implies copyright protection from a visual overlay. | Described the editor and print/PDF watermark as a visual overlay. |
| low | `README.md:44` | The install tree lists just one GIF, which may lead readers to omit assets used by the carousel. | Required the complete `fonts` and `img` directories in the install example. |
| low | `README.md:62`, `README.md:65` | A WOFF2 replacement can fail if its path changes while the `format(...)` hint still describes a TrueType file. | Documented updating the path and format hint together. |
| low | `README.md:77`, `github-plus.css:421`, `github-plus.css:431` | The README describes the project as MIT-licensed, while the bundled fonts identify a separate license and ship without its full text. | Clarified the distinction in the README. Report-only for the missing font notices because the exact upstream notices for the bundled builds need verification. |

Local checks verified that CSS asset paths and README preview and license paths resolve, that the CSS has no external resource URLs, and that the ignore rules match the intended files. Export rendering requires verification in Typora.
