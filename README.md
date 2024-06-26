# ssm

SVG spritesheet maker

[![CI](https://github.com/obeezzy/ssm/actions/workflows/main.yml/badge.svg)](https://github.com/obeezzy/ssm/actions/workflows/main.yml)
[![Deployment to PyPI](https://github.com/obeezzy/ssm/actions/workflows/deploy.yml/badge.svg?branch=v0.1.0)](https://github.com/obeezzy/ssm/actions/workflows/deploy.yml)

__ssm__ is a command-line tool for creating and managing SVG spritesheets. It has 5 main functions:

* __create__: For creating spritesheets from a list of SVG sprites (i.e. SVG icons etc.).
* __list__: For listing the SVG sprites stored in a spritesheet.
* __add__: For adding SVG sprites to an existing spritesheet.
* __remove__: For removing SVG sprites from an existing spritesheet.
* __export__: For exporting SVG sprites from an existing spritesheet; Can be used for converting a `<symbol>` back into a standalone `<svg>` or to display a format suitable for use in HTML (using `<use>`).

For more details, run `ssm -h` after installation.

## Installation

To install the most stable version of this package, run:
```bash
$ pip install ssm-svg
```

## Usage example

Create spritesheet `icons.svg` with `search.svg` and `menu.svg` as sprites:

```bash
$ ssm create -f icons.svg search.svg menu.svg
$ cat icons.svg
<svg xmlns="http://www.w3.org/2000/svg">
  <defs>
    <symbol id="search" viewBox="0 0 24 24">...</symbol>
    <symbol id="menu" viewBox="0 0 24 24">...</symbol>
  </defs>
</svg>
```

Create spritesheet and overwrite existing file (with the `-F` option):

```bash
$ ssm create -f icons.svg search.svg menu.svg -F
```

Create spritesheet containing `search.svg` and `menu.svg`, with custom ID `hamburger-icon` for `menu.svg` (instead of defaulting to its file name):

```bash
$ ssm create -f icons.svg search.svg hamburger-icon=menu.svg -F
$ cat icons.svg
<svg xmlns="http://www.w3.org/2000/svg">
  <defs>
    <symbol id="search" viewBox="0 0 24 24">...</symbol>
    <symbol id="hamburger-icon" viewBox="0 0 24 24">...</symbol>
  </defs>
</svg>
```

List IDs of sprites in spritesheet:

```bash
$ ssm list -f icons.svg
hamburger-icon
search
```

Add `facebook.svg` and `instagram.svg` to spritesheet:

```bash
$ ssm add -f icons.svg facebook.svg instagram.svg
$ cat icons.svg
<svg xmlns="http://www.w3.org/2000/svg">
  <defs>
    <symbol id="search" viewBox="0 0 24 24">...</symbol>
    <symbol id="hamburger-icon" viewBox="0 0 24 24">...</symbol>
    <symbol id="facebook" viewBox="0 0 24 24">...</symbol>
    <symbol id="instagram" viewBox="0 0 24 24">...</symbol>
  </defs>
</svg>
```

Remove sprites with IDs `facebook` and `instagram` from spritesheet:

```bash
$ ssm remove -f icons.svg facebook instagram
$ cat icons.svg
<svg xmlns="http://www.w3.org/2000/svg">
  <defs>
    <symbol id="search" viewBox="0 0 24 24">...</symbol>
    <symbol id="hamburger-icon" viewBox="0 0 24 24">...</symbol>
  </defs>
</svg>
```

NOTE: Inserting the same ID more than once would cause an error.

Add `facebook.svg` to spritesheet with custom ID `fb-icon` (instead of defaulting to its file name):

```bash
$ ssm add -f icons.svg fb-icon=facebook.svg
$ cat icons.svg
<svg xmlns="http://www.w3.org/2000/svg">
  <defs>
    <symbol id="search" viewBox="0 0 24 24">...</symbol>
    <symbol id="hamburger-icon" viewBox="0 0 24 24">...</symbol>
    <symbol id="fb-icon" viewBox="0 0 24 24">...</symbol>
  </defs>
</svg>
```

Export sprite with ID `menu` from spritesheet:

```bash
$ ssm export -f icons.svg menu
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
    <!-- "menu" SVG elements -->
</svg>
```

Export sprite with ID `menu` from spritesheet for use in HTML:

```bash
$ ssm export -f icons.svg menu --use
<svg><use href="icons.svg#menu"></use></svg>
```

Export sprites with IDs `search` and `menu` from spritesheet as `exported_files/search.svg` and `exported_files/menu.svg` respectively:

```bash
$ ssm export -f icons.svg --dir exported_files search menu
$ cat exported_files/search.svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
    <!-- "search" SVG elements -->
</svg>
$ cat exported_files/menu.svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
    <!-- "menu" SVG elements -->
</svg>
```

## License

[MIT](https://choosealicense.com/licenses/mit/)
