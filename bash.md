Read n bytes from urandom (in hex):

`xxd -l 200 -p /dev/urandom | tr -d " \n" ; echo`

Get words frequency from a file:

```bash
#!/bin/bash

# preprocessing
tr '[:space:]' '[\n*]' < "$1" | tr -dc '[:alpha:]\n\r' | tr -s '\n' > "$1.bsd_btw.txt"

# uniq
cat "$1.bsd_btw.txt" | sort | uniq > "$1.bsd_btw.txt.uniq"

# final
while read p; do 
  echo "$p - $(cat "$1.bsd_btw.txt" | grep "$p" | wc -l)" >> "$1.bsd_btw.txt.result"
done <"$1.bsd_btw.txt.uniq"

# display result
cat "$1.bsd_btw.txt.result" | column -t | sort -t '-' -k2 -g
```

Colors:

```bash
tput setaf 2  # Generates green text
tput bold     # Generate bold text
tput sgr0     # Reset those fancy effects

# To use them as variables:
bold=$(tput bold)
green=$(tput setaf 2)
reset=$(tput sgr0)
echo "${bold}HEADING${reset}"
```

Get words frequency updated(inmem):

```bash
#!/bin/bash

pre="$(mktemp -p /dev/shm/)"
uniq="$(mktemp -p /dev/shm/)"
result="$(mktemp -p /dev/shm/)"

# preprocessing
tr -c '[:alpha:]\n\r_' ' ' < "$1" | tr '[:space:]' '[\n*]' | tr -dc '[:alpha:]\n\r_' | tr -s '\n' > "$pre"

# uniq
cat "$pre" | sort | uniq > "$uniq"

# final
while read p; do 
  echo "$p - $(cat "$pre" | grep "$p" | wc -l)" >> "$result"
done <"$uniq"

# display result
cat "$result" | column -t | sort -t '-' -k2 -g
```
