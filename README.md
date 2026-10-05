# job-radar-directory

A shared, public directory of companies per city, for [job-radar](https://github.com/calbrecht07/job-radar).
For every company: its website, industries, careers page, and how its jobs can be read. No personal data:
which roles anyone wants, or what they think of a company, lives in their own private data repo.

The weekly company search of every job-radar user reads the folder for their city, and (with write access)
adds what it learns, so the next person searching the same city starts where the last one left off.

## Layout

```
cities/<city>/companies.csv   the directory
cities/<city>/sources.csv     pages that list companies in this city (re-read every week)
```

`companies.csv` columns:

| column | |
|---|---|
| `key` | website domain (or `name:<name>` when unknown) |
| `name`, `website`, `wikidata` | the company |
| `kind` | `startup`, `corporate` (large or listed) or `vc` |
| `industries` | `;`-separated, from Wikidata, directories and research |
| `employees` | from Wikidata, when known |
| `sources` | where it was found: `wikidata:city`, `wikidata:industry:<term>`, `directory:<name>`, `portfolio`, `research` |
| `careers_url` | the page that lists its jobs |
| `method` | how jobs are read: `feed` (a supported job board, see `board`), `jobdata` (schema.org job data), `enterprise` (a recruiting system without an adapter yet, see `enterprise`), `page` (job links), `js_only`, `no_jobs`, `none` (no careers page), `blocked` (refuses automated requests), `dead` |
| `board` | `ats:slug` for `feed` |
| `checked`, `first_seen`, `error` | discovery bookkeeping |

`sources.csv` columns: `url,name,type,industries,added,added_by`; `type` is `getro`, `consider`, `list` or `auto`.

## Contributing

Corrections are welcome as pull requests: a wrong website or careers page, a company that closed, a directory
page for your city. Rows are rewritten by the weekly runs, so fix the source (Wikidata, the directory page) when
the error comes from there.
