# 0826-pmset

This set up the wakeup and sleep in macos

```bash
# check schedule
pmset -g sched
# setup wakeup and sleep
sudo pmset repeat wakeorpoweron MTWRFSU 09:00:00 sleep MTWRFSU 18:00:00
```
