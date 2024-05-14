# nada datastream test

For oss i nada så vi skal ha en fungerende datastream kjørende.

Kjørt følgende i databasen autentisert som appens bruker:

```sql
CREATE TABLE dummy (col1 text, col2 text);
INSERT INTO dummy (col1,col2) VALUES ('asdf','asdf2');
INSERT INTO dummy (col1,col2) VALUES ('asdf123213123','asdf22124231');

ALTER DEFAULT PRIVILEGES IN SCHEMA PUBLIC GRANT SELECT ON TABLES TO "datastream-extra";
GRANT SELECT ON ALL TABLES IN SCHEMA PUBLIC TO "datastream-extra";

ALTER USER "datastream" WITH REPLICATION;
ALTER USER "datastream-extra" WITH REPLICATION;
CREATE PUBLICATION "ds_publication" FOR ALL TABLES;
SELECT PG_CREATE_LOGICAL_REPLICATION_SLOT('ds_replication', 'pgoutput');
```
