# cactuscon-2019

### Running the examples

- [Install comby](https://github.com/comby-tools/comby#install-pre-built-binaries)
- The match `with-highlights` utility is work in progress and not available yet :) You can run all the examples and get plain text output with the commands below
- In general, run the commands at the root directory of the directory or repository that you want to search
- Tack on `-stats` to get a summary of matches and number of files searched
- See more command line options with `-h` and usage at [comby.dev](https://comby.dev)


**Example `libssh2`**

- git clone [libssh2-f1cfa55](https://github.com/rvantonder/libssh2-f1cfa55), which is at the commit with the pattern
- cd `libssh2-f1cfa55`
- Then run:

```
comby 'alloc_workqueue(:[args]);' '' .c -match-only -stats
```

**Example `Linux Kernel`**

- git clone the linux kernel, or any repository you want to search over
- `cd` into the root directory, then run these commands

Part 1
```
comby 'alloc_workqueue(:[args]); :[[word]]' '' -rule 'where :[[word]] != "if"' .c -match-only
```

Part 2
```
comby 'alloc_workqueue(:[args]); :[[word]]' '' -rule 'where :[[word]] != "if", :[[word]] != "BUG_ON"' .c -match-only
```

**Example `Kubernetes`**

- `git clone https://github.com/kubernetes/kubernetes`
- `cd kubernetes`

```
comby ':[[v]], err := strconv.ParseInt(:[1], :[2], 64) :[rest]' '' -rule 'where match :[rest] { | "int32(:[arg])" -> :[arg] == :[[v]] }' .c -match-only
```
