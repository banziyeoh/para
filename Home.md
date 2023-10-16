```dataview
Table
rows.file.link as "Title"
From "3. Resources"
GROUP BY dateformat(file.ctime, "yyyy-MM") AS DATE SORT DATE DESC


```