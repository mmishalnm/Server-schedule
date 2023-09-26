# Server schedule

Automate System restart



## 1. Create Power-Off Script:

Create a shell script to power off your system. Let's call it `poweroff.sh`:

```bash
#!/bin/bash
sudo shutdown -h now
```
Save the script and make it executable by running:

```bash
chmod +x poweroff.sh
```
## 2. Create Power-on Script:

Create another shell script to power on your system. Let's call it `poweron.sh`:

```bash
#!/bin/bash
sudo rtcwake -m mem -s 30
```
In this script, we use rtcwake to wake up the system from a low-power state after 30 seconds. You can adjust the -s parameter to specify the delay before wake-up.

Save the script and make it executable:

```bash
chmod +x poweron.sh
```

## 3.Schedule Power-Off:
You can use `cron` to schedule the `power-off` script to run at a specific time. Open your crontab configuration:

```bash
crontab -e
```

Add a line to schedule the power-off script (replace ``HH:MM`` with the desired time):
```bash
HH MM * * * /path/to/poweroff.sh
```
Save and exit the crontab editor.

## 4.Schedule Power-On:

To schedule the power-on script, you can use the `at` command, which is suitable for one-time scheduling:
```bash
echo "sudo /path/to/poweron.sh" | at HH:MM tomorrow
```

This command schedules the power-on script to run at a specific time tomorrow. Replace `HH:MM` with the desired time.

Note that for `at` to work, the `atd` service should be installed and running. You can install it if it's not already installed:

```bash
sudo apt-get install at
```
Also, ensure that you set the system time correctly and account for time zones.

These scripts and scheduling methods will allow you to automatically power off and power on your Ubuntu system at specified times. Just make sure to replace `/path/to/poweroff.sh` and `/path/to/poweron.sh` with the actual paths to your scripts.
