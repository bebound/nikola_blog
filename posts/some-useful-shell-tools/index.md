<!--
.. title: Some Useful Shell Tools
.. slug: some-useful-shell-tools
.. date: 2017-05-07 00:10:25 UTC+08:00
.. tags: shell
.. category:
.. link:
.. description:
.. type: text
-->

Here are some shell tools I use, which can boost your productivity.

### [Prezto](https://github.com/sorin-ionescu/prezto)

A zsh configuration framework. Provides auto completion, prompt theme and lots of modules to work with other useful tools. I extremely love the `agnoster` theme.

![agnoster](/images/shell_agnoster.png)


### [Fasd](https://github.com/clvv/fasd)

Help you to navigate between folders and launch application.

Here are the official usage example:
```
  v def conf       =>     vim /some/awkward/path/to/type/default.conf
  j abc            =>     cd /hell/of/a/awkward/path/to/get/to/abcdef
  m movie          =>     mplayer /whatever/whatever/whatever/awesome_movie.mp4
  o eng paper      =>     xdg-open /you/dont/remember/where/english_paper.pdf
  vim `f rc lo`    =>     vim /etc/rc.local
  vim `f rc conf`  =>     vim /etc/rc.conf
```

### [pt](https://github.com/monochromegane/the_platinum_searcher)

A fast code search tool similar to `ack`.

### [fzf](https://github.com/junegunn/fzf)

A great fuzzy finder, it can also integrate with vim by [fzf.vim](https://github.com/junegunn/fzf.vim)

![fzf](/images/shell_fzf.gif)

### [thefuck](https://github.com/nvbn/thefuck)

Magnificent app which corrects your previous console command.

![thefuck](/images/shell_thefuck.gif)
