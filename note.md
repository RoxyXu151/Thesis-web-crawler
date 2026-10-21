# Usage notes

**English** | [简体中文](note.zh-CN.md)

## Resume configuration

Keep the resume index file's read and write paths and filenames consistent. Configure the data paths and URL prefixes passed to `getLast` correctly.

Some scripts print a month and index to help record progress:

```python
print(f"m{month}:{index}")
```

## Campus network observations

The original author's notes recorded slower IEEE access and the fastest ScienceDirect access on their campus network. These are observations from that environment; speeds may differ on other networks.

## Data access

Official APIs are recommended for retrieving or downloading data.

See the [project README](README.md) for installation and usage.
