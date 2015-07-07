ac-dcd
======

Auto completion for Emacs using the [D Completion Daemon (DCD)](https://github.com/Hackerpilot/DCD).


Requirements
------------
The [auto-complete](https://github.com/auto-complete/auto-complete) package must be installed. Also,
[yasnippet](https://github.com/capitaomorte/yasnippet) and
[popwin](https://github.com/m2ym/popwin-el) are recommended.

Installing ac-dcd from MELPA (see below) automatically installs auto-complete if not already installed.

Make sure that the `dcd-client` and `dcd-server` binaries are in your `PATH`. Otherwise, please
set the variables  `dcd-executable` and `dcd-server-executable` using `M-x customize`.


Usage
-----

Add this to your `.emacs` / `init.el`:


        ;;; ac-dcd
        (require 'ac-dcd)
        (add-hook 'd-mode-hook
          (lambda ()
              (auto-complete-mode t)
              (when (featurep 'yasnippet) (yas-minor-mode-on))
              (ac-dcd-maybe-start-server)
              (ac-dcd-add-imports)
              (add-to-list 'ac-sources 'ac-source-dcd)
              (define-key d-mode-map (kbd "C-c ?") 'ac-dcd-show-ddoc-with-buffer)
              (define-key d-mode-map (kbd "C-c .") 'ac-dcd-goto-definition)
              (define-key d-mode-map (kbd "C-c ,") 'ac-dcd-goto-def-pop-marker)
              (define-key d-mode-map (kbd "C-c s") 'ac-dcd-search-symbol)

              (when (featurep 'popwin)
                (add-to-list 'popwin:special-display-config
                             `(,ac-dcd-error-buffer-name :noselect t))
                (add-to-list 'popwin:special-display-config
                             `(,ac-dcd-document-buffer-name :position right :width 80))
                (add-to-list 'popwin:special-display-config
                             `(,ac-dcd-search-symbol-buffer-name :position bottom :width 5)))))

Alternatively,

    (add-hook 'd-mode-hook 'ac-dcd-setup)

Which does the same as the code above.

* You can set import paths using `M-x customize-variable RET ac-dcd-flags`.
* Alternatively, if you're using [DUB](http://code.dlang.org/) to manage your
  project, you can use `M-x ac-dcd-add-imports` to add import paths of the
  current project automatically.
* When something is wrong, please, check variables with `M-x customize-apropos
  RET ac-dcd` and restart server with `M-x ac-dcd-init-server`.


Features
--------
* Dlang source for auto-complete
* Function calltip expansion with yasnippet
* Show ddoc with `C-c ?`
* Goto definition with `C-c .`
* After goto definition, you can pop to previous position with `C-c ,`
* Search for a symbol and show the results in a temporary buffer with `C-c s`


Installation
------------

Install from [MELPA](http://melpa.milkbox.net) or [MELPA Stable](http://melpa-stable.milkbox.net/) with:

    M-x package-install RET ac-dcd.


Possible Issues
---------------

`ac-dcd-maybe-start-server` only guaranteed to work with one Emacs instance. On systems
with `pidof`, A 2nd Emacs will not attempt to start its own dcd-server and simply talk
to the one already running.


TODO
----

* UTF-8 support is in place. However, UTF-16 and UTF-32 may not work correctly.
  (Need help!)
