---
aliases: 
cssclasses: 
date-created: 2023-01-01
publish: false
tags:
  - atlas/core
---
 
## Random 30 Notes Box
```dataviewjs
const numberToShow = 4;
const notes =
dv.pages('"30 Notes"' )
    .filter(note => !note.file.path.startsWith("30 Notes/31 Medicine"))
.sort(() => 0.5 - Math.random())
.slice (0, numberToShow)
.map (note => note.file.link);
dv.list(notes);
```

## Random Work box 
```dataviewjs
const numberToShow = 5;
const notes = dv.pages('"30 Notes/31 Medicine"')
.sort (() => 0.5 - Math.random())
.filter (note => !note.file.tags.includes(""))
.slice (0, numberToShow)
.map (note => note.file.link);
dv.list(notes);
```
