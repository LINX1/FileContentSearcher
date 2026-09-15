# FileContentSearcher

Windows 桌面文件内容搜索器，支持递归扫描文件夹、提取多种格式文件的文字，并按文件名和正文搜索。

## 使用方法

1. 下载本目录中的 `FileContentSearcher.exe` 和 `_internal` 文件夹，并保持二者位于同一目录。
2. 双击运行 `FileContentSearcher.exe`。
3. 选择需要扫描的文件夹，等待文件加载完成。
4. 输入关键词进行搜索，左侧查看命中文件，右侧查看并高亮正文内容。

## 支持格式

支持 TXT、SQL、CSV、JSON、XML、HTML、常见代码文件、PDF、DOC/DOCX、XLS/XLSX、PPT/PPTX、WPS、VSDX、ODT/ODS/ODP、EPUB、EML、SQLite，以及部分 ZIP/JAR/WAR/APK 容器中的文本文件。

程序会根据当前环境尝试使用 Microsoft Office、WPS 和 LibreOffice 解析旧版 Office 文件。未安装的工具会自动禁用，也可以手动取消已安装工具的调用。

## 快照和日志

- 扫描完成后，程序会在 EXE 所在目录生成 `last_snapshot.json.gz`。
- 下次启动时不会自动恢复快照；存在快照时点击“加载上次快照”即可恢复。
- 加载失败、跳过和不支持的文件会记录在 `load_errors.txt`。
- 快照和日志属于本地运行数据，不包含在发布包中。

## 注意事项

- 请保留 `_internal` 文件夹，否则程序无法正常启动。
- 旧版 `.doc`、`.xls`、`.ppt` 的解析效果取决于本机安装的 Office/WPS/LibreOffice。
- 大型文件夹首次扫描需要一定时间，程序会显示扫描和加载进度。

## English

### Overview

FileContentSearcher is a Windows desktop full-text search tool. It recursively scans a selected folder, extracts text from supported files, and searches both file names and file contents with highlighted matches.

### Usage

1. Keep `FileContentSearcher.exe` and the `_internal` folder in the same directory.
2. Run `FileContentSearcher.exe`.
3. Select a folder and wait for scanning to finish.
4. Enter a keyword to search. Select a result to view its content and highlighted matches.

### Supported formats

The application supports text and source files, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, WPS, VSDX, ODT/ODS/ODP, EPUB, EML, SQLite, and text files inside some ZIP/JAR/WAR/APK containers.

When available, Microsoft Office, WPS, and LibreOffice can be used as fallback parsers for legacy Office documents. Missing tools are disabled automatically, and installed tools can be unchecked to prevent their use.

### Snapshots and logs

- After scanning, `last_snapshot.json.gz` is saved next to the executable.
- The application does not restore a snapshot automatically at startup. If a snapshot exists, click **Load Previous Snapshot** to restore it.
- Loading failures, skipped files, and unsupported files are recorded in `load_errors.txt`.
- Snapshots and logs are local runtime data and are not included in the release package.

### Notes

Keep the `_internal` folder next to the executable. Parsing results for legacy `.doc`, `.xls`, and `.ppt` files depend on the Office, WPS, or LibreOffice software installed on the computer.
