# Command Line

### `grep`

### `awk`

### `cut`

### `tr [OPTION] SET1 [SET2]`

- `-d` delete characters in the first set from the output

- `-s` replaces repeated characters listed in the `set1` with single occurrence

  ```shell
  > echo 'aaaaabcd' | tr -s 'a'
  abcd

  > echo $PATH
  /bin:/usr/sbin:/sbin

  > echo $PATH | tr -d ':' '\n'
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
