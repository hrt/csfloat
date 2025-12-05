---
title: Float Ranges
layout: default
parent: Reference
nav_order: 2
---

# Float Value Ranges

Float values determine the wear condition of CS2 skins.

## Wear Conditions

| Wear | Float Range | Abbreviation |
|:-----|:------------|:-------------|
| Factory New | 0.00 - 0.07 | FN |
| Minimal Wear | 0.07 - 0.15 | MW |
| Field-Tested | 0.15 - 0.38 | FT |
| Well-Worn | 0.38 - 0.45 | WW |
| Battle-Scarred | 0.45 - 1.00 | BS |

## Usage in API

### Listings Query

```
GET /listings?min_float=0.00&max_float=0.07
```

### Buy Order Expression

```json
{"field": "FloatValue", "operator": "<", "value": {"constant": "0.07"}}
```

{: .note }
Not all skins can have all wear conditions. Some have restricted float ranges.
