# restore-rds


copy backups to the container:
```bash
kubectl cp nmsdb-production.sql backup-rds:/rds/nmsdb-production.sql
kubectl cp orc8rdb-production.sql backup-rds:/rds/orc8rdb-production.sql
```
---

### mysql restore

connect to the backup-rds pod:
```bash
kubectl exec -it backup-rds -- sh
```

connect to mysql:
```bash
mysql --user=magma --password=wllctel2007 --database=magma \
  --host=nmsdb.c39jlnqmtsml.us-west-2.rds.amazonaws.com
```

drop and create new magma database:
```mysql
DROP DATABASE magma;
CREATE DATABASE magma;
```

restore nms database:
```bash
mysql --user=magma --password=wllctel2007 \
  --host=nmsdb.c39jlnqmtsml.us-west-2.rds.amazonaws.com \
  magma < /rds/nmsdb-test.sql
```

### restore postgresql

connect to postgres:
```bash
export PGPASSWORD=wllctel2007
psql --username=postgres --dbname=orc8r \
  --host=orc8rdb.c39jlnqmtsml.us-west-2.rds.amazonaws.com
```

rename database:
```
ALTER DATABASE orc8r CONNECTION LIMIT 0;
SELECT * FROM pg_stat_activity;
SELECT pid FROM pg_stat_activity WHERE usename = 'orc8r';

SELECT pg_terminate_backend(pid) FROM pg_stat_activity WHERE usename = 'orc8r' AND pg_backend_pid() != pid;

ALTER DATABASE orc8r RENAME TO orc8r_bak;
```

create database:
```
CREATE DATABASE orc8r WITH OWNER orc8r;
```

restore database:
```bash
psql --username=orc8r --dbname=orc8r \
  --host=orc8rdb.c39jlnqmtsml.us-west-2.rds.amazonaws.com \
  < orc8rdb-test.sql
```


