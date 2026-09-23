# my-skills

个人维护的 Codex Skills 集合。每个技能独立存放在 `skills/<skill-name>/`，新增技能直接提交到这个仓库，无需再创建独立仓库。

## 技能目录

| 技能 | 用途 | 主要依赖 |
| --- | --- | --- |
| [zgh-wechat-short-draft](skills/zgh-wechat-short-draft/) | 参考公众号素材创作原创情感短文或无字竖版贴图，完成封面、排版与飞书草稿入库 | Codex 图片生成、lark-cli、lark-base；文章模式另需 zgh-space-wechat-layout |

### 公众号短文与贴图

- **文章**：正文最多300字，2.35:1无字封面，可复制到公众号的HTML排版。
- **贴图**：默认20–60字独立配文，9:16无字竖图，文案不印在图片上。
- 注重原创、情感表达及完整结尾，每条成稿写入用户指定的飞书草稿表并回读核验。

完整规则、依赖和使用示例见该技能的 [README](skills/zgh-wechat-short-draft/README.md) 与 [SKILL.md](skills/zgh-wechat-short-draft/SKILL.md)。依赖技能并未全部收录，安装本仓库不代表已具备全部运行条件。

## 安装技能

先把仓库克隆到普通工作目录，**不要把整个仓库当作一个技能安装**：

```bash
git clone https://github.com/Clearleaves/my-skills.git
```

再将所需的技能文件夹复制到 Codex 技能目录。如果配置了 `CODEX_HOME`，目标目录是其中的 `skills/`；否则默认是 `~/.codex/skills/`。

### Windows PowerShell

在刚克隆的仓库目录执行：

```powershell
$skillsRoot = if ($env:CODEX_HOME) { Join-Path $env:CODEX_HOME 'skills' } else { Join-Path $env:USERPROFILE '.codex/skills' }
$skillDestination = Join-Path $skillsRoot 'zgh-wechat-short-draft'
if (Test-Path -LiteralPath $skillDestination) {
    throw '技能已存在，请先备份并比较后再更新，保留自己的本地配置。'
}
New-Item -ItemType Directory -Path $skillsRoot -Force | Out-Null
Copy-Item -LiteralPath './skills/zgh-wechat-short-draft' -Destination $skillDestination -Recurse
```

### macOS / Linux

在刚克隆的仓库目录执行：

```bash
skills_root="${CODEX_HOME:-$HOME/.codex}/skills"
if [ -e "$skills_root/zgh-wechat-short-draft" ]; then
  echo '技能已存在，请先备份并比较，保留本地配置。'
else
  mkdir -p "$skills_root"
  cp -R skills/zgh-wechat-short-draft "$skills_root/"
fi
```

重新打开 Codex 加载技能。安装成功后可按名称调用：

```text
使用 $zgh-wechat-short-draft，参考我指定的素材表，做一条贴图。
图片不要有字，文案单独保存到我的草稿。
```

更新时先在仓库执行 `git pull --ff-only`，比较技能目录后同步所需文件，保留 `*.local.md` 等个人配置。

## 目录约定

```text
my-skills/
├── README.md
└── skills/
    └── <skill-name>/
        ├── SKILL.md          # 技能入口，必需
        ├── README.md         # 安装与使用说明，按需
        ├── references/       # 参考资料，按需
        ├── scripts/          # 可执行辅助脚本，按需
        └── assets/           # 模板或素材，按需
```

添加技能时：

1. 新建 `skills/<skill-name>/`，名称使用小写字母、数字与连字符。
2. 提供含 `name`、`description` 前置信息的 `SKILL.md`，说明触发条件、流程、依赖和交付结果。
3. 只收录必要文件，验证技能格式；有脚本时验证实际行为。
4. 在本页技能目录登记用途和依赖。
5. 检查后提交到同一仓库。

## 配置与数据

仓库只维护可复用技能，不包含个人飞书Base地址、表ID、认证凭证、采集文章或生成结果。本地专用配置使用 `*.local.md` 等已忽略文件保存；密钥使用对应工具的认证机制管理。

从独立仓库迁入的首个技能是 `zgh-wechat-short-draft`。原仓库暂时保留，后续维护可集中在本仓库。

## 使用与授权

生成内容需要人工审阅。本仓库不保证阅读量或AI检测结果。当前未附带开源许可证；公开可见不等于授予任意转载、修改和再分发许可，需要时请联系仓库作者。
