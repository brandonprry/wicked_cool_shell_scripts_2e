#!/bin/bash
# open2 - -A smart wrapper for the cool Mac OS X 'open' command
#   to make it even more useful. By default, ‘open’ launches the
#   appropriate application for a specified file or directory
#   based on the Aqua bindings, and it has a limited ability to 
#   launch applications if they're in the /Applications dir.

#   First, whatever argument we're given, try it directly.
if ! open "$@" >/dev/null 2>&1 ; then
  if ! open -a "$@" >/dev/null 2>&1 ; then

    # More than one arg?  Don't know how to deal with it: --quit.
    if [ $# -gt 1 ] ; then
      echo "open: Can't figure out how to open or launch $@More than one program not supported" >&2
      exit 1
    else
        case $(echo $1 | tr '[:upper:]' '[:lower:]') in
        activ*|cpu   ) app="Activity Monitor"           ;;
        addr*        ) app="Address Book"               ;;
        chat         ) app="Messages"                   ;;
        dvd          ) app="DVD Player"                 ;;
        excel        ) app="Microsoft Excel"            ;;
        info*        ) app="System Information"         ;;
        prefs        ) app="System Preferences"         ;;
        qt|quicktime ) app="QuickTime Player"           ;;
        word         ) app="Microsoft Word"             ;;        
        * ) echo "open: Don't know what to do with $1" >&2
            exit 1
      esac
      echo "You asked for $1 but I think you mean $app." >&2
      open -a "$app"
    fi
  fi
fi

exit 0
