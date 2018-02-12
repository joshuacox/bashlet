# bashlet

Tiny Bash Template for starting tiny bash scripts

### Directions

Write a function in bash:

```
echo () {
  funky=$1
  phrase=$2
  echo "$phrase, with more $funky"
}
```

then call your function in the RAISON block

```
if [[ $RAISON == "my_echo" ]]; then
  if [[ $print_help == "true" ]]; then
    echo_usage
    exit 1
  fi
  my_echo $2
  exit 0
```

and now your function can be called thusly:

```
$ bashlet my_echo this_is_my_echo
this_is_my_echo
```

### Options

Getopt processes the options with these lines:

```
# Execute getopt on the arguments passed to this program, identified by the special character $@
short_opts="hv"
long_opts="help,verbose,verbosity:,parallel:"
PARSED_OPTIONS=$(getopt -n "$0" -o "$short_opts" --long "$long_opts" -- "$@")
```

### Parallel

There is also an example for making a task parallel using [GNU Parallel](https://www.gnu.org/software/parallel/)

Try

```
./bashlet --parallel 8 parallel_echo 
```

```
./bashlet --parallel 3 parallel_echo 
```

```
./bashlet --parallel 1 parallel_echo 
```

and notice the different order they return in for each case

### Similar projects

take a look at [b3bp](http://bash3boilerplate.sh/) or their github repo [here](https://github.com/kvz/bash3boilerplate)

##### Differences?

For one mine uses external getopt, I think in the end theirs is a very viable, well thought-out solution and should be considered.  

It might even be considered a progressive path.  

i.e.  take whatever it is that you want to repeatedly do and 

1. put it in a text file
1. add a she-bang bin bash
1. stop now if your needs are met.... until you meet a very similar scenario 
1. start variablizing things with a `$1` here and a `$2` there
1. soon you wrap it all up in a function
1. stick it in bashlet and start parsing options and such and call your function in the main block
1. eventually make your thing into a library and start calling it from a b3bp script.
