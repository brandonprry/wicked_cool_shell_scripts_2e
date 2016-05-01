#!/bin/bash

# docron--Runs the daily, weekly, and monthly system cron jobs on a 
#   system that's likely to be shut down during the usual time of day when
#   the system cron jobs would otherwise be scheduled to run.

rootcron="/etc/crontab"   # This is going to vary significantly based on
                          # which version of Unix or Linux you've got.

if [ $# -ne 1 ] ; then
  echo "Usage: $0 [daily|weekly|monthly]" >&2
  exit 1
fi

# If this script isn't being run by the administrator, fail out. In 
#   earlier scripts, you saw USER and LOGNAME being tested, but in this
#   situation, we'll check the user ID value directly. Root = 0.

if [ "$(id -u)" -ne 0 ] ; then
   # Or you can use $(whoami) != "root" here, as needed.
  echo "$0: Command must be run as 'root'" >&2
  exit 1
fi

# We assume that the root cron has entries for 'daily', 'weekly', and 
#   'monthly' jobs. If we can't find a match for the one specified, well,
#   that's an error. But first, we'll try to get the command if there is 
#   a match (which is what we expect).

job="$(awk "NF > 6 && /$1/ { for (i=7;i<=NF;i++) print \$i }" $rootcron)"

if [ -z "$job" ] ; then   # No job? Weird. Okay, that's an error.
  echo "$0: Error: no $1 job found in $rootcron" >&2
  exit 1
fi

SHELL='which sh'          # To be consistent with cron's default

eval $job               # We’ll exit once the job is finished.
