

`ssh tsp 'journalctl | grep --line-buffer ssh | grep --line-buffer "Disconnected from"'| less`

- less is pager, convient to show long texts

1. `sed`
   - `cat ssh.log | sed 's/.*Disconnected from //'|less`: replace everything before and  "Disconnected from" to empty

# 1. Regular Expressions

in most cases, by default, it will only match once

by adding g, `s/[ab]//g`, it matches all matching patterns

- `s/(ab|bc)*//g`
- `s/^.*?Disconnected from (invalid | authenticating )?user (.*) [0-9.]+ port [0-9+ ([preauth])?$/\2/`

## 1.2 Debugger



# 2. Data wrangling

- `wx -l` count number of lines
- `sort ` 
  - -n numerical sort
  - -k selected white space separate column
  - 1,1 start with the first column and end with the first column

- `uniq`
  - `uniq -c`
- 



e.g. `cat ssh.log| sed -E 's/^.*Disconnected from (invalid | authenticating )?user (.*) (\[preauth\])?$/\2/'| sort | uniq -c| sort -nk1,1 | tail -n10`

# 3. awk (editor)

- column based editor
- in white-separated columns
- `awk '{print \$2} | paste -sd'` print the second column in a line and separate by ','
- `awk '/$1 ==1 && $2 ~ /^c.*e$ {print \$0}'`: find all lines that the first column is 1 and the second column matches the regular expression that starts with c and ends with e, and then prints the whole line
- Programming language
  - `awk 'BEGIN {rows=0} ...... {rows +=1} END {print rows}'`

# 4. Analyzing data

bc : calculator

- -l 
- `| paste -sd+ | bc -l`
- 



### R

- summary data
  - `|awk '{print $1}'| R --slave -e 'x <- scan(file='stdin', quiet=TRUE); summary(x)'`
- plot data
  - `|sort -nk1,1 | tail -n5 | gnuplot -p -e 'set boxwidth 0.5; plot "-" using 1:xtic(2) with boxes'`
-  

# 5. Data wrangling to make arguments

Make result from command to be the arguments for next command

 `xgars`

- `rustup toolchain list| grep nightly| grep -v 'nightly-x86'| grep 2019|set 's/-86.*//'| xargs echo rustup toolchain uninstall ` 

# 6. Wrangling binary data

- ffmpeg

  - Encode & decode images/videos
  - `ffmpeg -loglevel panic -i /dev/video0 -frames 1 -f image2 -| convert - -colorspace gray -| gzip | ssh tsp  'gzip -d | tee copy.png' | feh - `  take a picture,  -: use standard output | convert to gray picture and print out to the standard output | zip the picture | ssh to remote and decode  

  - ==didn't fully understand, about the pipeline==

# #. Exercises

1. 
2. 2
3. 3
4. 3
5. 3
6. 3

Solution: 