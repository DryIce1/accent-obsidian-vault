---
type:
  - datascope
description: See world-events-today referenced from the daily notes
---

```meta-bind-embed
[[Shortcuts widget - meta bind]]
```
```dataview
TABLE world-events-today as "World Events Today" 
FROM -"00 Meta"
WHERE world-events-today != null
SORT file.day desc
SORT file.day desc
```