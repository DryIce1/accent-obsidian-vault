<%"---"%>
last-month: 
- "[[<% tp.date.now("YYYY-MM", -15, tp.file.title, "YYYY-MM") %>]]"
quarter: 
  - "[[<% tp.date.now("YYYY-[Q]Q", +0, tp.file.title, "YYYY-MM") %>]]"
year: 
  - "[[<% tp.date.now("YYYY", +0, tp.file.title, "YYYY-MM") %>]]"
weeks:<%*
const monthMoment = moment(tp.file.title, "YYYY-MM");
const monthStart = monthMoment.clone().startOf('month');
const monthEnd = monthMoment.clone().endOf('month');
const currentMonth = monthMoment.month();

let weekStart = monthStart.clone().startOf('isoWeek');

while (weekStart.isBefore(monthEnd.clone().add(1, 'day'))) {
if (weekStart.clone().add(3, 'days').isBetween(monthStart, monthEnd, null, '[]')) {
    tR += `\n- "[[${weekStart.format("gggg-[W]WW")}]]"`;
  }
  weekStart.add(1, 'week');
}
%>
date-created: <% tp.date.now("YYYY-MM-DD", +0, tp.file.title, "YYYY-MM") %>
aliases: <% tp.date.now("MMMM YYYY", +0, tp.file.title, "YYYY-MM") %>
tags: log/month
type: log/month
cssClasses:
  - log
publish: false
banner: 
banner-y: 
cover: 
banner-description: 
<%"---"%>

```meta-bind-embed
[[Periodic notes monthly note - meta bind embed]]
```

# Log