.. GuessIt documentation master file, created by
   sphinx-quickstart on Sun Nov 29 15:18:07 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

GuessIt
=======

.. image:: http://img.shields.io/pypi/v/guessit.svg
    :target: https://pypi.python.org/pypi/guessit
    :alt: Latest Version

.. image:: http://img.shields.io/badge/license-LGPLv3-blue.svg
    :target: https://pypi.python.org/pypi/guessit
    :alt: LGPLv3 License

.. image:: http://img.shields.io/travis/guessit-io/guessit.svg
    :target: https://travis-ci.org/guessit-io/guessit
    :alt: Build Status

.. image:: http://img.shields.io/coveralls/guessit-io/guessit.svg
    :target: https://coveralls.io/github/guessit-io/guessit
    :alt: Coveralls

GuessIt is a python library that extracts as much information as possible from a video filename.

It has a very powerful matcher that allows to guess :ref:`properties <properties>` from a video using its filename only.
This matcher works with both movies and tv shows episodes.

For example, GuessIt can do the following::

    $ guessit "Treme.1x03.Right.Place,.Wrong.Time.HDTV.XviD-NoTV.avi"
    For: Treme.1x03.Right.Place,.Wrong.Time.HDTV.XviD-NoTV.avi
    GuessIt found: {
        "title": "Treme",
        "season": 1,
        "episode": 3,
        "episode_title": "Right Place, Wrong Time",
        "format": "HDTV",
        "video_codec": "XviD",
        "release_group": "NoTV",
        "container": "avi",
        "mimetype": "video/x-msvideo",
        "type": "episode"
    }

Migration note
--------------

GuessIt 2 has been rewriten from scratch. GuessIt is now a release name parser only, and support for additional
features like hashes computations has been dropped.

To migrate from guessit ``0.x`` or ``1.x``, please read the :ref:`migration page<migration>`.

Install
-------

Installing GuessIt is simple with `pip <http://www.pip-installer.org/>`_::

    $ pip install guessit

You can also :ref:`install from sources <sources>`.

Usage
-----

GuessIt can be used from command line::

    $ guessit
    usage: guessit [-h] [-c CONFIG] [-t TYPE] [-n] [-Y] [-D]
                   [-L ALLOWED_LANGUAGES] [-C ALLOWED_COUNTRIES] [-E]
                   [-T EXPECTED_TITLE] [-G EXPECTED_GROUP] [-f INPUT_FILE] [-v]
                   [-P SHOW_PROPERTY] [-a] [-j] [-y] [-p] [-V] [--version]
                   [filename [filename ...]]

    positional arguments:
      filename              Filename or release name to guess

    optional arguments:
      -h, --help            show this help message and exit

    Naming:
      -c CONFIG, --config CONFIG
                            Filepath to the configuration file. Configuration
                            contains the same options as those command line
                            options, but option names have "-" characters replaced
                            with "_". If not defined, guessit tries to read a
                            configuration default configuration file at
                            ~/.guessit/options.(json|yml|yaml) and
                            ~/.config/guessit/options.(json|yml|yaml). Set to
                            "false" to disable default configuration file loading.
      -t TYPE, --type TYPE  The suggested file type: movie, episode. If undefined,
                            type will be guessed.
      -n, --name-only       Parse files as name only, considering "/" and "\" like
                            other separators.
      -Y, --date-year-first
                            If short date is found, consider the first digits as
                            the year.
      -D, --date-day-first  If short date is found, consider the second digits as
                            the day.
      -L ALLOWED_LANGUAGES, --allowed-languages ALLOWED_LANGUAGES
                            Allowed language (can be used multiple times)
      -C ALLOWED_COUNTRIES, --allowed-countries ALLOWED_COUNTRIES
                            Allowed country (can be used multiple times)
      -E, --episode-prefer-number
                            Guess "serie.213.avi" as the episode 213. Without this
                            option, it will be guessed as season 2, episode 13
      -T EXPECTED_TITLE, --expected-title EXPECTED_TITLE
                            Expected title to parse (can be used multiple times)
      -G EXPECTED_GROUP, --expected-group EXPECTED_GROUP
                            Expected release group (can be used multiple times)

    Input:
      -f INPUT_FILE, --input-file INPUT_FILE
                            Read filenames from an input text file. File should
                            use UTF-8 charset.

    Output:
      -v, --verbose         Display debug output
      -P SHOW_PROPERTY, --show-property SHOW_PROPERTY
                            Display the value of a single property (title, series,
                            video_codec, year, ...)
      -a, --advanced        Display advanced information for filename guesses, as
                            json output
      -j, --json            Display information for filename guesses as json
                            output
      -y, --yaml            Display information for filename guesses as yaml
                            output

    Information:
      -p, --properties      Display properties that can be guessed.
      -V, --values          Display property values that can be guessed.
      --version             Display the guessit version.


It can also be used as a python module::

    >>> from guessit import guessit
    >>> guessit('Treme.1x03.Right.Place,.Wrong.Time.HDTV.XviD-NoTV.avi')  # doctest: +ALLOW_UNICODE
    MatchesDict([('title', 'Treme'), ('season', 1), ('episode', 3), ('episode_title', 'Right Place, Wrong Time'), ('format', 'HDTV'), ('video_codec', 'XviD'), ('release_group', 'NoTV'), ('container', 'avi'), ('mimetype', 'video/x-msvideo'), ('type', 'episode')])

``MatchesDict`` is a dict that keeps matches ordering.

Command line options can be given as dict or string to the second argument.

REST API
--------

A REST API will be available soon ...

Sources are available in a dedicated `guessit-rest repository <https://github.com/Toilal/guessit-rest>`_.

Support
-------

This project is hosted on `GitHub <https://github.com/guessit-io/guessit>`_. Feel free to open an issue if you think you
have found a bug or something is missing in guessit.

GuessIt relies on `Rebulk <https://github.com/Toilal/rebulk>`_ project for pattern and rules registration.

License
-------

GuessIt is licensed under the `LGPLv3 license <http://www.gnu.org/licenses/lgpl.html>`_.
