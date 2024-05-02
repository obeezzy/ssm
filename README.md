# ssm

SVG spritesheet maker

[![CI](https://github.com/obeezzy/ssm/actions/workflows/main.yml/badge.svg)](https://github.com/obeezzy/ssm/actions/workflows/main.yml)
[![Deployment to PyPI](https://github.com/obeezzy/ssm/actions/workflows/deploy.yml/badge.svg?branch=v0.0.1)](https://github.com/obeezzy/ssm/actions/workflows/deploy.yml)

__ssm__ is a simple approach to creating and managing SVG spritesheets. It has 5 main functions:

* __create__: For creating spritesheets from a list of SVG sprites (i.e. SVG icons etc.)
* __list__: For listing the SVG sprites stored in a spritesheet
* __add__: For adding SVG sprites to an existing spritesheet
* __remove__: For remove SVG sprites from an existing spritesheet
* __export__: For exporting SVG sprites from an existing spritesheet. Can be used for converting a `<symbol>` back into a standalone `<svg>` or to display a format suitable for HTML (using `<use>`).

For more details, run `python -m ssm -h` after installation.

## Installation
To install the most stable version of this package, run:
```bash
$ pip install ssm-svg
```

## Usage example

Create spritesheet:

```bash
$ python -m ssm create -f icons.svg search.svg menu.svg
```

Create spritesheet and overwrite existing file:

```bash
$ python -m ssm create -f icons.svg search.svg menu.svg -F
```

Create spritesheet with custom IDs for SVG sprites:

```bash
$ python -m ssm create -f spritesheet.svg search-icon=search.svg hamburger-icon=menu.svg
```

List IDs of SVG sprites in spritesheet:

```bash
$ python -m ssm list -f spritesheet.svg
```

Add SVG sprites to spritesheet:

```bash
$ python -m ssm add -f spritesheet.svg facebook.svg instagram.svg
```

Add SVG sprites to spritesheet with custom IDs for SVG sprites:

```bash
$ python -m ssm add -f spritesheet.svg fb-icon=facebook.svg gram-icon=instagram.svg
```

Remove SVG sprites from spritesheet:

```bash
$ python -m ssm remove -f spritesheet.svg fb-icon gram-icon
```

Export SVG sprites from spritesheet:

```bash
$ python -m ssm export -f spritesheet.svg search
```

Export SVG sprites from spritesheet for use in HTML:

```bash
$ python -m ssm export -f spritesheet.svg search --use
```

## License

[MIT](https://choosealicense.com/licenses/mit/)
