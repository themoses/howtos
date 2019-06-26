# Yum is frozen and wont react

There are a couple of reasons why this happens but I always managed to get it back to work with the following steps:

1. Send the process to the background by hitting `CTRL + Z`
2. Identify the process id with `ps aux | grep yum`
3. Kill the yum process with `kill -9 PROCESS_ID`
4. Run the following commands or put them together in a script:

```
rm -f /var/lib/rpm/__*
rm -f /var/run/yum.pid
rm -f /var/lib/rpm/__db*
rm -f /var/lib/rpm/.rpm.lock
rm -f /var/lib/rpm/.dbenv.lock
rpm --rebuilddb
yum clean all
```

5. Run `yum update` again
