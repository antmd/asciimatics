Troubleshooting
===============

256 colours not working
-----------------------
By default a lot of terminals will only support 8/16 colours.  Windows users
are limited to just these options for a native Windows console.  However other
systems can enable extra colours by picking a terminal that supports the
extended colour palettes.  For details of which terminals support additional
colours and how to enable them see `this Wikipedia article
<https://en.wikipedia.org/wiki/Comparison_of_terminal_emulators>`_.

In most cases, simply selecting a terminal type of ``xterm-256color`` will
usually do the trick these days.

.. _mouse-issues-ref:

Mouse support not working
-------------------------
Mouse support isn't fully enabled by default on all terminal types.  This will
often require some extra extensions to be enabled as described `here
<http://unix.stackexchange.com/questions/35021/how-to-configure-the-terminal
-so-that-a-mouse-click-will-move-the-cursor-to-the>`__.  In addition, if you
want 256 colours, you will need to mix modes as described `here
<http://stackoverflow.com/questions/29020638/which-term-to-use-to-have-both
-256-colors-and-mouse-move-events-in-python-curse>`__.

Although it is possible to get Linux terminals to report all mouse movement,
the reporting of mouse buttons along with movement appears to be highly
erratic.  The best reporting appears to be using the button event mode - i.e.
mixing ``xterm-1002`` with ``xterm-256color``.

Windows title does not change
-----------------------------
Much like mouse support, the commands to set the window title is not supported
on all terminal types.  Windows should work without any changes.  Other systems
may need to use a similar method as above to mix modes to add status line
support as described `here <https://gist.github.com/KevinGoodsell/744284>`_.

.. _ctrl-s-issues-ref:

Ctrl+S does not work
--------------------
In order to maintain legacy support for real terminal systems, most
terminals/consoles still support software flow control using Ctrl+S/Ctrl+Q.
You can switch this off on Linux by typing ``stty -ixon`` in your shell before
you start asciimatics as explained `here <http://unix.stackexchange.com/
questions/12107/how-to-unfreeze-after-accidentally-pressing-ctrl-s-in-a-
terminal>`__. Sadly, there is nothing that can be done on Windows to
prevent this as it is built in to the operating system, so you will never be
able to detect the Ctrl+S key.  See `here
<http://stackoverflow.com/questions/26436581/is-it-possible-to-disable-system-
console-xoff-xon-flow-control-processing-in-my>`__ for details.

I can't run it inside PyCharm
-----------------------------
Depending on which version you're using, you may see an Exception or simply
nothing (i.e. it looks like the program has hung).  The reason for this is
that the PyCharm Terminal/Console is not a true native terminal/console and
so the native interfaces used by asciimatics will not work.  There are 2
workarounds.

1. The simplest is just to run asciimatics inside a real terminal
   or window - i.e. not inside PyCharm.

2. If you must run inside PyCharm, the only option I've got working
   so far is the tests but even some of them need to skip where they
   cannot actually run.  To run from the IDE, you must start a real
   console from the Terminal window e.g. using `start cmd /c "python
   <your file name>"`.
