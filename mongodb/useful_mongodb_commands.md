# Useful MongoDB commands
## Calculate the size on disk of all your database (in bytes)

```
mongo --port port_number --quiet  --eval 'db.adminCommand("listDatabases").databases.sort(function(l, r) {return r.sizeOnDisk - l.sizeOnDisk}).forEach(function(d) {print(d.name + " - " + d.sizeOnDisk)});
```
