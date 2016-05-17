#!/bin/bash
# frameit - script to make it easy to add a graphical frame around
#   an image file, using ImageMagick

usage()
{
cat << EOF
Usage: $(basename $0) -b border -c color imagename
   or  $(basename $0) -f frame  -m color imagename

In the first case, specify border parameters as size x size or percentage x percentage
followed by the color desired for the border (RGB or color name).

In the second instance, specify the frame size and offset, followed by the
matte color.

EXAMPLE USAGE:
   $(basename $0) -b 15x15 -c black imagename
   $(basename $0) -b 10%x10% -c grey imagename

   $(basename $0) -f 10x10+10+0 imagename
   $(basename $0) -f 6x6+2+2 -m tomato imagename
EOF
exit 1
}

#### MAIN CODE BLOCK

# Most of this is parsing starting arguments!

while getopts "b:c:f:m:" opt; do
  case $opt in
   b ) border="$OPTARG";                ;;
   c ) bordercolor="$OPTARG";           ;;
   f ) frame="$OPTARG";                 ;;
   m ) mattecolor="$OPTARG";            ;;
   ? ) usage;                           ;;
  esac
done
shift $(($OPTIND - 1))  # eat all the parsed arguments

if [ $# -eq 0 ] ; then     # no images specified?
  usage
fi

# did we specify a border and a frame?

if [ ! -z "$bordercolor" -a ! -z "$mattecolor" ] ; then
  echo "$(basename $0): You can't specify a color and matte color simultaneously." >&2
  exit 1
fi

if [ ! -z "$frame" -a ! -z "$border" ] ; then
  echo "$(basename $0): You can't specify a border and frame simultaneously." >&2
  exit 1
fi

if [ ! -z "$border" ] ; then
  args="-bordercolor $bordercolor -border $border"
else
  args="-mattecolor $mattecolor -frame $frame"
fi


for name
do
  suffix="$(echo $name | rev | cut -d. -f1 | rev)"
  prefix="$(echo $name | rev | cut -d. -f2- | rev)"
  newname="$prefix+f.$suffix"
  echo "Adding a frame to image $name, saving as $newname"
  convert $name $args $newname
done

exit 0
