```bash
docker compose up --force-recreate
```

## Check the process running on specific port number

```bash
sudo lsof -i :3000
```

## Kill a process running on specific port number

```bash
sudo fuser -k 3000/tcp # or
sudo kill -9 1234 # where 1234 is the PID
```