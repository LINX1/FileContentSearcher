# 文件内容搜索器

这是一个 Windows 桌面文件全文搜索工具：

- 选择文件夹后递归扫描子目录；
- 扫描进度按文件总数显示；
- 扫描前统计阶段会实时显示已发现的文件数量，避免大目录长时间停留在 `0 / 0`；
- 使用线程池并行提取文件内容和执行关键词搜索，分批处理以控制内存和任务数量；
- 搜索同时匹配文件名和正文，并标记命中来源；
- 顶部显示当前环境是否检测到 Microsoft Office 和 WPS，并支持中英文界面切换；
- 支持 TXT、SQL、CSV、JSON、XML、HTML、代码文件等文本文件；
- 支持 PDF、DOC/DOCX/DOCM、WPS、XLS/XLSX/XLSM、PPT/PPTX/PPTM；
- 支持 ODT/ODS/ODP、EPUB、EML 邮件、SQLite/DB 数据库；
- 支持 VSDX Visio 文件，提取页面图形中的文字；
- 支持 ZIP/JAR/WAR/APK 等压缩容器中的文本文件；
- 对未知扩展名会先检测实际内容，确认是文本后按普通文本加载，不会因扩展名不在列表中而漏检；
- 将成功解析的文字内容加载到内存；
- 扫描完成后在程序目录生成压缩快照 `last_snapshot.json.gz`，比未压缩 JSON 更节省空间；
- 扫描失败和不支持的文件会记录到程序目录的 `load_errors.txt`；常见的二进制 SVN 元数据、Office 临时文件、系统噪声文件和无效容器会跳过，但其中实际为文本的文件仍会加载，并按原因汇总，只保留少量示例路径；
- 下次启动仅在程序目录存在快照时显示“加载上次快照”按钮，点击后手动恢复；
- “重新加载”按钮会重新扫描当前文件夹并覆盖快照；
- 左侧显示命中文件绝对路径，右侧显示完整文本并高亮关键词；
- 双击左侧结果可以用系统默认程序打开原文件。

## 运行源码

```powershell
python search_text_app.py
```

## 打包 EXE

需要网络安装依赖时运行：

```powershell
.\build_exe.ps1
```

生成文件为 `dist\FileContentSearcher\FileContentSearcher.exe`。运行时请保留 EXE 旁边的 `_internal` 文件夹。快照文件 `last_snapshot.json.gz` 会生成在 EXE 所在目录。

旧版 `.doc` 已内置 Antiword 和 OLE 文本解析通道，优先不启动 Office/WPS 即可提取标准二进制 Word 文本；如果本机安装了 Microsoft Word 或 WPS，程序会通过 `pywin32` 调用对应的 Writer 作为备用转换通道，再尝试 LibreOffice。`.wps` 文件优先通过 WPS Writer 打开，也会尝试 Word。Antiword 无法识别的标准/WPS `.doc` 会按此顺序处理。Word/WPS/PowerPoint/Excel 通道单文件最多等待 20 秒；通道超时后仍会继续尝试后续文件，避免漏掉偶尔能被 Office 打开的文档，但如果 Office 本身异常，多个文件会分别等待超时。旧版 `.ppt` 会优先调用本机 PowerPoint 提取文字，再尝试 LibreOffice；旧版 `.xls` 在 `xlrd` 失败后会尝试本机 Excel。程序会自动查找系统中的 `soffice.exe`，也支持将 LibreOffice 目录放到 `tools\libreoffice`（要求存在 `tools\libreoffice\program\soffice.exe`），打包脚本会自动将其带入 EXE。顶部的 Office/WPS/LibreOffice 复选框默认勾选已检测到的工具；取消勾选后本次扫描不会调用对应系统工具，未安装的工具保持不可勾选。
