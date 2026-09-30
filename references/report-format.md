# 报告格式

## 结构化 JSON（可选输出，便于存档与回溯）

```ts
interface PullbackReport {
  date: string;          // YYYY-MM-DD
  title: string;
  riskLevel: "low" | "medium" | "high";
  summary: string;       // ≤500 字结论
  signals: Array<{
    name: string;        // 信号名，如「10Y 美债收益率」
    level: "red" | "amber" | "green";
    detail: string;      // 量化数据 + 一句话解读
    source: string;      // 数据来源
  }>;
  triggers: {
    escalate: string[];  // 升级触发线
    deescalate: string[];// 降级触发线
  };
  watchlist: Array<{ window: string; event: string; focus: string }>;  // 未来两周日历
  bodyMd: string;        // 完整 Markdown 正文
}
```

## Markdown 正文结构

1. **结论卡**：风险等级 + 一句话判断（预警还是确认）
2. **信号矩阵**：六项，每项灯色 + 量化数据 + 来源
3. **指数位置**：VOO/QQQM/标普距近期高点回撤、关键支撑
4. **触发线**：升级/降级条件（量化、可验证）
5. **观察清单**：未来两周财报与数据日历
6. **反向声音**：当前判断最可能错在哪（这个板块必须有，防止确认偏误）
7. **免责声明**：不构成投资建议，市场有风险

完整真实样例：[samples/research-2026-09-29.json](../samples/research-2026-09-29.json)（4 信号共振、等级「中」的一天）。

## 写作要求

- 金额、点位、概率必须带具体数字，杜绝「大幅」「明显」这类模糊词
- 中文的「共振信号」最多列 3 条，按重要性排
- 每条红灯信号必须能追溯到来源
