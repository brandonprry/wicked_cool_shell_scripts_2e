#!/bin/bash
# verifycron--Checks a crontab file to ensure that it's
#    formatted properly. Expects standard cron notation of
#       min hr dom mon dow CMD,    
#    where min is 0-59, hr is 0-23, dom is 1-31, mon is 1-12 (or names)
#    and dow is 0-7 (or names). Fields can be ranges (a-e) or lists
#    separated by commas (a,c,z) or an asterisk. Note that the step 
#    value notation of Vixie cron (e.g., 2-6/2) is not supported by 
#    this script in its current version.


validNum()
{
  # Return 0 if the number given is a valid integer and 1 if not. 
  # Specify both number and maxvalue as args to the function.
  num=$1   max=$2

  # Asterisk values in fields are rewritten as "X" for simplicity,
  #   so any number in the form "X" is de facto valid.

  if [ "$num" = "X" ] ; then
    return 0
  elif [ ! -z $(echo $num | sed 's/[[:digit:]]//g') ] ; then
    # Stripped out all the digits, and the remainder isn't empty? No good.
    return 1
  elif [ $num -gt $max ] ; then
    # Number is bigger than the maximum value allowed.
    return 1
  else
    return 0
  fi
}

validDay()
{
  # Return 0 if the value passed to this function is a valid day name, 
  #   1 otherwise.

  case $(echo $1 | tr '[:upper:]' '[:lower:]') in
    sun*|mon*|tue*|wed*|thu*|fri*|sat*) return 0 ;;
    X) return 0 ;;         # Special case--it's a rewritten "*"
    *) return 1
  esac
}

validMon()
{
  # This function returns 0 if given a valid month name, 1 otherwise.

   case $(echo $1 | tr '[:upper:]' '[:lower:]') in 
     jan*|feb*|mar*|apr*|may|jun*|jul*|aug*) return 0           ;;
     sep*|oct*|nov*|dec*)                    return 0           ;;
     X) return 0 ;; # special case, it's an "*"
     *) return 1        ;;
   esac
}

fixvars()
{
  # Translate all '*' into 'X' to bypass shell expansion hassles.
  # Save original input as "sourceline" for error messages.

  sourceline="$min $hour $dom $mon $dow $command"
   min=$(echo "$min" | tr '*' 'X')      # minute
  hour=$(echo "$hour" | tr '*' 'X')     # hour
   dom=$(echo "$dom" | tr '*' 'X')      # day of month
   mon=$(echo "$mon" | tr '*' 'X')      # month
   dow=$(echo "$dow" | tr '*' 'X')      # day of week
}

if [ $# -ne 1 ] || [ ! -r $1 ] ; then
  # If no crontab filename is given or it's not readable by the script, fail.
  echo "Usage: $0 usercrontabfile" >&2; exit 1
fi

lines=0  entries=0  totalerrors=0

# Go through the crontab file line by line, checking each one.

while read min hour dom mon dow command
do
  lines="$(( $lines + 1 ))" 
  errors=0
  
  if [ -z "$min" -o "${min%${min#?}}" = "#" ] ; then
    # If it's a blank line or the first character of the line is "#", skip it.
    continue    # Nothing to check
  fi


  ((entries++))

  fixvars

  # At this point, all the fields in the current line are split out into
  # separate variables, with all asterisks replaced by "X" for convenience,
  # so let's check the validity of input fields...

  # Minute check

  for minslice in $(echo "$min" | sed 's/[,-]/ /g') ; do
    if ! validNum $minslice 60 ; then
      echo "Line ${lines}: Invalid minute value \"$minslice\""
      errors=1
    fi
  done

  # Hour check
  
  for hrslice in $(echo "$hour" | sed 's/[,-]/ /g') ; do
    if ! validNum $hrslice 24 ; then
      echo "Line ${lines}: Invalid hour value \"$hrslice\"" 
      errors=1
    fi
  done

  # Day of month check

  for domslice in $(echo $dom | sed 's/[,-]/ /g') ; do
    if ! validNum $domslice 31 ; then
      echo "Line ${lines}: Invalid day of month value \"$domslice\""
      errors=1
    fi
  done

  # Month check: Has to check for numeric values and names both.
  #   Remember that a conditional like "if ! cond" means that it's
  #   testing whether the specified condition is FALSE, not true.

  for monslice in $(echo "$mon" | sed 's/[,-]/ /g') ; do
    if ! validNum $monslice 12 ; then
      if ! validMon "$monslice" ; then
        echo "Line ${lines}: Invalid month value \"$monslice\""
        errors=1
      fi
    fi
  done

  # Day of week check: Again, name or number is possible.

  for dowslice in $(echo "$dow" | sed 's/[,-]/ /g') ; do
    if ! validNum $dowslice 7 ; then
      if ! validDay $dowslice ; then
        echo "Line ${lines}: Invalid day of week value \"$dowslice\""
        errors=1
      fi
    fi
  done

  if [ $errors -gt 0 ] ; then
    echo ">>>> ${lines}: $sourceline"
    echo ""
    totalerrors="$(( $totalerrors + 1 ))"
  fi
done < $1 # read the crontab passed as an argument to the script

# Notice that it's here, at the very end of the "while" loop, that we
#   redirect the input so that the user-specified filename can be 
#   examined by the script!

echo "Done. Found $totalerrors errors in $entries crontab entries."

exit 0
