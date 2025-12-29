---
title: "objectProducedByAgent"
---

## 定义

此关系将对象（通常是艺术品）与其创作者连接起来。

## 使用说明

* **源类**：HumanMadeObject
* **目标类**：Agent（Person 或 Group）
* **属性名**：produced_by

## 示例

绘画作品通过此关系连接到创作它的艺术家。

```json
{
  "type": "HumanMadeObject",
  "produced_by": {
    "type": "Creation",
    "carried_out_by": [
      {
        "type": "Person",
        "_label": "艺术家姓名"
      }
    ]
  }
}
```