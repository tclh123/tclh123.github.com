---
layout: post
title: "vim saving of files as sudo"
date: 2013-12-15 22:40
comments: true
categories: vim, shell
---


## Understanding `:w !sudo tee %`

**Following is copied from Andrew Marshall's answer on [StackOverflow](http://stackoverflow.com/questions/2600783/how-does-the-vim-write-with-sudo-trick-work/7078429#7078429).**

### % means "the current file"

As eugene y pointed out, % does indeed mean "the current file name". Another use for this in Vim is in substitution commands. For example, :%s/foo/bar means "in the current file, replace occurrences of foo with bar." If you highlight some text before typing :s, you'll see that the highlighted lines take the place of % as your substitution range.

### :w isn't updating your file

One confusing part of this trick is that you might think :w is modifying your file, but it isn't. If you opened and modified file1.txt, then ran :w file2.txt, it would be a "save as"; file1.txt wouldn't be modified, but the current buffer contents would be sent to file2.txt.

Instead of file2.txt, you can substitute a shell command to receive the buffer contents. For instance, :w !cat will just display the contents.

If Vim wasn't run with sudo access, its :w can't modify a protected file, but if it passes the buffer contents to the shell, a command in the shell can be run with sudo. In this case, we use tee.

### Understanding tee

As for tee, picture the tee command as a T-shaped pipe in a normal bash piping situation: it directs output to specified file(s) and also sends it to standard output, which can be captured by the next piped command.

For example, in ps -ax | tee processes.txt | grep 'foo', the list of processes will be written to a text file and passed along to grep.

     +-----------+    tee     +------------+
     |           |  --------  |            |
     | ps -ax    |  --------  | grep 'foo' |
     |           |     ||     |            |
     +-----------+     ||     +------------+
                       ||   
               +---------------+
               |               |
               | processes.txt |
               |               |
               +---------------+
(Diagram created with Asciiflow.)

See the tee man page for more info.

### Tee as a hack

In the situation your question describes, using tee is a hack because we're ignoring half of what it does. sudo tee writes to our file and also sends the buffer contents to standard output, but we ignore standard output. We don't need to pass anything to another piped command in this case; we're just using tee as an alternate way of writing a file and so that we can call it with sudo.

### Making this trick easy

You can add this to your .vimrc to make this trick easy-to-use: just type :w!!.

```
" Allow saving of files as sudo when I forgot to start vim using sudo.
cmap w!! w !sudo tee > /dev/null %
The > /dev/null part explicitly throws away the standard output, since, as I said, we don't need to pass anything to another piped command.
```

