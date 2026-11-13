# 26 Linux Interview Questions

The questions are grouped by topic, with the same wording and numbering as your list.

---

## Part 1: Linux Command-Line Operations (Q1 to Q10)

**Q1. Watching a live log and filtering it**
> How do you watch the last 50 lines of a live log file in real time, while showing only the lines that contain `ERROR`?

**Q2. Finding recent files**
> Which command finds all `.log` files inside `/var/log` that were modified in the last 7 days?

**Q3. Disk space troubleshooting**
> A server has run out of disk space. How do `df -h` and `du -sh` work together to help you find the root cause?

**Q4. Port conflict**
> A web server will not start because port `80` is already in use. How do you find the exact process that is holding that port?

**Q5. Archiving and compression**
> What is the difference between `tar -cvf` and `tar -czvf`? How do you extract a `.tar.gz` file into a specific folder?

**Q6. Searching inside files**
> How do you search for the text `"connection refused"` (ignoring capital or small letters) in all files inside `/etc/nginx/`?

**Q7. `awk` vs `cut`**
> Why is `awk '{print $1}'` often better than `cut -d' ' -f1` when the output has uneven spaces?

**Q8. Replacing text in a file**
> How do you use `sed` to replace every `dev-db` with `prod-db` directly inside a configuration file?

**Q9. Symbolic link vs hard link**
> What happens to a symbolic link and to a hard link if the original file is deleted?

**Q10. Checking a remote port**
> How do you check whether a remote database port (for example `10.0.1.5:3306`) is reachable from the terminal, without using `ping`?

---

## Part 2: File Permissions and Ownership (Q11 to Q16)

**Q11. Permissions to numbers**
> Convert `-rwxr-x---` into octal (numeric) form. What can the owner, the group and others do?

**Q12. Changing owner and group together**
> Which single command changes the owner to `appuser` and the group to `appgroup` for a folder and everything inside it?

**Q13. Understanding `umask`**
> If the `umask` is `0022`, what permissions does a new file get, and what does a new folder get?

**Q14. The sticky bit**
> Why is the sticky bit set on `/tmp`? What problem can happen if it is removed from a shared folder?

**Q15. ACL with `setfacl`**
> When normal `rwx` permissions are not enough, how do you give one extra user read and write access to a file without changing its group?

**Q16. Making a file unchangeable**
> How do you lock an important configuration file so that even `root` cannot edit or delete it?

---

## Part 3: Processes and Systemd Services (Q17 to Q24)

**Q17. Finding heavy processes**
> How do you check, in a live view, which processes are using the most CPU and RAM?

**Q18. `kill -15` vs `kill -9`**
> When stopping a stuck process, why should you try `kill -15` (SIGTERM) before `kill -9` (SIGKILL)?

**Q19. `start`, `enable` and `reload`**
> What is the difference between `systemctl start`, `systemctl enable` and `systemctl reload`?

**Q20. A service fails to start**
> `systemctl start myapp` fails. Which two commands do you run next to find the reason?

**Q21. Keeping a job running after logout**
> How do you start a long-running script so that it keeps running even after your SSH connection drops?

**Q22. Zombie processes**
> What is a zombie process (state `Z`)? Why does `kill -9` not remove it, and how is it actually cleared?

**Q23. Logs of one service**
> How do you view the `journalctl` logs of only the `sshd` service since the last boot?

**Q24. Lowering a job's priority**
> How do you run a heavy backup script with low CPU priority, so it does not slow down live production traffic?

---

## Part 4: Basic Shell and Python Scripting (Q25 to Q30)

**Q25. Exit status**
> Inside a Bash script, how do you check whether the previous command succeeded or failed?

**Q26. Service health check**
> Write a small Bash `if-else` that checks whether `nginx` is running and prints either "Healthy" or "Down".

---
