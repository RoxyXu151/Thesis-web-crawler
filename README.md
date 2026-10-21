# Academic Paper Web Crawlers

**English** | [简体中文](README.zh-CN.md)

## Overview

A collection of Python crawlers for major academic publishing websites. The scripts collect paper metadata, including titles, authors, abstracts, keywords, DOIs, publication dates, and journal names. The project also includes tools for integrating data from multiple sources and retrieving citation counts.

**This project is intended for technical discussion and learning. Official APIs are recommended for data retrieval:**

1. [Scopus Preview](https://www.scopus.com/home.uri)
2. [Scopus API document example](https://api.scopus.com/doc-details/documents/2-s2.0-85048982194)

## Features

- **Multiple publishers**: IEEE, ScienceDirect, INFORMS, Taylor & Francis Online, and Ceramics.
- **Multithreaded crawling**: Threaded variants are available for several crawlers.
- **Data integration**: Combine metadata from different sources into a consistent format.
- **Citation counts**: Retrieve citation counts through the Crossref API.
- **Resume support**: Use existing output to locate the previous crawling position.

## Requirements and installation

### Environment

- Python 3.6 or later; choose dependency versions compatible with your Python version.
- Chrome for Selenium-based crawling.
- ChromeDriver compatible with your Chrome version.

### Dependencies

```bash
pip install pandas selenium lxml requests
```

`concurrent.futures` is part of Python's standard library and does not require a separate installation.

## Project structure

```text
Thesis-web-crawler/
├── crawler_code/             # Crawler scripts
│   ├── func.py               # Shared helpers
│   ├── ieee.py               # IEEE crawler
│   ├── ieee-muti.py          # Multithreaded IEEE crawler
│   ├── sciencedirect.py      # ScienceDirect crawler
│   ├── scicedirect_muti.py   # Multithreaded ScienceDirect crawler
│   ├── informs.py            # INFORMS crawler
│   ├── informs-muti.py       # Multithreaded INFORMS crawler
│   ├── tandfonline.py        # Taylor & Francis Online crawler
│   ├── tandfonline-muti.py   # Multithreaded Taylor & Francis Online crawler
│   ├── ceramics.py           # Ceramics crawler
│   └── ceramics-m.py         # Multithreaded Ceramics crawler
├── data_integration.py       # Data integration
├── 获取被引次数.py             # Citation count retrieval
├── note.md                   # Usage notes in English
├── note.zh-CN.md             # Usage notes in Simplified Chinese
├── README.md                 # English documentation (default)
└── README.zh-CN.md           # Simplified Chinese documentation
```

Script filenames are unchanged; use the exact names shown above when running commands.

## Usage

### 1. Crawl paper metadata

Choose the appropriate script from `crawler_code/`:

```bash
# Run the IEEE crawler
python crawler_code/ieee.py

# Run its multithreaded variant
python crawler_code/ieee-muti.py
```

Before running a crawler, configure the input and output paths, target links, resume index files, and any required login details in the script. Paths are relative to the current working directory. See the [usage notes](note.md) for additional configuration details.

### 2. Integrate data

```bash
python data_integration.py
```

This script reads metadata collected from different publishers, selects records based on their source URLs, and writes integrated CSV files by month. Configure its input and output paths before running it.

### 3. Retrieve citation counts

```bash
python 获取被引次数.py
```

This script queries Crossref for citation counts by DOI and updates the data files. By default, it reads `updated_file.csv`, periodically writes `updated_file1.csv`, and saves the final results to `updated_file_final.csv`. Adjust these paths in the script as needed.

## Modules

### Crawlers

- **func.py**: Shared helpers, including locating the previous crawling position.
- **ieee.py / ieee-muti.py**: Collect titles, authors, abstracts, keywords, DOIs, and other metadata from IEEE.
- **sciencedirect.py / scicedirect_muti.py**: ScienceDirect crawlers.
- **informs.py / informs-muti.py**: INFORMS crawlers.
- **tandfonline.py / tandfonline-muti.py**: Taylor & Francis Online crawlers.
- **ceramics.py / ceramics-m.py**: Ceramics crawlers.

### Data processing

- **data_integration.py**: Combine data from different sources into a consistent format.
- **获取被引次数.py**: Retrieve citation counts through the Crossref API.

## Usage considerations

1. Install Chrome and a compatible ChromeDriver before using the crawlers.
2. Some websites require login to access full content; configure the required login details in the scripts.
3. Crawling too quickly may trigger a website's anti-bot mechanisms. Adjust the request intervals as appropriate.
4. Prefer official APIs for data retrieval. This project is intended for technical learning and discussion.
5. Multithreading can improve throughput but may also increase the likelihood of being detected by a website.
6. Complete the crawling steps and save each publisher's data to the configured paths before integration.
7. Keep the resume index file's read and write paths consistent, and configure the paths and URL prefixes passed to `getLast` correctly. See [usage notes](note.md).

## Contributing

Suggestions and improvements are welcome:

1. Add support for more academic websites.
2. Improve crawler performance and stability.
3. Improve data processing and integration.
4. Add data analysis features.

## Disclaimer

This project is intended for academic research and technical learning. Follow the terms and rules of the websites you access. Users are responsible for any legal consequences arising from their use of these tools. Official APIs are recommended for data retrieval.

## License

[MIT License](LICENSE).
