# 学术论文网站爬虫工具

## 项目介绍

本项目是一个针对主要学术论文网站的爬虫工具集合，用于自动化获取学术论文的元数据信息，包括标题、作者、摘要、关键词、DOI、发表日期、发表期刊等。该工具支持多个主流学术网站，并提供数据整合和引用次数获取功能。

**注意：本项目仅作技术讨论和学习使用，推荐使用官方API进行数据获取：**

1. [Scopus preview - Scopus - 欢迎使用 Scopus](https://www.scopus.com/home.uri)
2. [api.scopus.com/doc-details/documents/2-s2.0-85048982194](https://api.scopus.com/doc-details/documents/2-s2.0-85048982194)

## 功能特点

- **多网站支持**：支持IEEE、ScienceDirect、Informs、Taylor & Francis Online、Ceramics等主要学术网站
- **多线程爬取**：部分爬虫提供多线程版本，提高爬取效率
- **数据整合**：将不同来源的数据整合到统一格式
- **引用次数获取**：通过CrossRef API获取论文被引用次数
- **断点续爬**：支持从上次爬取位置继续爬取

## 安装要求

### 环境要求

- Python 3.6+
- Chrome浏览器（用于Selenium爬取）
- ChromeDriver（与Chrome浏览器版本匹配）

### 依赖库

```bash
pip install pandas selenium lxml requests concurrent.futures
```

## 项目结构

```
Thesis-web-crawler/
├── crawler_code/             # 爬虫代码目录
│   ├── func.py               # 通用函数
│   ├── ieee.py               # IEEE网站爬虫
│   ├── ieee-muti.py          # IEEE网站多线程爬虫
│   ├── sciencedirect.py      # ScienceDirect网站爬虫
│   ├── scicedirect_muti.py   # ScienceDirect网站多线程爬虫
│   ├── informs.py            # Informs网站爬虫
│   ├── informs-muti.py       # Informs网站多线程爬虫
│   ├── tandfonline.py        # Taylor & Francis Online网站爬虫
│   ├── tandfonline-muti.py   # Taylor & Francis Online网站多线程爬虫
│   ├── ceramics.py           # Ceramics网站爬虫
│   └── ceramics-m.py         # Ceramics网站多线程爬虫
├── data_integration.py       # 数据整合脚本
├── 获取被引次数.py            # 获取论文引用次数脚本
├── note.md                   # 项目注意事项
└── README.md                 # 项目说明文档
```

## 使用方法

### 1. 爬取论文数据

各爬虫脚本位于`crawler_code`目录下，可以根据需要选择对应网站的爬虫：

```bash
# 运行IEEE爬虫
python crawler_code/ieee.py

# 运行多线程版本
python crawler_code/ieee-muti.py
```

**注意**：使用前需要在脚本中配置相应的登录信息（如有需要）。

### 2. 数据整合

使用`data_integration.py`脚本整合不同来源的数据：

```bash
python data_integration.py
```

该脚本会读取各网站爬取的数据，并根据URL来源进行整合，最终生成按月份分类的整合数据文件。

### 3. 获取引用次数

使用`获取被引次数.py`脚本获取论文的引用次数：

```bash
python 获取被引次数.py
```

该脚本通过CrossRef API获取DOI对应的引用次数，并更新到数据文件中。

## 各模块说明

### 爬虫模块

- **func.py**：提供通用函数，如获取上次爬取位置
- **ieee.py/ieee-muti.py**：IEEE网站爬虫，获取论文标题、作者、摘要、关键词、DOI等信息
- **sciencedirect.py/scicedirect_muti.py**：ScienceDirect网站爬虫
- **informs.py/informs-muti.py**：Informs网站爬虫
- **tandfonline.py/tandfonline-muti.py**：Taylor & Francis Online网站爬虫
- **ceramics.py/ceramics-m.py**：Ceramics网站爬虫

### 数据处理模块

- **data_integration.py**：整合不同来源的数据，统一数据格式
- **获取被引次数.py**：通过CrossRef API获取论文引用次数

## 注意事项

1. 爬虫使用前需要确保已安装Chrome浏览器和对应版本的ChromeDriver
2. 部分网站需要登录才能访问完整内容，请在脚本中配置相应的登录信息
3. 爬取速度过快可能会触发网站的反爬机制，建议适当调整爬取间隔
4. 建议使用官方提供的API接口获取数据，本项目仅作技术学习和讨论使用
5. 使用多线程版本可以提高爬取效率，但也会增加被网站检测的风险
6. 数据整合前确保各网站的数据已爬取完成并保存在正确的路径下
7. 注意index文件输出，读取文件和输出文件要一样，getLast路径和链接需要正确配置

## 贡献与改进

欢迎提出建议和改进意见，可以通过以下方式贡献：

1. 添加对更多学术网站的支持
2. 优化爬虫性能和稳定性
3. 改进数据处理和整合逻辑
4. 增加更多数据分析功能

## 免责声明

本项目仅供学术研究和技术学习使用，请遵守相关网站的使用条款和规定。使用本工具产生的任何法律责任由使用者自行承担。推荐使用官方提供的API接口获取数据。
