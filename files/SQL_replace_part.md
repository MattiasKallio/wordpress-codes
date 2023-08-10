# Replace part of text in postmeta
I just need to remember this SQL query to replace part of a text in a postmeta field. The "where" key is important, otherwise you will replace all the text in all the postmeta fields.

### Replace part of text and add quotes around it

```sql

UPDATE wprj_postmeta SET meta_value = REPLACE(meta_value, CONCAT(SUBSTRING_INDEX(SUBSTRING_INDEX(meta_value, 'Startword ', -1), ' endword or phrase', 1)), CONCAT('"', SUBSTRING_INDEX(SUBSTRING_INDEX(meta_value, 'Startword ', -1), ' endword or phrase', 1), '"') ) WHERE meta_key = "usethekey";

```