# colorize less

- execute `sudo apt-get install source-highlight`
  
# add this to ~/.lessfilter
```
case "$1" in
    .bash_|*.bat|*.bib|*.c|Changelog|*.diff|Gemfile|\
    *.gemspec|*.h|*.ini|*.js|*.json|*.jsonld|\
    Makefile|*.md|*.patch|*.php|*.pl|*.pm|*.py|Rakefile|\
    *.rake|*.rb|*.R|*.Rprofile|*.rss|*.sh|*.sql|*.xsl|\
    *.tex|*.toc|*.yaml|*.yml)
        source-highlight --failsafe --infer-lang -f esc --style-file=esc.style -i "$1" ;;

*.pdf)
    if command -v pdftotext > /dev/null 2>&1 ; then pdftotext -layout "$1" -
    else echo "No pdftotext available; try installing poppler-utils"; fi ;;

*.txt)
    source-highlight --failsafe --infer-lang -f esc --style-file=esc.style -s changelog -i "$1" ;;
*)
    if grep -q "#\!/bin/bash" "$1" 2> /dev/null; then
        source-highlight --failsafe --infer-lang -f esc --style-file=esc.style -s bash -i "$1"
    fi
    exit 1
esac;

exit 0
```

- execute `chmod u+x ~/.lessfilter`
- add to ~/.bashrc
```
export LESS='-R'
export LESSOPEN='|~/.lessfilter %s'
```

