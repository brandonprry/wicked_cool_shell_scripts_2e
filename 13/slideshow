#!/bin/bash
# slideshow - Display a slideshow of photos from the specified directory. 
#             Uses ImageMagick's "display" utility.

delay=2			# default delay in seconds
psize="1200x900>"	# preferred image size for display

if [ $# -eq 0 ] ; then
  echo "Usage: $(basename $0) watch-directory" >&2 ; exit 1
fi

watch="$1"

if [ ! -d "$watch" ] ; then
  echo "$(basename $0): specified watch directory $watch isn't a directory" >&2 ; exit 1
fi

cd "$watch"

if [ $? -ne 0 ] ; then
  echo "$(basename $0): failed trying to cd into $watch" >&2 ; exit 1
fi

suffixes="$(file * | grep image | cut -d: -f1 | rev | cut -d. -f1 | \
   rev | sort | uniq | sed 's/^/\*./')"

if [ -z "$suffixes" ] ; then
  echo "$(basename $0): no images to display in folder $watch" >&2 ; exit 1
fi

/bin/echo -n "Displaying $(ls $suffixes | wc -l) images from $watch "
set -f ; echo with suffixes $suffixes ; set +f

display -loop 0 -delay $delay -resize $psize -backdrop $suffixes

exit 0
