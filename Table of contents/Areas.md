```dataview
table
from "Resources"
group by areas
flatten areas
where areas != " "
```