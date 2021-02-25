---
layout: post
title:      "Preventing Duplicates in a MySQL Database"
date:       2020-11-10 09:49:48 +0000
---

I found that I was doing pretty good in my technical assessment until I got to the part that said not to let a duplicate be saved into the database. This turned into a search of what kind of statement can I use within my ‘create’ function that will check for the record in the table first.
What I have found since then is there are a few ways to do this.

Using a REPLACE INTO ‘table’ SQL statement will replace the information in the record with the new information you’re trying to insert similar to doing an update except it does a DELETE then an INSERT.

```
REPLACE INTO `table`
SET `unique_id` = '0000003',
`name` = ‘Bob’;
```

Using an INSERT IGNORE INTO ‘table’ will check for the presence of the record matching the information and skip or ignore the command if it is there. If not, it will insert it into the database.

```
INSERT IGNORE INTO `table`
SET `unique_id` = '0000003',
`name` = ‘Bob’;
```

Using an INSERT INTO  ‘table’  ON DUPLICATE KEY UPDATE will check for the presence of the record matching the information and skip or ignore the command if it is there.

```
INSERT IGNORE INTO `table`
ON DUPLICATE KEY UPDATE `unique_id`;
UPDATE table SET `name` = ‘Bob’ WHERE  ‘unique_id’ = '0000003';
```
