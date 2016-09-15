#!/bin/bash
# dayinpast - given a date, report what day of the week it was

if [ $# -ne 3 ] ; then
  echo "Usage: $(basename $0) mon day year" >&2
  echo "  with just numerical values (ex: 7 7 1776)" >&2
  exit 1
fi

date --version > /dev/null 2>&1 	# discard error, if any
baddate="$?"				# just look at return code

if [ ! $baddate ] ; then
  date -d $1/$2/$3 +"That was a %A."
else

  if [ $2 -lt 10 ] ; then
    pattern=" $2[^0-9]"
  else
    pattern="$2[^0-9]"
  fi

  dayofweek="$(ncal $1 $3 | grep "$pattern" | cut -c1-2)"

  case $dayofweek in 
    Su ) echo "That was a Sunday"; 	;;
    Mo ) echo "That was a Monday"; 	;;
    Tu ) echo "That was a Tuesday"; 	;;
    We ) echo "That was a Wednesday"; 	;;
    Th ) echo "That was a Thursday"; 	;;
    Fr ) echo "That was a Friday"; 	;;
    Sa ) echo "That was a Saturday"; 	;;
  esac
fi
exit 0
