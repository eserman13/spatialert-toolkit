# spatiAlert Toolkit

Free tools for cleaning data and finding hotspots of undervaccination. **RecordMatcher** matches and merges files using identifiers like school name or ID, **PlaceFinder** turns addresses into coordinates, and **spatiAlert** maps Getis-Ord Gi* hotspots. The two HTML tools run in your browser; spatiAlert runs locally in R.

**Use the tools:** https://eserman13.github.io/spatialert-toolkit/

## How the tools fit together

| Step | Tool | What it does | Where it lives |
|---|---|---|---|
| 1. Prepare | **RecordMatcher** | Matches and merges records between two or more files that don't share a clean ID | This repo (`tools/RecordMatcher.html`) |
| 2. Prepare | **PlaceFinder** | Turns addresses into latitude and longitude | This repo (`tools/PlaceFinder.html`) |
| 3. Analyze | **spatiAlert** | Detects Getis-Ord Gi* hotspots from point or area-aggregated data | [Its own repo](https://github.com/eserman13/spatiAlert) |

The first two steps get school-level vaccination data into the shape spatiAlert needs. Each tool also works on its own.

## RecordMatcher

Matches records between files that don't necessarily share a clean ID, for example matching school vaccination data to one or more school address or school enrollment files using school name, then merges the data.

- **Accepts:** `.csv`, `.tsv`, `.txt`, `.xlsx`, `.xls`, `.xlsm`, `.ods`
- **What each file needs:** a column to match on, such as school name or ID. One column works; two usually works better. An optional grouping column (for example district or county) limits matching to records in the same group.
- **Produces:** a merged CSV in which every row carries its match score, how the match was decided, and whether it was reviewed, plus an optional clean-up step.
- **Progress:** you can save your work as a `.json` file and resume later.

## PlaceFinder

Turns addresses into latitude and longitude.

- **Accepts:** `.csv`, `.tsv`, `.txt`, `.xlsx`, `.xls`, `.xlsm`, `.ods`
- **What the file needs:** address information, either as separate street, city, and state columns or as one full-address column. An optional county column checks each result against the expected county.
- **How lookups work:** addresses are sent to the US Census geocoder. You can also choose to try OpenStreetMap for addresses the Census geocoder can't find. Each row records where its coordinates came from.
- **Produces:** your file with coordinates added, plus a step for fixing addresses that failed.
- **Progress:** you can save your work as a `.json` file and resume later.

## spatiAlert

A Shiny app that detects spatial hotspots of undervaccination using the Getis-Ord Gi* statistic. It runs locally in R. For installation, data requirements, and a walkthrough, see the [spatiAlert repository](https://github.com/eserman13/spatiAlert) and its [Getting Started Guide](https://github.com/eserman13/spatiAlert/blob/main/spatiAlert_Getting_Started.pdf).

## Working with sensitive data

RecordMatcher and PlaceFinder process your files inside your browser, and your files are not uploaded to a server. For sensitive data, download the tool and run it locally rather than opening it online. One exception applies to PlaceFinder: addresses are sent to the US Census geocoder (and to OpenStreetMap, if you turn that option on) to be looked up, whether you use the online or downloaded copy.

## What's in this repository

```
index.html                  The toolkit web page
tools/
  RecordMatcher.html        Single-file tool; download it and open in a browser
  PlaceFinder.html          Single-file tool; download it and open in a browser
images/                     Screenshots shown on the web page
LICENSE                     MIT license
README.md                   This file
```

To use a tool offline, download its HTML file from the `tools/` folder (or use the Download buttons on the web page) and open it in any modern browser.

## Tutorials and sample data

Video tutorials and sample files are planned. They will be linked from the web page when ready.

## Citation

Serman EA. spatiAlert Toolkit (RecordMatcher v1.0, PlaceFinder v1.1). 2026. https://eserman13.github.io/spatialert-toolkit/

## Questions or problems

Contact Emily A. Serman, eserman@clemson.edu, or open an issue in this repository.

## License

MIT. See [LICENSE](LICENSE).
