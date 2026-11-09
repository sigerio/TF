# TF

机巢系统总仓库，通过 Git 子模块固定各工程的版本。

| 目录 | 工程 | 远端仓库 | 跟踪分支 |
| --- | --- | --- | --- |
| `ANA-IEC104` | IEC104 上位机 | [sigerio/ANA-IEC104](https://github.com/sigerio/ANA-IEC104) | 沿用原有提交 |
| `xj_jc` | 机巢主控 | [TF-WORK / xj_jc](https://github.com/sigerio/TF-WORK/tree/xj_jc) | `xj_jc` |
| `sun_control` | 太阳能分发板 | [TF-WORK / sun_control](https://github.com/sigerio/TF-WORK/tree/sun_control) | `sun_control` |
| `wether` | 气象板 | [TF-WORK / wether](https://github.com/sigerio/TF-WORK/tree/wether) | `wether` |

三个固件工程各自保留原有 Git 历史，存放在 `TF-WORK` 的三条独立分支。
总仓库以子模块提交号固定版本；`.gitmodules` 中的分支用于显式更新，普通拉取不会自动换成分支最新提交。

## 获取工程

```bash
git clone --recurse-submodules git@github.com:sigerio/TF.git
```

已有总仓库：

```bash
git pull --ff-only
git submodule update --init --recursive
```

## 更新固件工程

子模块检出后通常处于 detached HEAD。修改前在对应目录建立工作分支，并显式推送到该工程的远端分支。例如更新主控：

```bash
cd xj_jc
git switch -c work
# 修改、验证并提交
git push origin HEAD:xj_jc
cd ..
git add xj_jc
git commit -m "更新主控子模块版本"
git push origin main
```

`sun_control`、`wether` 分别推送到同名远端分支。需先推送子模块提交，再推送总仓库引用。

## 构建与文档

分别使用三个工程 `MDK/` 下的 Keil 工程文件构建。构建完成后，可运行 `copy_hex.bat` 将三个 HEX 复制到总目录；生成的 HEX 不纳入总仓库。

- [系统通信与设计整理](docs/系统通信与设计整理.md)
- [主控工程说明](xj_jc/docs/README.md)
- [主控 IEC104 协议](xj_jc/iec104_protocol_spec.md)
- [门平台测试模式需求与验证记录](xj_jc/docs/门平台测试模式需求说明.md)

主控当前包含104测试模式。其软件验证结果和既有测试限制见需求文档；本次仓库整理不表示固件已经过实机验证。
