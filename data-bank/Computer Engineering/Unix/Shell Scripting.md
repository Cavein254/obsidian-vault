In **Bash**, the `bg` command is used to **resume a suspended job in the background**.

```bash
jobs
```
The above will create all jobs in the system
```bash
sleep 100 &
```
This will create a job. The `&` will send the job into the background. You can use the `jobs` command to show all the jobs that are running