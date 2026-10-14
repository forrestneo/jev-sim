# jev-sim：会话内决策模型

用 ZCode 会话内的大模型模拟 Jev 式类型化决策：**Choice（选择）/ Noul（真假概率）/ Score（量规评分）**——零外部决策模型 API、零密钥、数据不出本机。[English](./README.md)

## 在 ZCode 里安装（现在就能装，不用等审核）

**方式 A —— CDN 市场（任何网络都能用，包括 github.com 被屏蔽的环境）：**

在 **插件市场 → 添加 → 添加插件市场** 粘贴：

```
https://cdn.jsdelivr.net/gh/forrestneo/jev-sim@main/marketplace-cdn.json
```

添加后 **个人 → forrestneo-jev-sim → jev-sim → 安装**。

**方式 B —— 直接添加本 GitHub 仓库：**

1. 打开 **插件市场 → 添加 → 添加插件市场**
2. 粘贴本仓库地址：`https://github.com/forrestneo/jev-sim`
3. 添加后在 **个人 → forrestneo-jev-sim → jev-sim → 安装**
4. 新建任务，在 composer 里选中 jev-sim 技能，直接给判断题：

> 背景：发件人李某，正文：你们平台 2 号下单的椅子到货就是断腿的，联系客服三天没人理，今天不给我退款，我就去12315投诉并且找律师发函。
> 问题：这封邮件路由给哪个团队？选项：市场 / 客服-退款 / 法务 / 销售

预期：3 个轮转采样的判官子代理，聚合输出各选项概率和 `status`（`answer` / `none` / `clarify`）。

同一插件也已提交官方插件市场审核（[zai-org/zcode-plugins#94](https://github.com/zai-org/zcode-plugins/pull/94)），合并后也可以直接从官方市场安装。

## 文档

完整文档随插件存放：[README_CN.md](./plugins/jev-sim/README_CN.md)（中文）/ [README.md](./plugins/jev-sim/README.md)（EN）——含决策协议、输出契约、校准流程、测试结果和诚实的局限说明。

| 原语 | 输入 | 输出 |
|---|---|---|
| Choice | 背景 + 问题 + 选项 | 每个选项的概率 + NONE 出口 |
| Noul | 背景 + 命题 | 命题为真的概率 0-1 |
| Score | 背景 + 量规 | 等级分布 + 期望分值 |

## 副作用

无网络访问（全部采样在当前会话内完成）；运行插件 `scripts/` 下两个 Python 脚本（仅标准库）做聚合与校准；仅当你显式运行校准时会在插件内写 `calibration.json`。无 hooks、无 MCP server、不收集凭据。

## 许可

MIT —— 见 [LICENSE](./LICENSE)。
