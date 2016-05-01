#!/bin/bash
# validator--Checks to ensure that the PATH contains only valid directories, 
#   then checks that all environment variables are valid.
#   Looks at SHELL, HOME, PATH, EDITOR, MAIL, and PAGER.

errors=0

source ../1/library.sh # which contains Script #1, the in_path() function

validate()
{
  varname=$1    
  varvalue=$2
  
  if [ ! -z $varvalue ] ; then
    if [ "${varvalue%${varvalue#?}}" = "/" ] ; then
      if [ ! -x $varvalue ] ; then
        echo "** $varname set to $varvalue, but I cannot find executable."
        (( errors++ ))
      fi
    else
      if in_path $varvalue $PATH ; then 
        echo "** $varname set to $varvalue, but I cannot find it in PATH."
        errors=$(( $errors + 1 ))
      fi
    fi 
  fi
}

# BEGIN MAIN SCRIPT
# =================

if [ ! -x ${SHELL:?"Cannot proceed without SHELL being defined."} ] ; then
  echo "** SHELL set to $SHELL, but I cannot find that executable."
  errors=$(( $errors + 1 ))
fi

if [ ! -d ${HOME:?"You need to have your HOME set to your home directory"} ]
then
  echo "** HOME set to $HOME, but it's not a directory."
  errors=$(( $errors + 1 ))
fi

# Our first interesting test: Are all the paths in PATH valid?

oldIFS=$IFS; IFS=":"     # IFS is the field separator. We'll change to ':'

for directory in $PATH
do
  if [ ! -d $directory ] ; then
      echo "** PATH contains invalid directory $directory"
      errors=$(( $errors + 1 ))
  fi
done

IFS=$oldIFS             # restore value for rest of script

# The following variables should each be a fully qualified path, 
#   but they may be either undefined or a progname. Add additional 
#   variables as necessary for your site and user community.

validate "EDITOR" $EDITOR
validate "MAILER" $MAILER
validate "PAGER"  $PAGER

# And, finally, a different ending depending on whether errors > 0

if [ $errors -gt 0 ] ; then
  echo "Errors encountered. Please notify sysadmin for help."
else
  echo "Your environment checks out fine."
fi

exit 0
