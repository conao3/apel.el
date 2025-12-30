# APEL - A Portable Emacs Library

APEL is an Emacs Lisp library that provides portable functions and utilities for writing cross-version compatible Emacs packages. It abstracts away differences between Emacs versions and provides convenient utilities for common tasks.

## Overview

APEL consists of several modules:

| Module | Description |
|--------|-------------|
| `poe.el` | Emulation of functions and macros from newer Emacs versions |
| `poem.el` | Portable functions for writing MULE-aware programs |
| `pces.el` | Portable character encoding scheme (coding-system) features |
| `invisible.el` | Utilities for working with invisible text regions |
| `mcharset.el` | MIME charset related features |
| `static.el` | Utilities for static (compile-time) evaluation |
| `broken.el` | Information about broken Emacs facilities |
| `pccl.el` | Utilities for writing portable CCL programs |
| `alist.el` | Association list utilities |
| `calist.el` | Condition tree and condition/situation-alist utilities |
| `path-util.el` | Path management and file detection utilities |
| `filename.el` | Safe filename generation utilities |
| `install.el` | Emacs Lisp package installation utilities |
| `mule-caesar.el` | ROT 13-47-48 Caesar rotation utility |
| `pcustom.el` | Portable custom environment |
| `timezone.el` | Timezone utilities (Y2K compatible) |
| `product.el` | Product version information management |

## Installation

### Using make

```sh
make
make install
```

You can specify the Emacs executable:

```sh
make install EMACS=emacs
```

You can specify installation directories:

```sh
make install PREFIX=/usr/local
make install LISPDIR=~/elisp
```

To see what files will be installed and where:

```sh
make what-where LISPDIR=~/elisp
```

### Manual Installation

Add the APEL directory to your `load-path`:

```elisp
(add-to-list 'load-path "/path/to/apel")
```

## Usage

### alist.el - Association List Utilities

#### `put-alist (ITEM VALUE ALIST)`

Modify ALIST to set VALUE for ITEM. If a pair with car ITEM exists, replace its cdr with VALUE. Otherwise, create a new pair and return a new alist.

#### `del-alist (ITEM ALIST)`

Delete the pair with key ITEM from ALIST.

#### `set-alist (SYMBOL ITEM VALUE)`

Modify the alist stored in SYMBOL to set VALUE for ITEM.

```elisp
(set-alist 'auto-mode-alist "\\.pln$" 'text-mode)
```

#### `modify-alist (MODIFIER DEFAULT)`

Modify alist DEFAULT with alist MODIFIER.

#### `set-modified-alist (SYMBOL MODIFIER)`

Modify the alist value of SYMBOL with alist MODIFIER.

### path-util.el - Path Utilities

#### `add-path (PATH &rest OPTIONS)`

Add PATH to `load-path` if it exists under `default-load-path` directories.

Supported PATH formats:
- Relative to load-path: `"PATH"`
- Home directory relative: `"~/PATH"` or `"~USER/PATH"`
- Absolute: `"/foo/bar/baz"`

Options:
- `'all-paths` - Search from `load-path` instead of `default-load-path`
- `'append` - Add PATH to the end of `load-path`

#### `add-latest-path (PATTERN &optional ALL-PATHS)`

Add the latest versioned path matching PATTERN to `load-path`.

```elisp
;; If bbdb-1.50 and bbdb-1.51 exist, adds bbdb-1.51
(add-latest-path "bbdb")
```

#### `get-latest-path (PATTERN &optional ALL-PATHS)`

Return the latest directory matching PATTERN.

```elisp
(let ((gnus-path (get-latest-path "gnus")))
  (add-path (expand-file-name "lisp" gnus-path))
  (add-to-list 'Info-default-directory-list
               (expand-file-name "texi" gnus-path)))
```

#### `file-installed-p (FILE &optional PATHS)`

Return the absolute path of FILE if it exists in PATHS (defaults to `load-path`).

#### `exec-installed-p (FILE &optional PATHS SUFFIXES)`

Return the absolute path of FILE if it exists in PATHS (defaults to `exec-path`).

#### `module-installed-p (MODULE &optional PATHS)`

Return non-nil if MODULE is provided or exists in PATHS.

### filename.el - Safe Filename Generation

#### `replace-as-filename (STRING)`

Return a safe filename from STRING. Uses `filename-filters` for transformation.

Configuration variables:
- `filename-limit-length` - Maximum filename length
- `filename-replacement-alist` - Alist of characters to replacement strings

## License

APEL is free software distributed under the GNU General Public License (GPL).

## Contributing

Bug reports and suggestions can be sent to:

- English: apel-en@m17n.org
- Japanese: apel-ja@m17n.org

To join the mailing list, send an empty email to:

- English: apel-en-ctl@m17n.org
- Japanese: apel-ja-ctl@m17n.org
