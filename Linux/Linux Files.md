___
- Commands to view files:
	```
	cat file
	head file
	tail file
	more file 
	less file
	```
- To search in files:
	```
	cat file | grep string
	grep string file 
	```

- Redirecting files:
	```
	ls | grep file # pipe send STDOUT to STDIN
	ls > file # > sends STDOUT to file
	ls 2> file # 2> sends STDERR to file
	file < ls # send STDIN to file
	```
- `/dev/null` is place where copying anything will get disappeared.
- `cat file | tee file2` this will cat the file and also save output into file2. `tee` take STDIN from pipe and displays it as well as saves it.
- `xargs` takes STDIN from pipe and than adds it to second command argument. `cat file | xargs mkdir`.
- `cut` and `paste` can be used to join text files in front of each other.
- `sort` can be used to sort a text file.
- `wc` can be used to count words in a file.
- `sed s/umair/khan/g` sed will replace umair with khan globaly.
___