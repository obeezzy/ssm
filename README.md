# ssm

SVG spritesheet maker

[![CI](https://github.com/obeezzy/ssm/actions/workflows/main.yml/badge.svg)](https://github.com/obeezzy/ssm/actions/workflows/main.yml)
[![Deployment to PyPI](https://github.com/obeezzy/ssm/actions/workflows/deploy.yml/badge.svg?branch=v0.0.4)](https://github.com/obeezzy/ssm/actions/workflows/deploy.yml)

__ssm__ is a simple approach to creating and managing SVG spritesheets. It has 5 main functions:

* __create__: For creating spritesheets from a list of SVG sprites (i.e. SVG icons etc.)
* __list__: For listing the SVG sprites stored in a spritesheet
* __add__: For adding SVG sprites to an existing spritesheet
* __remove__: For removing SVG sprites from an existing spritesheet
* __export__: For exporting SVG sprites from an existing spritesheet. Can be used for converting a `<symbol>` back into a standalone `<svg>` or to display a format suitable for HTML (using `<use>`).

For more details, run `python -m ssm -h` after installation.

## Installation
To install the most stable version of this package, run:
```bash
$ pip install ssm-svg
```

## Usage example

Create spritesheet `icons.svg` with `search.svg` and `menu.svg` as sprites:

```bash
$ python -m ssm create -f icons.svg search.svg menu.svg
$ cat icons.svg
<?xml version='1.0' encoding='UTF-8'?>
<svg xmlns="http://www.w3.org/2000/svg">
  <defs>
    <symbol id="menu" viewBox="0 0 24 24">...</symbol>
    <symbol id="search" viewBox="0 0 24 24">...</symbol>
  </defs>
</svg>
```

Create spritesheet and overwrite existing file:

```bash
$ python -m ssm create -f icons.svg search.svg menu.svg -F
```

Create spritesheet with custom ID `hamburger-icon` instead of defaulting to its file name:

```bash
$ python -m ssm create -f icons.svg search.svg hamburger-icon=menu.svg
$ cat icons.svg
<?xml version='1.0' encoding='UTF-8'?>
<svg xmlns="http://www.w3.org/2000/svg">
  <defs>
    <symbol id="hamburger-icon" viewBox="0 0 24 24">...</symbol>
    <symbol id="search" viewBox="0 0 24 24">...</symbol>
  </defs>
</svg>
```

List IDs of SVG sprites in spritesheet:

```bash
$ python -m ssm list -f icons.svg
menu
search
```

Add SVG sprites to spritesheet:

```bash
$ python -m ssm add -f icons.svg facebook.svg instagram.svg
$ cat icons.svg
<?xml version='1.0' encoding='UTF-8'?>
<svg xmlns="http://www.w3.org/2000/svg">
  <defs>
    <symbol id="hamburger-icon" viewBox="0 0 24 24">...</symbol>
    <symbol id="search" viewBox="0 0 24 24">...</symbol>
    <symbol id="facebook" viewBox="0 0 24 24">...</symbol>
    <symbol id="instagram" viewBox="0 0 24 24">...</symbol>
  </defs>
</svg>
```

Remove SVG sprites with IDs `facebook` and `instagram` from spritesheet:

```bash
$ python -m ssm remove -f icons.svg facebook instagram
$ cat icons.svg
<?xml version='1.0' encoding='UTF-8'?>
<svg xmlns="http://www.w3.org/2000/svg">
  <defs>
    <symbol id="hamburger-icon" viewBox="0 0 24 24">...</symbol>
    <symbol id="search" viewBox="0 0 24 24">...</symbol>
  </defs>
</svg>
```

NOTE: Inserting the same ID more than once would cause an error.

Add SVG sprites to spritesheet with custom ID `fb-icon` instead of defaulting to its file name:

```bash
$ python -m ssm add -f icons.svg fb-icon=facebook.svg
$ cat icons.svg
<?xml version='1.0' encoding='UTF-8'?>
<svg xmlns="http://www.w3.org/2000/svg">
  <defs>
    <symbol id="hamburger-icon" viewBox="0 0 24 24">...</symbol>
    <symbol id="search" viewBox="0 0 24 24">...</symbol>
    <symbol id="fb-icon" viewBox="0 0 24 24">...</symbol>
  </defs>
</svg>
```

Export sprite with ID `menu` from spritesheet:

```bash
$ python -m ssm export -f icons.svg menu
<?xml version='1.0' encoding='utf-8'?>
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">...</svg>
```

Export sprite with ID `menu` from spritesheet for use in HTML:

```bash
$ python -m ssm export -f icons.svg menu --use
<svg><use href="icons.svg#menu"></use></svg>
```

Export sprite with IDs `search` and `menu` from spritesheet as `exported_files/search.svg` and `exported_files/menu.svg` respectively:

```bash
$ python -m ssm export -f icons.svg --dir exported_files search menu
$ cat exported_files/menu.svg
<?xml version='1.0' encoding='utf-8'?>
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">...</svg>
$ cat exported_files/search.svg
<?xml version='1.0' encoding='utf-8'?>
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">...</svg>
```

## License

[MIT](https://choosealicense.com/licenses/mit/)
