# Command Line


### `echo [-neE] [ARGUMENTS]`
- `-e` interpert escaped-character
- `-E` Not interpert escaped-character (by default)
- Display output of command `echo $(command)`
```bash
> echo "The date is: $(date +%D)"
The data is '04/13/2020'
```
- Display variable `echo $USER`
```bash
Andrew Chen
```

### `grep [OPTION] [COND] FILE`

- `-E` regex matching

- `-s` replaces repeated characters listed in the `set1` with single occurrence

- `--color` add color for matching element

### `awk`
  ```
  awk '{ print $2 }'
  awk '{ gsub(/[:]/, ".*:") } { print $1":[0-9]+"};'
  ```

### `cut [OPTION] [FILE]`
  - `-f(--field)`  Select by specifying a field, a set of fields, or a range of fields, which separated by`,`. <br/>
    Can set delimiter by using `-d`. Otherwise, it'll use `TAB` by default.
    - `-d(--delimiter`) Specify a delimiter that will be used instead of the default `TAB` delimiter.
    - `-s(--only-delimited`) Cut doesn’t print lines not containing delimiters.

  ```bash
  #input.txt
  Hello World
  Happy New World
  World

  > cut -f1 -d ' ' input.txt
  Hello
  Happy
  World

  > cut -f1,2 -d ' ' input.txt
  Hello World
  Happy New
  World

  > cut -f1 -d ' ' -s input.txt
  Hello
  Happy
  ```

### `sed`
  ```
  sed 's/.$//'
  ```
### `xargs`


### `tr [OPTION] SET1 [SET2]`

- `-d` delete characters in the first set from the output

- `-s` replaces repeated characters listed in the `set1` with single occurrence

```shell
> echo 'aaaaabcd' | tr -s 'a'
abcd

> echo $PATH
/bin:/usr/sbin:/sbin

> echo $PATH | tr ':' '\n'
/bin
/usr/sbin
/sbin
```

- `-c` complements the set of characters in strin

### `sudo su`
  - Change the current user to root user
  - Can achieve by using #
    - e.g. `# echo "Hello World" > /sys/...`
### `tee`
  - print and output the content to a file (`>` don’t print the content)
