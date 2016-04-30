#!/bin/bash
# validAlphaNum--Ensures that input consists only of alphabetical
#   and numeric characters.

validAlphaNum()
{
  # Validate arg: returns 0 if all upper+lower+digits, 1 otherwise.
  # Remove all unacceptable chars.
  validchars="$(echo $1 | sed -e 's/[^[:alnum:]]//g')"

  if [ "$validchars" = "$1" ] ; then
    return 0
  else
    return 1
  fi
}

# BEGIN MAIN SCRIPT-–DELETE EVERYTHING BELOW THIS LINE IF YOU
#   WANT TO INCLUDE THIS IN OTHER SCRIPTS.
# =================
#/bin/echo -n "Enter input: "
#read input

# Input validation
#if ! validAlphaNum "$input" ; then
#  echo "Your input must consist of only letters and numbers." >&2
#  exit 1
#else
#  echo "Input is valid."
#fi

#exit 0
