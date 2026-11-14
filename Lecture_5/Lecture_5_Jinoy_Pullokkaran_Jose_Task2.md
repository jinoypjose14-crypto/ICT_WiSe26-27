# Lecture 5 – Task 2: Search and Filter

## Task 2.1 – Filter processes by username

Command:
```bash
ps aux | grep '^jinoy-p+'
```
Output:
```text
jinoy-p+ 1436  0.0  0.1  22204 12916 ?  Ss  13:44  0:00 /usr/lib/systemd/systemd --user
jinoy-p+ 1441  0.0  0.0  23016  4096 ?  S   13:44  0:00 (sd-pam)
jinoy-p+ 1461  0.0  0.0   8856  5856 tty1 Ss+ 13:44 0:00 -bash
jinoy-p+ 1547  2.4  0.0  18564  7688 ?  S   13:46  0:04 sshd-session
jinoy-p+ 1548  0.1  0.0   8844  5872 pts/0 Ss 13:46 0:04 -bash
jinoy-p+ 2027  114  0.0  9764  4692 pts/0 R+ 14:27 0:00 ps aux
jinoy-p+ 2028  71.4  0.0  6716   204 pts/0 S+ 14:27 0:00 grep --color=auto ^jinoy-p+
jinoy-p+ 2029  83.3  0.0 11508   204 pts/0 R+ 14:27 0:00 tee Task2_1_output.txt
```
## Task 2.2 – Avoid false positives

Command:
```bash
ps aux | grep '^jinoy-p+[[:space:]]'
```
Output:
```text
jinoy-p+    1436  0.0  0.1  22204 12916 ?        Ss   13:44   0:00 /usr/lib/systemd/systemd --user
jinoy-p+    1441  0.0  0.0  23016  4096 ?        S    13:44   0:00 (sd-pam)
jinoy-p+    1461  0.0  0.0   8856  5856 tty1     Ss+  13:44   0:00 -bash
jinoy-p+    1547  2.4  0.0  18564  7688 ?        S    13:46   1:02 sshd-session: jinoy-pullokkaran-jose@pts/0
jinoy-p+    1548  0.1  0.0   8844  5872 pts/0    Ss   13:46   0:04 -bash
jinoy-p+    2041 75.3  0.0   9764  4684 pts/0    R+   14:29   0:00 ps aux
jinoy-p+    2042 20.5  0.0   6848  2692 pts/0    S+   14:29   0:00 grep --color=auto ^jinoy-p+[[:space:]]
jinoy-p+    2043 36.1  0.0  16112  7244 pts/0    S+   14:29   0:00 tee Task2_2_output.txt
```
## Task 2.3 – Exclude root processes

Command:
```bash
ps aux | grep -v '^root'
```
Output:
```text
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
systemd+     565  0.0  0.1  22752 14704 ?        Ss   13:43   0:00 /usr/lib/systemd/systemd-resolved
systemd+     977  0.0  0.1  21436 12324 ?        Ss   13:43   0:00 /usr/lib/systemd/systemd-networkd
message+    1026  0.0  0.0   9016  5680 ?        Ss   13:43   0:02 @dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
polkitd     1048  0.0  0.0 306448  8508 ?        Ssl  13:43   0:00 /usr/lib/polkit-1/polkitd --no-debug --log-level=notice
syslog      1121  0.0  0.0 220548  6228 ?        Ssl  13:43   0:00 /usr/sbin/rsyslogd -n -iNONE
_chrony     1146  0.0  0.0  20556  6424 ?        S    13:43   0:01 /usr/sbin/chronyd -n -F 1
_chrony     1157  0.0  0.0  12096  2464 ?        S    13:43   0:00 /usr/sbin/chronyd -n -F 1
jinoy-p+    1436  0.0  0.1  22204 12916 ?        Ss   13:44   0:00 /usr/lib/systemd/systemd --user
jinoy-p+    1441  0.0  0.0  23016  4096 ?        S    13:44   0:00 (sd-pam)
jinoy-p+    1461  0.0  0.0   8856  5856 tty1     Ss+  13:44   0:00 -bash
jinoy-p+    1547  2.3  0.0  18564  7688 ?        S    13:46   1:02 sshd-session: jinoy-pullokkaran-jose@pts/0
jinoy-p+    1548  0.1  0.0   8844  5872 pts/0    Ss   13:46   0:04 -bash
jinoy-p+    2059  140  0.0   9764  4696 pts/0    R+   14:30   0:00 ps aux
jinoy-p+    2060  152  0.0    672   244 pts/0    R+   14:30   0:00 grep --color=auto -v ^root
jinoy-p+    2061  152  0.0  16112  7628 pts/0    S+   14:30   0:00 tee Task2_3_output.txt
```
## Task 2.4 – Exclude kworker and irq processes

Command:
```bash
ps aux | grep -v -E 'kworker|irq' > Task2_output.txt
```
Output:
```text
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.1  0.1  25940 16488 ?        Ss   13:43   0:05 /usr/lib/systemd/systemd --switched-root --system --deserialize=50
root           2  0.0  0.0      0     0 ?        S    13:43   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        S    13:43   0:00 [pool_workqueue_release]
root          15  0.1  0.0      0     0 ?        I    13:43   0:03 [rcu_preempt]
root          16  0.0  0.0      0     0 ?        S    13:43   0:00 [rcu_exp_par_gp_kthread_worker/0]
root          17  0.0  0.0      0     0 ?        S    13:43   0:00 [rcu_exp_gp_kthread_worker]
root          18  0.0  0.0      0     0 ?        S    13:43   0:00 [migration/0]
root          19  0.0  0.0      0     0 ?        S    13:43   0:00 [kprobe-optimizer]
root          20  0.0  0.0      0     0 ?        S    13:43   0:00 [idle_inject/0]
root          21  0.0  0.0      0     0 ?        S    13:43   0:00 [cpuhp/0]
root          22  0.0  0.0      0     0 ?        S    13:43   0:00 [cpuhp/1]
root          23  0.0  0.0      0     0 ?        S    13:43   0:00 [idle_inject/1]
root          24  0.0  0.0      0     0 ?        S    13:43   0:00 [migration/1]
root          28  0.0  0.0      0     0 ?        S    13:43   0:00 [cpuhp/2]
root          29  0.0  0.0      0     0 ?        S    13:43   0:00 [idle_inject/2]
root          30  0.0  0.0      0     0 ?        S    13:43   0:00 [migration/2]
root          34  0.0  0.0      0     0 ?        S    13:43   0:00 [cpuhp/3]
root          35  0.0  0.0      0     0 ?        S    13:43   0:00 [idle_inject/3]
root          36  0.0  0.0      0     0 ?        S    13:43   0:00 [migration/3]
root          40  0.0  0.0      0     0 ?        S    13:43   0:00 [cpuhp/4]
root          41  0.0  0.0      0     0 ?        S    13:43   0:00 [idle_inject/4]
root          42  0.0  0.0      0     0 ?        S    13:43   0:00 [migration/4]
root          46  0.0  0.0      0     0 ?        S    13:43   0:00 [cpuhp/5]
root          47  0.0  0.0      0     0 ?        S    13:43   0:00 [idle_inject/5]
root          48  0.0  0.0      0     0 ?        S    13:43   0:00 [migration/5]
root          58  0.0  0.0      0     0 ?        S    13:43   0:00 [kdevtmpfs]
root          60  0.0  0.0      0     0 ?        I    13:43   0:00 [rcu_tasks_kthread]
root          61  0.0  0.0      0     0 ?        I    13:43   0:00 [rcu_tasks_rude_kthread]
root          62  0.0  0.0      0     0 ?        S    13:43   0:00 [kauditd]
root          63  0.0  0.0      0     0 ?        S    13:43   0:00 [khungtaskd]
root          64  0.0  0.0      0     0 ?        S    13:43   0:00 [oom_reaper]
root          68  0.0  0.0      0     0 ?        S    13:43   0:02 [kcompactd0]
root          69  0.0  0.0      0     0 ?        SN   13:43   0:00 [ksmd]
root          70  0.0  0.0      0     0 ?        SN   13:43   0:00 [khugepaged]
root          82  0.0  0.0      0     0 ?        S    13:43   0:00 [watchdogd]
root          85  0.0  0.0      0     0 ?        S    13:43   0:00 [kswapd0]
root          87  0.0  0.0      0     0 ?        S    13:43   0:00 [ecryptfs-kthread]
root          93  0.0  0.0      0     0 ?        S    13:43   0:00 [scsi_eh_0]
root          95  0.0  0.0      0     0 ?        S    13:43   0:00 [scsi_eh_1]
root         360  0.0  0.0      0     0 ?        S    13:43   0:00 [scsi_eh_2]
root         401  0.0  0.0      0     0 ?        S    13:43   0:00 [jbd2/sda2-8]
root         498  0.0  0.0      0     0 ?        S    13:43   0:00 [psimon]
root         505  0.0  0.1  50528 17124 ?        S<s  13:43   0:02 /usr/lib/systemd/systemd-journald
root         548  0.2  0.1 345028  9776 ?        SLsl 13:43   0:08 /usr/sbin/multipathd -d -s
systemd+     565  0.0  0.1  22752 14704 ?        Ss   13:43   0:00 /usr/lib/systemd/systemd-resolved
root         569  0.0  0.1  40404 14648 ?        Ss   13:43   0:00 /usr/lib/systemd/systemd-udevd
root         574  0.0  0.0      0     0 ?        S    13:43   0:00 [psimon]
systemd+     977  0.0  0.1  21436 12324 ?        Ss   13:43   0:00 /usr/lib/systemd/systemd-networkd
root        1018  0.0  0.0   2888  2012 ?        Ss   13:43   0:00 /bin/sh /usr/lib/systemd/scripts/chronyd-starter.sh -n -F 1
message+    1026  0.0  0.0   9016  5680 ?        Ss   13:43   0:02 @dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
root        1043  0.0  0.3  46744 30168 ?        Ss   13:43   0:01 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
polkitd     1048  0.0  0.0 306448  8508 ?        Ssl  13:43   0:00 /usr/lib/polkit-1/polkitd --no-debug --log-level=notice
root        1053  0.2  0.4 2108324 43860 ?       Ssl  13:43   0:06 /usr/lib/snapd/snapd
root        1060  0.0  0.1  18556  9668 ?        Ss   13:43   0:00 /usr/lib/systemd/systemd-logind
root        1062  0.0  0.1 543364 15128 ?        Ssl  13:43   0:01 /usr/libexec/udisks2/udisksd
syslog      1121  0.0  0.0 220548  6228 ?        Ssl  13:43   0:00 /usr/sbin/rsyslogd -n -iNONE
_chrony     1146  0.0  0.0  20556  6424 ?        S    13:43   0:01 /usr/sbin/chronyd -n -F 1
_chrony     1157  0.0  0.0  12096  2464 ?        S    13:43   0:00 /usr/sbin/chronyd -n -F 1
root        1188  0.0  0.1 391608 14268 ?        Ssl  13:43   0:00 /usr/sbin/ModemManager
root        1266  0.0  0.3 126116 33076 ?        Ssl  13:43   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
root        1271  0.0  0.0  10744  7824 ?        Ss   13:43   0:00 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
root        1290  0.0  0.0   7060  3344 ?        Ss   13:43   0:00 /usr/sbin/cron -f -P
root        1303  0.0  0.0   8760  5616 ?        Ss   13:43   0:00 login -- jinoy-pullokkaran-jose
jinoy-p+    1436  0.0  0.1  22204 12916 ?        Ss   13:44   0:00 /usr/lib/systemd/systemd --user
jinoy-p+    1441  0.0  0.0  23016  4096 ?        S    13:44   0:00 (sd-pam)
jinoy-p+    1461  0.0  0.0   8856  5856 tty1     Ss+  13:44   0:00 -bash
root        1492  0.0  0.1  18428 12272 ?        Ss   13:45   0:00 sshd-session: jinoy-pullokkaran-jose [priv]
jinoy-p+    1547  2.3  0.0  18564  7688 ?        S    13:46   1:03 sshd-session: jinoy-pullokkaran-jose@pts/0
jinoy-p+    1548  0.1  0.0   8844  5872 pts/0    Ss   13:46   0:04 -bash
root        1886  2.3  0.5 501544 47948 ?        Ssl  14:12   0:26 /usr/libexec/fwupd/fwupd
root        1897  0.4  0.1 318704 11492 ?        Ssl  14:12   0:04 /usr/libexec/upowerd
jinoy-p+    2073  200  0.0   9764  4684 pts/0    R+   14:31   0:00 ps aux
```
