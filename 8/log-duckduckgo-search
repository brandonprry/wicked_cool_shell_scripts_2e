#!/bin/bash

# log-duckduckgo-search--Given a search request, logs the pattern and then
#   feeds the entire sequence to the real DuckDuckGo search system.

# Make sure the directory path and file listed as logfile are writable by
#  the user the web server is running as.
logfile="/var/www/wicked/scripts/searchlog.txt"

if [ ! -f $logfile ] ; then
  touch $logfile
  chmod a+rw $logfile
fi

if [ -w $logfile ] ; then
  echo "$(date): $QUERY_STRING" | sed 's/q=//g;s/+/ /g' >> $logfile
fi

echo "Location: https://duckduckgo.com/html/?$QUERY_STRING"
echo ""

exit 0
