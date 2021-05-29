# backup-rds

start backup-rds server:
```bash
kubectl run backup-rds --image=shubhamtatvamasi/backup-rds
```

backup nms and orc8r:
```bash
kubectl exec -it backup-rds -- sh -c "echo && \
  mysqldump --user=magma --password=wllctel2007 \
    --host=nmsdb.c39jlnqmtsml.us-west-2.rds.amazonaws.com \
    magma > nmsdb-test.sql && \
  PGPASSWORD=wllctel2007 pg_dump --username=orc8r \
    --host=orc8rdb.c39jlnqmtsml.us-west-2.rds.amazonaws.com \
    orc8r > orc8rdb-test.sql"
```

port-forward pod:
```bash
kubectl port-forward backup-rds 8080:80
```

Download backup files: http://localhost:8080/