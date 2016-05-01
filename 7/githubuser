#!/bin/bash
# githubuser--Given a GitHub username, pulls information about them.

if [ $# -ne 1 ]; then
  echo "Usage: $0 <username>"
  exit 1
fi

# The -s silences curl's normally verbose output.
curl -s "https://api.github.com/users/$1" | \
        awk -F'"' '
            /\"name\":/ { 
              print $4" is the name of the Github user."
            }
            /\"followers\":/{ 
              split($3, a, " ") 
              sub(/,/, "", a[2])
              print "They have "a[2]" followers." 
            }
            /\"following\":/{
              split($3, a, " ")
              sub(/,/, "", a[2])
              print "They are following "a[2]" other users."
            }
            /\"created_at\":/{
              print "Their account was created on "$4"."
            }
            '
exit 0
