# pitpsql

```
mkdir backups
mkdir archives
```

init the db as
```
initdb data
```

and copy in all the conf files BUT recovery conf and


``` pg_ctl start -D data/```


wals are copied from pg_xlogs to /archives every rotation every 16MB

To create the first backup do 

```
pg_basebackup --xlog --format=t -D /backups/`date +%Y%m%d`
```

Remove the data folder --> /usr/local/psql/data for example and:

```
tar -xvf backups/20170710/base.tar -C data
```

and the wals will be read from archives, so that applies the backup plus all wals.

if you want to restore to a specifc point , use timestamps or
```
SELECT pg_create_restore_point( 'important_moment' );
```


and then in recovery.conf
```
recovery_target_name=important_moment
```

timestamps can be used as:
```
recovery_target_time='2014-12-01 10:19:42'
```
