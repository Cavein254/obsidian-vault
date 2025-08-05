In **Bash**, the `bg` command is used to **resume a suspended job in the background**.

```bash
jobs
```
The above will create all jobs in the system
```bash
sleep 100 &
```
This will create a job. The `&` will send the job into the background. You can use the `jobs` command to show all the jobs that are running
```bash
sleep 100 &
jobs       
[1]  + running    sleep 100
```
This process can be killed using:
```bash
kill %1
```