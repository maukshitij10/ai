# Q: at, batch, cron (including send mail every 5 minutes)

## at / batch  (one-time jobs)
```bash
dnf install at mailx -y
systemctl enable --now atd
at now + 2 minutes
at> echo "Hello from at" >> /tmp/at_out.txt
at> (press Ctrl+D)
at 10:30 PM                         # specific time
atq                                 # list pending jobs
at -c <jobid>                       # show job
atrm <jobid>                        # delete job

batch                               # runs when system load < 0.8
batch> date >> /tmp/batch_out.txt
batch> (Ctrl+D)
```
Allow/deny users: /etc/at.allow, /etc/at.deny.

## cron (recurring jobs)
```bash
systemctl enable --now crond
crontab -e                          # edit your crontab
crontab -l                          # list
crontab -r                          # remove all
```
Format: `minute hour day-of-month month day-of-week command`

Send mail to a user every 5 minutes:
```
*/5 * * * * echo "Reminder mail" | mail -s "Cron Test" student1
```
(needs `dnf install mailx postfix -y ; systemctl enable --now postfix`)
Check mail: `su - student1` -> `mail`.  Check cron log: `tail /var/log/cron`.

Other examples:
```
0 2 * * * /root/backup.sh        # daily at 2 AM
30 18 * * 1-5 command            # weekdays 6:30 PM
@reboot command
```
System cron: /etc/crontab, /etc/cron.d/, cron.daily/.
