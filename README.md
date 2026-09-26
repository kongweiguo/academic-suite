# Academic Suite · 学术文献套件

一次编排文献规范命名、完整翻译和论文精读，管理阶段选择、成果位置与断点续作。面向能够读取技能指令并使用所需工具的 agent 或 LLM 工作环境，不绑定模型或产品。

[技能入口](SKILL.md) · [GitHub 仓库](https://github.com/kongweiguo/academic-suite) · [问题反馈](https://github.com/kongweiguo/academic-suite/issues)

## 四个独立技能

| 技能 | 职责 |
| --- | --- |
| [academic-rename](https://github.com/kongweiguo/academic-rename) | 唯一书目命名规则、核验、改名及恢复 |
| [academic-translate](https://github.com/kongweiguo/academic-translate) | 完整对照翻译、图表公式及译文交付 |
| [academic-read](https://github.com/kongweiguo/academic-read) | 数字水印初学者的原理精读与复现指南 |
| academic-suite | 调度上述技能、传递实际源状态、记录整体进度 |

安装 suite 本身不会包含或自动安装三个专业技能。整套处理安装全部四个；只需要某一专业任务时可独立使用相应技能。Suite 不复制专业规则，也不默认执行论文实验。

## 通用安装

推荐以 `~/.agents/skills/` 作为通用的本地存放约定，也可使用自选目录。它不是某个 agent 或模型的私有安装位置，亦不保证所有宿主自动发现：支持发现的宿主按其配置加载，其他宿主显式读取实际 `SKILL.md` 及引用文件。`agents/openai.yaml` 只是可选界面元数据，不是通用加载要求。

### 使用 Git 安装全部技能

需要已有 Git。以下命令仅用于目标目录尚不存在时；已有安装按更新说明处理。默认分支统一为 `master`。

macOS / Linux：

```sh
mkdir -p "$HOME/.agents/skills"
git clone --branch master https://github.com/kongweiguo/academic-rename.git "$HOME/.agents/skills/academic-rename"
git clone --branch master https://github.com/kongweiguo/academic-translate.git "$HOME/.agents/skills/academic-translate"
git clone --branch master https://github.com/kongweiguo/academic-read.git "$HOME/.agents/skills/academic-read"
git clone --branch master https://github.com/kongweiguo/academic-suite.git "$HOME/.agents/skills/academic-suite"
```

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force -Path "$HOME/.agents/skills"
git clone --branch master https://github.com/kongweiguo/academic-rename.git "$HOME/.agents/skills/academic-rename"
git clone --branch master https://github.com/kongweiguo/academic-translate.git "$HOME/.agents/skills/academic-translate"
git clone --branch master https://github.com/kongweiguo/academic-read.git "$HOME/.agents/skills/academic-read"
git clone --branch master https://github.com/kongweiguo/academic-suite.git "$HOME/.agents/skills/academic-suite"
```

### 不使用 Git

分别下载 master 分支 ZIP：[rename](https://github.com/kongweiguo/academic-rename/archive/refs/heads/master.zip)、[translate](https://github.com/kongweiguo/academic-translate/archive/refs/heads/master.zip)、[read](https://github.com/kongweiguo/academic-read/archive/refs/heads/master.zip)、[suite](https://github.com/kongweiguo/academic-suite/archive/refs/heads/master.zip)。解压后将目录分别命名为对应技能名，放入选定目录；`SKILL.md` 应直接位于每个技能根目录，不额外嵌套一层 `*-master`。保留全部引用文件，不覆盖已有修改。

### 显式加载

没有自动发现时，可直接发送普通文字请求，把示意路径换成当前环境可读的实际绝对路径：

```text
请读取 /path/to/skills/academic-suite/SKILL.md。
三个专业技能的入口分别是：
/path/to/skills/academic-rename/SKILL.md
/path/to/skills/academic-translate/SKILL.md
/path/to/skills/academic-read/SKILL.md
请按这些入口读取所需引用，处理我提供的论文。
```

不要求四个目录相邻，只要实际路径明确且可读。纯聊天环境若无法读取文件，需将所需 SKILL 与引用内容提供给模型；实际处理文献仍需要相应读取、写入及查看能力。安装技能不等于安装工具或授权账号。

## 使用与成果

- 使用 academic-suite 完成这篇论文的统一命名、全文翻译和精读。
- 使用 academic-suite 翻译并精读这篇论文，保留源名。
- 使用 academic-suite 先预览整套方案，不修改文件。
- 使用 academic-suite 根据已有进度继续精读，保留已有译文及我的修改。

`$academic-suite` 仅是支持该语法的宿主中的可选调用方式。

默认先确定实际源名，再独立完成翻译和精读；精读以原文为依据。两种成果分别是完整文章，本地放在源旁或指定位置，在线放在原文实际父级或承载容器内。各自后缀和细则由专业技能维护。整体进度 `academic-suite-progress.md` 放在任务工作区，包含原文、译文、精读的真实位置和阶段状态。

已有成果先核实身份再续作，保留用户修改。命名受阻时可用实际源名继续其他可执行阶段。仅预览默认不落盘；复现指南完成不等于实验运行成功，在线草稿不等于在线交付完成。

## 更新与旧版迁移

本次发布将四仓库统一为 `master`，每仓从一个新的 `Initial commit` 开始。持有旧 `main` 或旧历史克隆时，先把个人修改保存在仓库外，将旧安装目录移出技能发现范围，再按安装步骤重新克隆。按文件人工迁入所需改动，不合并或推回旧提交历史；新版本确认可用后可移除旧副本。

在这次重建后的克隆上，常规更新前保留本地修改，然后运行以下命令；macOS、Linux 和 PowerShell 均可使用：

```sh
git -C "$HOME/.agents/skills/academic-rename" pull --ff-only origin master
git -C "$HOME/.agents/skills/academic-translate" pull --ff-only origin master
git -C "$HOME/.agents/skills/academic-read" pull --ff-only origin master
git -C "$HOME/.agents/skills/academic-suite" pull --ff-only origin master
```

无法快进时先核对本地改动和历史，不覆盖本地修改。ZIP 安装通过下载新 ZIP 并对照更新，保留修改后再替换；不要对无 Git 元数据的目录使用 Git 更新命令。更新后按宿主的方式重新读取技能，不假设已加载的会话自动刷新。

## 维护与验收

完整工作流与验收要求见 [SKILL.md](SKILL.md)。通过加载技能进行阅读对照和场景评审，区分文档审查与真实执行。本仓库只有指令和文档，不含安装脚本、校验程序或运行依赖。平台连接和实验依赖不随技能安装自动获得。
