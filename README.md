# TyPrePy: Type Hinting Preprocessor for Python

Writing something so I can write code using type-hinting from Python 3.5+ syntax
while keeping code backwards compatible.

## What it Does:

Takes code written using the new syntax and backports it to the comment-based syntax,
as recommended in [PEP 484][1]. Note that the linked PEP 484 portion is specific to
2.7, this error can arrise in earlier Python 3 versions, as being nearly 2017
doesn't help here.

Old code:

```
def embezzle(self, account: str, funds: int = 1000000, *fake_receipts: str) -> None:
    """Embezzle funds from account using fake receipts."""
    <code goes here>
```

New code:

```
def embezzle(self, account, funds=1000000, *fake_receipts):
    # type: (str, int, *str) -> None
    """Embezzle funds from account using fake receipts."""
    <code goes here>
```

It currently does not auto install the [typing module][2] as that would be silly.

## Installation

Run `pip install typrepy`

You may need to use `sudo` depending on how your computer is configured. I **highly**
recommend using [PyEnv][3] or a similar environment manager however so you don't need
to do that ever again.

### Installation with Bootstrapper

The source for TyPrePy is written with new Python type-hinting. During the build process
for distribution, it runs itself in order to create backwards compatible code. The `pip`
installer is built to use the pre-processed code during install.

If you want to build it entirely from source for some reason, you should clone the repo
and then use the `bootstrap/bootstrap.sh` script to build it from python 3.6+.

## Usage

To use TyPrePy from the command line, simply run `typrepy <file> <destination>`.
Respects normal folder stuff and all that jazz, but won't do anything in-place
unless you run with `--inplace` and include the destination as the same as the
file location.

You can also use TyPrePy as part of a build process (this repository does, for
example). I highly advise against this unless you need to however, as the number
of steps required to build your work is inversely proportional to the number of
people who will use your work.


[1]: https://www.python.org/dev/peps/pep-0484/#suggested-syntax-for-python-2-7-and-straddling-code
[2]: https://pypi.org/project/typing/
[3]: https://github.com/pyenv/pyenv