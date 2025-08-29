## Check actual network name:
```bash
docker network ls
NETWORK ID     NAME                DRIVER    SCOPE
8d3d4c5c8e32   myproject_gitea     bridge    local
```
### Run Alpine container with correct network:
```
docker run -it --rm --network=myproject_gitea alpine sh
```
Where `myproject` is the name from the network
### Install git + curl inside:
```bash
apk add --no-cache git curl
git ls-remote http://gitea:3000/admin/django-boilerplate.git
```
If it produces error then their is an authentication issue