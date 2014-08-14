ac-dcd
======

Auto completion for Emacs using the [D Completion Daemon (DCD)](https://github.com/Hackerpilot/DCD).
Coding in a [dub](https://github.com/D-Programming-Language/dub) project?
You should also probably use [ac-dcd-dub](https://github.com/atilaneves/ad-dcd-dub).

Usage
-----

Add this to your `.emacs` / `init.el`:


    (require 'ac-dcd)
    (add-to-list 'ac-modes 'd-mode)
    (add-hook 'd-mode-hook (lambda () (setq ac-sources (append '(ac-source-dcd) ac-sources))))


Make sure that the `dcd-client` binary is in your `PATH` and that the dcd-server is running.


Installation
------------

Install from [MELPA](melpa.milkbox.net) or [MELPA Stable](http://melpa-stable.milkbox.net/) with:

    M-x package-install RET ac-dcd.
