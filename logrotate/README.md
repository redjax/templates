# Logrotate

Templates for a Linux [logrotate policy](https://linux.die.net/man/8/logrotate). You can read more about setting up logrotate in [this RedHat blog entry](https://www.redhat.com/en/blog/setting-logrotate).

## Usage

Sometimes when running a script or cron job, you might output logs by appending this to the end of your command:

```bash
<command> > /var/log/path/to/logname.log 2>&1
```

This would save the output of the script (what you would see if you ran the script directly in your terminal) to a file at `/var/log/path/to/logname.log`.

Over time this log file could get extremely large. It is not unheard of for a runaway logfile to eat up hundreds of gigabytes by mistake.

Logrotate sets rotation policies for logfiles at a given path. You create a new logrotate file for each log file you output. For this example, let's say you have a cron job that runs every 6 hours and creates a backup of your home directory. The job outputs its logs to `/var/log/home_backup/backup.log`. You want to rotate this file at 10MB, or every week (whichever occurs first), retaining 2 weeks worth of backups, and recreate the logfile once it's rotated.

You create logrotate policies in `/etc/logrotate.d/<logrotate_policy_name>`. The file can be named whatever you want, but it's advisable to make the name of the file descriptive of the log file it's rotating. You can omit a file extension from the file name.

Create a file at `/etc/logrotate.d/home_dir_backup`:

```plaintext
/var/log/home_backup.log {
    size 10M           # Rotate if log file reaches 10MB
    weekly             # Or rotate weekly, whichever happens first
    rotate 14          # Keep 14 rotated logs (2 weeks worth)
    compress           # Compress rotated logs with gzip
    delaycompress      # Delay compression until next rotation cycle
    missingok          # Don't issue error if log file is missing
    notifempty         # Skip rotation if log file is empty
    create 0640 root adm  # Recreate log file with correct permissions and ownership. You can also use $USER for the user and group
}

```

Now, if you schedule a cron job like this, the log file will automatically rotate:

```shell
0 */6 * * * cp -R /home/username /backup/homedir > /var/log/home_backup.log 2>&1  # this is the path you should use in the logrotate policy
```
