# Academic Suite · 学术文献套件

一次编排文献规范命名、完整翻译和论文精读，交接共享编号，维护成果互联、论文索引与断点续作。面向能够读取技能指令并使用所需工具的 agent 或 LLM 工作环境，不绑定模型或产品。

[技能入口](SKILL.md) · [GitHub 仓库](https://github.com/kongweiguo/academic-suite) · [问题反馈](https://github.com/kongweiguo/academic-suite/issues)

## 四个独立技能

| 技能 | 职责 |
| --- | --- |
| [academic-rename](https://github.com/kongweiguo/academic-rename) | 唯一共享编号与目录取号、书目命名和类型标记规则、改名及恢复 |
| [academic-translate](https://github.com/kongweiguo/academic-translate) | 完整对照翻译、图表公式及译文交付 |
| [academic-read](https://github.com/kongweiguo/academic-read) | 数字水印初学者的原理精读与复现指南 |
| academic-suite | 调度上述技能、传递实际编号和源状态、协调互联、维护论文索引与整体进度 |

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
- 使用 academic-suite 为这个集合的已有原文、译文和精读建立论文索引并补齐互链，不生成缺失成果。

`$academic-suite` 仅是支持该语法的宿主中的可选调用方式。

阅读时从“论文索引”找到完整题名，再点击原文、翻译或精读入口；进入译文或精读后，可通过开头导航切换同篇文档。共享编号帮助目录排序，索引和导航帮助直接访问，不需要靠比对三个长文件名寻找关联。

默认先由 rename 核实可复用的同源同版本编号或按当前目录取号、确定实际源名和已核实基本名 `B`，再独立完成翻译和精读；精读以原文为依据。编号以 rename 的[共享编号与目录取号](https://github.com/kongweiguo/academic-rename/blob/master/references/naming.md#共享编号与目录取号)为准，类型识别与基本名提取以其[唯一命名规范](https://github.com/kongweiguo/academic-rename/blob/master/references/naming.md#类型前缀与基本名)为准。Suite 传递实际父目录路径或在线父容器 ID（`scope_location`）、实际编号、源稳定身份、版本与真实成果，不自行编号或从实际源名重新拼接标签。

以核实的 `P001` 为例，新命名形式为 `[P001][原文]B.pdf`（保留真实扩展名）；本地完整成果为 `[P001][翻译]B/[P001][翻译]B.md`、`[P001][精读]B/[P001][精读]B.md`，在线成果使用对应的编号与类型名称。具体输出结构由专业技能提供；两项成果本地放在源旁或指定位置，在线放在原文实际父级或承载容器内。选择保留源名时原文名称不变，普通内容任务取号不启动 CCF 查询或改源。原文未编号或只读时，也可核实复用实际成果名中的编号。

整套任务在本地集合根目录或指定位置创建或复用 `论文索引.md`；在线在原文实际父级容器内同级创建或复用原生 `论文索引`，保持原文层级。新索引默认六列：编号、完整题名与版本、原文、翻译、精读、状态与备注。阶段状态写在成果链接旁，命名或导航受限项放在备注列，保留已有用户自定义列和注释。单目录在开头记录实际范围，行内显示 `P001`；跨目录统一索引首列同时注明范围和编号。索引按实际源稳定身份、版本与范围更新，编号只作显示，无编号旧成果也可加入。索引、`academic-suite-progress.md` 和恢复日志各保留原有职责，均不作为取号依据，不另造发号台账。

需要新取号时，同批候选号在当前任务内协调，写前重读目录并串行产生每篇首个真实带编号资源，回读后交接给其余成果；候选计划不代表已占号。每个阶段取得真实结果后，Suite 协调专业技能更新自身完整成果顶部的“原文｜翻译｜精读”导航，再回读更新索引；并行生成期间不互写对方报告，汇合后串行补齐互链与索引。缺失成果只呈现真实状态，候选 URL 不生成链接。本地索引链接从索引所在目录计算并逐路径段编码，不能照搬报告内的相对链接；在线使用核实过的稳定资源 URL。无法完整列举目录而不能新取号时，仍可继续内容及已核实来源的无编号索引、互联。已有译文只读而无法补链时，仍交付可用精读与索引，并标明导航待同步。单项专业任务可独立执行，不依赖 Suite 或自动创建全库索引；显式索引或互联任务只整理授权范围内已有成果。

已有成果先核实身份与版本再续作，保留用户修改；旧版类型前缀、`_翻译`、`_精读` 仍沿用原路径或在线 ID，不随规则更新自动迁移。显式要求迁移时，由 rename 规划名称和恢复记录，专业技能修复可验证引用，Suite 回读后更新索引。不同目录同号或旧资源删除后新论文再次取到该号，都不能据编号合并或覆盖旧索引行。编号或命名受阻时继续其他可执行工作并标注待处理，不使用候选编号或名称冒充真实结果。仅预览不写编号资源、索引、正文或执行记录；复现指南完成不等于实验运行成功，在线草稿不等于在线交付完成。

## 更新与旧版迁移

四仓库此前已统一为 `master`，各自从新的 `Initial commit` 开始，后续功能更新以普通提交发布。本次更新无需再次重建历史。只有仍持有重建前的旧 `main` 或旧历史克隆时，才先把个人修改保存在仓库外，将旧安装目录移出技能发现范围，再重新克隆；按文件迁入所需改动，不合并或推回旧提交历史。

在历史重建后的克隆上，常规更新前保留本地修改，然后运行以下命令；macOS、Linux 和 PowerShell 均可使用：

```sh
git -C "$HOME/.agents/skills/academic-rename" pull --ff-only origin master
git -C "$HOME/.agents/skills/academic-translate" pull --ff-only origin master
git -C "$HOME/.agents/skills/academic-read" pull --ff-only origin master
git -C "$HOME/.agents/skills/academic-suite" pull --ff-only origin master
```

无法快进时先核对本地改动和历史，不覆盖本地修改。ZIP 安装通过下载新 ZIP 并对照更新，保留修改后再替换；不要对无 Git 元数据的目录使用 Git 更新命令。更新后按宿主的方式重新读取技能，不假设已加载的会话自动刷新。

## 维护与验收

完整工作流与验收要求见 [SKILL.md](SKILL.md)，索引维护见[论文索引与互联交接](references/paper-index.md)。通过加载技能进行阅读对照和场景评审，覆盖编号复用、多集合同编号、版本变化、并行部分完成、只读来源及成果、用户修改、旧成果续作与重复运行，区分文档审查与真实执行。本仓库只有指令和文档，不含安装脚本、校验程序或运行依赖。平台连接和实验依赖不随技能安装自动获得。
