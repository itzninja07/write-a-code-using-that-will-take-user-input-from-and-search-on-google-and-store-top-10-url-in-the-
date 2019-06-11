#!/bin/bash

if [[ $(echo $*) ]]; then

    searchterm="$*"

else

    read -p "Type here to search: " searchterm

fi

searchterm=$(echo $searchterm | sed -e 's/\ /+/g')

lynx --dump http://www.google.com/search?q=$searchterm | grep https:// | head | cut -d"-" -f 1 | tr -d "[:blank:]" >>new.txt
#cat new.txt

while read web
do
   google-chrome $web

done < new.txt

rm new.txt
