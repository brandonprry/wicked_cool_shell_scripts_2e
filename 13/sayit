#!/bin/bash
# sayit -- [Mac OS X only] uses the Mac "say" command to 
#          read whatever's specified

dosay="`which say` --quality=127"
format="`which fmt` -w 70"

voice=""	    	      # default system voice
rate=""			# default to the standard speaking rate

demovoices()
{
   # offer up a sample of each available voice

   voicelist=$( say -v \? | grep "en_" | cut -c1-12 | 
       sed 's/ /_/;s/ //g;s/_$//')

   if [ "$1" = "list" ] ; then
     echo Available voices: $(echo $voicelist | sed 's/ /, /g;s/_/ /g') | $format
     echo "HANDY TIP: use \"$(basename $0) demo\" to hear all the voices"
     exit 0
   fi

   for name in $voicelist ; do
     myname=$(echo $name | sed 's/_/ /')
     echo "Voice: $myname"
     $dosay -v "$myname" "Hello! I'm $myname. This is what I sound like."
   done

   exit 0
}

usage()
{
   echo "Usage: sayit [-v voice] [-r rate] [-f file] phrase"
   echo "   or: sayit demo"
   exit 0
}

while getopts "df:r:v:" opt; do
  case $opt in
    d ) demovoices list	   ;;
    f ) input="$OPTARG"    ;;
    r )  rate="-r $OPTARG" ;;
    v ) voice="$OPTARG"    ;;
  esac
done

shift $(($OPTIND - 1))

if [ $# -eq 0 -a -z "$input" ] ; then
  $dosay "Dude! You haven't given me any parameters to work with."
  echo "Error: no parameters specified. Specify a file or phrase"
  exit 0
fi

if [ "$1" = "demo" ] ; then
  demovoices
fi

if [ ! -z "$input" ] ; then
  $dosay $rate -v "$voice" -f $input
else
  $dosay $rate -v "$voice" "$*"
fi
exit 0
