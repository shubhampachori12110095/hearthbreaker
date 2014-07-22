Hearthstone Simulator
=====================

The purpose of this project is to create an open source Hearthstone simulator for the purposes of machine learning and
data mining of Blizzard's [Hearthstone: Heroes of WarCraft](http://battle.net/hearthstone).  The end goal
is to create a system implementing every card in Hearthstone, then simulate games of bots against bots to train
them.  The results from these games can be used to determine cards which work well together and cards which do not.
The goal is not to create a clone of Hearthstone which players can use to replace the game itself with.

 * Documentation (In Progress) [http://danielyule.github.io/hearthstone-simulator/](http://danielyule.github.io/hearthstone-simulator/)
 * Travis CI Build Status: [![Build Status](https://travis-ci.org/danielyule/hearthstone-simulator.svg?branch=master)](https://travis-ci.org/danielyule/hearthstone-simulator)
 * Coveralls Code Coverage: [![Coverage Status](https://coveralls.io/repos/danielyule/hearthstone-simulator/badge.png?branch=master)](https://coveralls.io/r/danielyule/hearthstone-simulator?branch=master)
 * Developer Mailing List: [Google Group](https://groups.google.com/forum/#!forum/hearthstone-simulator-dev)

Usage
-----
###Console Application
There is a basic console that you can use for playing against a bot.  The bot you are playing against will not
attack you, and will play one card from its hand per turn. (So it is very easy to beat)

Start the console with ``python hsgame/ui/text_runner.py deck1.hsdeck deck2.hsdeck``.  The two deck files are
text files with the name of the class followed by a comma, followed by the names of each of the cards in the deck
in English.

The console application requires ncurses, which should be included with python on *nix and mac systems, but if you are 
on windows, you must download it from 
[http://www.lfd.uci.edu/~gohlke/pythonlibs/#curses](http://www.lfd.uci.edu/~gohlke/pythonlibs/#curses)


###Unit Tests
The tests are located in the [`tests`](tests) package.

All tests can be run with the following command: `python -m unittest discover -s tests -p *_tests.py`

The Hearthstone Simulator is compatible with [Python](https://www.python.org/) 3.2+ and [PyPy3](http://pypy.org/) 2.3+

For Python 3.2 and PyPy3, the unit tests are dependent on the [mock package](https://pypi.python.org/pypi/mock).

Progress
--------

Currently, the main engine is mostly implemented, along with all the non Naxxramas cards.  [cards.csv](cards.csv) is a listing of all cards in the
game along with information on which has been implemented.  Any card which has been implemented also has at least one
unit test to ensure that it works correctly

Structure
---------
Almost all of the game logic is found in [hsgame.game_objects](hsgame/game_objects.py).  The game functions largely on an event based system.
The events use a bind/trigger mechanism.  For example, a card which has a deathrattle will bind an event to its 'death'
event that takes the appropriate action.  Parameters can be passed to an event at the time it is bound, or the time it
is triggered, or both.  For an overview of the events and the parameters they receive, see [events.md](events.md).

The cards themselves are each a class, and can be found in the [hsgame/cards](hsgame/cards) directory, organized by type
(spell/minion/secret/weapon) and by class.  To see which cards have been implemented, simply search for "yes".

This project also includes a replay facility, which allows for games to be recorded and played back.  The format for
the replay syntax is documented in [replay_format.md](replay_format.md).

Contributing
------------

To contribute, simply fork the repository, make changes and submit a pull request.

All pull requests which implement new cards must also include a unit test for those cards.  In the case where the card
 has no side effects aside from playing the minion, tests should include another card's effects on it.

All pull requests will be automatically verified through 
[travis-ci.org](https://travis-ci.org/danielyule/hearthstone-simulator), and a coverage report generated through
 [coveralls.io](https://coveralls.io/r/danielyule/hearthstone-simulator)

For more specifics about contributing, see the 
[contributing page](http://danielyule.github.io/hearthstone-simulator/contributing.html), 
or join the [Developer Mailing List](https://groups.google.com/forum/#!forum/hearthstone-simulator-dev)

Related Projects
----------------
Hiroaki Oyaizu has created [HearthSim](https://github.com/oyachai/HearthSim), another Hearthstone simulator, written in Java
with a stronger focus on efficiency and AI modelling. It currently has fewer cards implemented, but has a much more
sophisticated AI.

_Hearthstone: Heroes of WarCraft_ and _Blizzard_ are trademarks of Blizzard Entertainment.
