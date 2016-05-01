#!/bin/bash
# watermark -- add specified text as a watermark on the input image
#    saving the output as image+wm

wmfile="/tmp/watermark.$$.png"
fontsize="44"		# should be a starting arg

trap "`which rm` -f $wmfile" 0 1 15    # no temp file left behind

if [ $# -ne 2 ] ; then
  echo "Usage: $(basename $0) imagefile "watermark text"" >&2 ; exit 1
fi

if [ ! -r "$1" ] ; then
  echo "$(basename $0): Can't read input image $1" >&2 ; exit 1
fi

# to start, get the dimensions of the image

dimensions="$(identify -format "%G" "$1")"

# now let's create the temporary watermark overlay

convert -size $dimensions xc:none -pointsize $fontsize -gravity south \
  -draw "fill black text 1,1 '$2' text 0,0 '$2' fill white text 2,2 '$2'" \
  $wmfile

# echo "created watermark file with dimensions $dimensions"

# now let's composite the overlay and the original file

suffix="$(echo $1 | rev | cut -d. -f1 | rev)"
prefix="$(echo $1 | rev | cut -d. -f2- | rev)"

newfilename="$prefix+wm.$suffix"
composite -dissolve 75% -gravity south $wmfile "$1" "$newfilename"

echo "Created new watermarked image file $newfilename"

exit 0
