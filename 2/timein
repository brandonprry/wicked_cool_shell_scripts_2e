#!/bin/bash

# timein--Shows the current time in the specified time zone or 
#   geographic zone. Without any argument, this shows UTC/GMT. Use
#   the word "list" to see a list of known geographic regions.
#   Note that it's possible to match zone directories (regions),
#   but that only time zone files (cities) are valid specifications.

#   Time zone database ref: http://www.twinsun.com/tz/tz-link.htm

zonedir="/usr/share/zoneinfo"

if [ ! -d $zonedir ] ; then
  echo "No time zone database at $zonedir." >&2 ; exit 1
fi

if [ -d "$zonedir/posix" ] ; then
  zonedir=$zonedir/posix        # modern Linux systems
fi

if [ $# -eq 0 ] ; then
  timezone="UTC"
  mixedzone="UTC"
elif [ "$1" = "list" ] ; then
  ( echo "All known time zones and regions defined on this system:"
    cd $zonedir
    find -L * -type f -print | xargs -n 2 | \
      awk '{ printf "  %-38s %-38s\n", $1, $2 }' 
  ) | more
  exit 0
else

  region="$(dirname $1)"
  zone="$(basename $1)"

  # Is the given time zone a direct match? If so, we're good to go. 
  #   Otherwise we need to dig around a bit to find things. Start by 
  #   just counting matches.

  matchcnt="$(find -L $zonedir -name $zone -type f -print |
        wc -l | sed 's/[^[:digit:]]//g' )"

  # Check if at least one file matches
  if [ "$matchcnt" -gt 0 ] ; then
    # But exit if more than one file matches
    if [ $matchcnt -gt 1 ] ; then
      echo "\"$zone\" matches more than one possible time zone record." >&2
      echo "Please use 'list' to see all known regions and time zones" >&2
      exit 1
    fi
    match="$(find -L $zonedir -name $zone -type f -print)"
    mixedzone="$zone" 
  else # maybe we can find a matching time zone region, rather than a specific time zone
    # First letter capitalized, rest of word lowercase for region + zone
    mixedregion="$(echo ${region%${region#?}} \
                 | tr '[[:lower:]]' '[[:upper:]]')\
                 $(echo ${region#?} | tr '[[:upper:]]' '[[:lower:]]')"
    mixedzone="$(echo ${zone%${zone#?}} | tr '[[:lower:]]' '[[:upper:]]') \
               $(echo ${zone#?} | tr '[[:upper:]]' '[[:lower:]]')"
    
    if [ "$mixedregion" != "." ] ; then
      # Only look for specified zone in specified region
      # to let users specify unique matches when there's more than one
      # possibility (e.g., "Atlantic")
      match="$(find -L $zonedir/$mixedregion -type f -name $mixedzone -print)"
    else
      match="$(find -L $zonedir -name $mixedzone -type f -print)"
    fi

    # If file exactly matched the specified pattern
    if [ -z "$match"  ] ; then
      # Check if the pattern was too ambiguous
      if [ ! -z $(find -L $zonedir -name $mixedzone -type d -print) ] ; then
         echo "The region \"$1\" has more than one time zone. " >&2
      else  # Or if it just didn't produce any matches at all
        echo "Can't find an exact match for \"$1\". " >&2
      fi
      echo "Please use 'list' to see all known regions and time zones." >&2
      exit 1
    fi
  fi
  timezone="$match"
fi

nicetz=$(echo $timezone | sed "s|$zonedir/||g")    # pretty up the output

echo It\'s $(TZ=$timezone date '+%A, %B %e, %Y, at %l:%M %p') in $nicetz

exit 0
