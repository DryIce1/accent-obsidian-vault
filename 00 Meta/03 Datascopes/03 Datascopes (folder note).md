---
aliases: 
banner: https://i.pinimg.com/originals/4a/73/18/4a73186742620ddc29db89c955f14e09.jpg
banner-y: 65
cssclasses:
  - dvl-c
date-created: 2023-02-18
publish: true
type:
  - datascope
---

```dataview
TABLE
("![|150](" + banner +")") as Banner, 
"<i>" + description + "</i>" AS "Description"
WHERE file.folder = this.file.folder
WHERE file.name != this.file.name
SORT file.mtime DESC
```
