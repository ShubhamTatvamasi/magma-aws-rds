# restore-rds

connect to the backup-rds pod:
```bash
kubectl exec -it backup-rds -- sh
mysql --user=magma --password=wllctel2007 --database=magma \
  --host=nmsdb.c39jlnqmtsml.us-west-2.rds.amazonaws.com
```

drop and create new magma database:
```mysql
DROP DATABASE magma;
CREATE DATABASE magma;
```

copy file to the container:
```bash
kubectl cp nmsdb-test.sql /tmp/nmsdb-test.sql
```

restore nms database:
```bash
mysql --user=magma --password=wllctel2007 \
  --host=nmsdb.c39jlnqmtsml.us-west-2.rds.amazonaws.com \
  magma < /tmp/nmsdb-test.sql
```
