---
title: verilog-mode.el
date: 2022-05-13 14:07:29
tags:
categories:
- cad
---

```bash
emacs --no-site-file --load path/to/verilog-mode.el --batch filename.v -f verilog-auto-save-compile
```

> CAUTION: *filename.v* is **overwrite** by command

## verilog-mode.el

```verilog
/*AUTOINPUT*/
/*AUTOWIRE*/
/*AUTOINST*/
/*AUTO_TEMPLATE*/
```

### `-f verilog-batch-auto`

> For use with `--batch`, perform automatic expansions as a stand-alone tool. This sets up the appropriate Verilog mode environment, updates automatics with M-x verilog-auto on all command-line files, and saves the buffers.
> For proper results, multiple filenames need to be passed on the command line in bottom-up order.

### `-f verilog-auto-save-compile`

> Update automatics with M-x verilog-auto, save the buffer, and *compile*



## Emacs

### `--no-site-file`

Another file for site-customization is `site-start.el`. Emacs loads this *before* the user's init file (`.emacs`, `.emacs.el` or `.emacs.d/.emacs.d`). You can inhibit the loading of this file with the option ``--no-site-file``

### `--batch`

The command-line option `--batch` causes Emacs to run noninteractively.  The idea is that you specify Lisp programs to run; when they are finished, Emacs should exit.

 `--load, -l FILE`, load Emacs Lisp FILE using the load function; 

`--funcall, -f FUNC`, call Emacs Lisp function FUNC with no arguments

### `-f FUNC`

`--funcall, -f FUNC`, call Emacs Lisp function FUNC with no arguments

### `--load, -l FILE`

`--load, -l FILE`, load Emacs Lisp FILE using the load function

> Verilog-mode is a standard part of GNU Emacs as of 22.2.



## multiple directories

**AUTOINST** only search in the file's directory default.

You can append below `verilog-library-directories` for multiple directories search

```
// Local Variables:
// verilog-library-directories:("." "subdir" "subdir2")
// End:
```



## reference

Emacs Online Documentation [https://doc.endlessparentheses.com/](https://doc.endlessparentheses.com/)

Emacs verilog-mode 的使用 URL: [https://www.wenhui.space/docs/02-emacs/verilog_mode_useguide/](https://www.wenhui.space/docs/02-emacs/verilog_mode_useguide/)
