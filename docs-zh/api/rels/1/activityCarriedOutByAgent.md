---
title: "activityCarriedOutByAgent"
---

## 定义

此关系将活动与执行该活动的行动者（个人或群体）连接起来。

## 使用说明

* **源类**：Activity
* **目标类**：Agent（Person 或 Group）
* **属性名**：carried_out_by

## 示例

艺术家创作艺术品的活动会被此关系连接到艺术家个人。

```json
{
  "type": "Creation",
  "carried_out_by": [
    {
      "type": "Person",
      "_label": "艺术家姓名"
    }
  ]
}
```