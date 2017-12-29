# linux

Useful commands and tools for working with linux.

## Checking a port

```
lsof -i -P -n
lsof -i -P -n | grep LISTEN
lsof -i -P -n | grep 27017

# lsof: list open files
# -i: internet, i.e. IP
# -n: network names
# -P: port numbers
```

## Forward a Port to a Remote Server

```
ssh -f user@personal-server.com -L 2000:personal-server.com:25 -N
```


