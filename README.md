# TF

机巢系统总仓库，包含上位机和固件工作区两个子模块。

| 目录 | 内容 | 仓库 |
| --- | --- | --- |
| `ANA-IEC104/` | IEC104 上位机 | [sigerio/ANA-IEC104](https://github.com/sigerio/ANA-IEC104) |
| `TF-WORK/` | 三个固件工程和公共文档 | [sigerio/TF-WORK](https://github.com/sigerio/TF-WORK) |

```text
TF/
├── ANA-IEC104/          # 上位机子模块
└── TF-WORK/            # 固件工作区子模块，跟踪 main
    ├── xj_jc/          # 机巢主控，普通源码目录
    ├── sun_control/    # 太阳能分发板，普通源码目录
    ├── wether/         # 气象板，普通源码目录
    ├── docs/
    └── copy_hex.bat
```

三个固件工程均直接存放在 `TF-WORK/main` 的目录下。总仓库通过提交号固定子模块版本。

## 获取工程

```bash
git clone --recurse-submodules git@github.com:sigerio/TF.git
```

已有总仓库：

```bash
git pull --ff-only
git submodule update --init --recursive
```

如仅需要三个固件工程，可直接克隆 `git@github.com:sigerio/TF-WORK.git`，无需初始化子模块。

## 更新固件工作区

```bash
cd TF-WORK
git switch main
git pull --ff-only
# 修改、验证并提交工作区中的工程
git push origin main
cd ..
git add TF-WORK
git commit -m "更新固件工作区版本"
git push origin main
```

需先推送工作区提交，再推送总仓库引用。构建方法、协议和验证记录见 [固件工作区说明](TF-WORK/README.md)。
