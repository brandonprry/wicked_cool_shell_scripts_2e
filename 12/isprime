#!/bin/bash
# isprime - given a number, ascertain if it's a prime or not
#     This uses what's know as trial division: simply check to see if any
#     number from 2 .. (n-1) divides into the number without a remainder.

  counter=2
remainder=1

if [ $# -eq 0 ] ; then
  echo "Usage: isprime NUMBER" >&2
  exit 1
fi

number=$1

# 3 and 2 are primes, 1 is not.

if [ $number -lt 2 ] ; then
  echo "No, $number is not a prime" ; exit 0
fi

# now let's run some calculations

while [ $counter -le $(expr $number / 2) -a $remainder -ne 0 ]
do
  remainder=$(expr $number % $counter)  # '/' is divide, '%' is remainder
  # echo "  for counter $counter, remainder = $remainder"
  counter=$(expr $counter + 1)
done

if [ $remainder -eq 0 ] ; then
  echo "No, $number is not a prime"
else
  echo "Yes, $number is a prime"
fi
exit 0
