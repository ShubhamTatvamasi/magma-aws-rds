# magma-aws-rds

connect to mysql:
```bash
kubectl run backup-mysql --rm -it --command \
  --image=shubhamtatvamasi/mysql -- sh -c \
  "mysql --user=magma --password=wllctel2007 --database=magma \
  --host=nmsdb.c39jlnqmtsml.us-west-2.rds.amazonaws.com"
```

connect to postgres:
```bash
kubectl run backup-psql --rm -it --command \
  --env=PGPASSWORD=wllctel2007 \
  --image=shubhamtatvamasi/psql -- sh -c \
  "psql --username=orc8r --dbname=orc8r \
  --host=orc8rdb.c39jlnqmtsml.us-west-2.rds.amazonaws.com"
```

