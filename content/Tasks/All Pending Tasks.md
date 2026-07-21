```dataview
TASK FROM "/"
AND !"Attachments"
WHERE !completed
GROUP BY file.name
```
