```dataview
TABLE
tags as "Tags",
areas as "Areas",
file.mtime as "Last Modified",
file.starred as "Bookmarked",
archived as "Archived"
FROM "Resources"
flatten areas as "Areas"
```