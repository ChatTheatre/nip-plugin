%META:TOPICINFO{author=\"kallea\" date=\"1084984610\" format=\"1.0\"
version=\"1.7\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPTodoStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>TODO: Fighting\</FONT\>

\<font class=\"query\"\>PROJECT STATUS\</font\> COMPLETED

\<font class=\"query\"\>STATUS NOTES\</font\>

This system is in-place, pending sync to S7 and Stages.

\<font class=\"query\"\>ASSIGNED CODER(S)\</font\>

  --------------- ---------- -----------------------------
  **Who**         **From**   **Contact information**
  Main.KalleAlm   Skotos     <kalle@mortalis.skotos.net>
  --------------- ---------- -----------------------------

\<font class=\"query\"\>WHAT?\</font\> A generic fighting system, with
add-on \"modules\" for fighting systems.

\<font class=\"query\"\>PRIORITY\</font\> HIGH

\<font class=\"query\"\>ETA?\</font\> Completed May 9th, 2004.

\<font class=\"query\"\>HOW WILL IT WORK?\</font\>

The initial system will simply use three maps - one with imperatives, a
second with condition regards and a third with min-max delay to wait
after the imperative. Example of an imperative map, for Marrach\'s
duelling, would be:

    ([ "rest"    : ([ "guard"   : 80, 
                            "cut"     : 15,
                            "feint" : 5 ]),
        "guard" : ([ "jab"    : 18,
                            "cut"     : 18,
                            "feint" : 9,
                            "dodge" : 9,
                            "rest"   : 18,
                            "slip"   : 9,
                            "lunge" : 9,
                            "advance" : 5,
                            "retire"  : 5 ]),
        "cut"     : ([ "rest"    : 18,
                            "jab"     : 18,
                            "cut"     : 18,
                            "feint" : 9,
                            "dodge" : 9,
                            "slip"   : 9,
                            "lunge" : 9,
                            "advance" : 5,
                            "retire"  : 5 ]),
        "feint" : ([ "rest"  : 18,
                            "jab"     : 18,
                            "cut"     : 18,
                            "feint" : 9,
                            "dodge" : 9,
                            "slip"   : 9,
                            "lunge" : 9,
                            "advance" : 5,
                            "retire"  : 5 ]),
        "jab"     : ([ "guard"  : 38,
                            "jab"     : 18,
                            "cut"     : 18,
                            "rest"   : 14,
                            "feint" : 4,
                            "advance" : 4,
                            "retire"  : 4 ]),
        "dodge" : ([ "jab"    : 30,
                            "cut"     : 30,
                            "feint" : 20,
                            "rest"   : 10,
                            "guard" : 10 ]),
        "slip"   : ([ "guard"   : 38,
                            "jab"     : 18,
                            "cut"     : 18,
                            "rest"   : 5,
                            "guard" : 15,
                            "advance" : 3,
                            "retire"  : 3 ]),
        "lunge" : ([ "rest"  : 20,
                            "jab"     : 20,
                            "cut"     : 20,
                            "feint" : 10,
                            "dodge" : 10,
                            "slip"   : 10,
                            "lunge" : 10 ]),
        "advance" : ([ "guard"  : 60,
                            "cut"     : 20,
                            "feint" : 10,
                            "rest"   : 10 ]),
        "retire"  : ([ "guard"  : 60,
                            "cut"     : 20,
                            "feint" : 10,
                            "rest"   : 10 ]) ])

The above map is the imperative map. It is used to determine 1) which
commands are valid following the previous command, and 2) how likely
each action is, in percent. Each map points to a map of imperatives,
where the values all sum up to 100 (%).

The next map maps numeric properties in the NIP, and converts these into
bonuses in the decision-making. The full syntax of this map is as
follows:\<pre\>(\[ \"NIP property\" : ({ middle, effect, positive-bonus,
negative-bonus }) \])\</pre\>

Example:

    ([ "duelling:fatigue" : ({ 50, 0.2, ({ "cut", "jab", "feint" }), "rest" }) ])

In the above example, the following rules apply for the
\"duelling:fatigue\" property: \* The middle is 50. This means a fatigue
of 85 will become a bonus value of 35. A fatigue of 20 will become -30.
\* The effect is 0.2 (20%). This means the final bonus for a bonus value
of, say, 20, will be 4. \* The positive-bonus is ({ \"cut\", \"jab\",
\"feint\" }). This means these three imperatives will receive the bonus
**if the bonus value is a positive number**. \* The negative-bonus is
\"rest\". This means the \"rest\" imperative will receive the bonus, if
the bonus value is **a negative number**.

A single property can have multiple entries. These would simply be
listed in a linear row, e.g. ({ 50, 0.2, ({ \"cut\", \"jab\", \"feint\"
}), \"rest\", 20, 0.1, ({ \"dodge\", \"slip\" }), nil }) \]).

The final map is the delay map. This maps all the available imperatives
with a minimum and a maximum delay value. This is used to determine the
speed of the nipper, but also serves to ensure the nipper do not act
\"too fast\", ever. (if they do, long pauses in between actions will
occur where the nipper receive \"You are too busy with something else.\"
errors).

The syntax of this map is:\<pre\>(\[ \"imperative\" : ({ min, max })
\])\</pre\>

    ([ "rest"    : ({ 0.1, 0.3 }),
        "guard" : ({ 0.5, 4.0 }),
        "cut"     : ({ 2.1, 3.0 }),
        "feint" : ({ 2.1, 3.0 }),
        "jab"     : ({ 2.1, 2.5 }),
        "dodge" : ({ 1.1, 2.0 }),
        "slip"   : ({ 4.0, 6.0 }),
        "lunge" : ({ 3.5, 5.5 }),
        "advance" : ({ 0.5, 1.0 }),
        "retire"  : ({ 0.5, 1.0 }) ])

In the above, if the nipper would decide to perform a jab, then the next
action would occur between 2.1 and 2.5 seconds later.

Apart from the above maps, the system will include a few scripts. \*
**merry:lib:core_fight_init** - Initialize a fight. This is called in
the nipper to initialize the fight thread (external from the heartbeat
thread as it has to work in its separate speed), with the argument
\$opponent set to the object reference of the opponent. \*
**merry:lib:core_fight_end** - Called at the end of the fight.

In any combat system, the nipper needs at least two external functions,
one that determines when a fight has begun, and another which determines
when the fight is over.

In CM, the initiating of a fight is simple enough. A
merry:react:duel-whom which triggers the duel.

The ending of a fight is equally simple. When a duel ends, each
participant performs the action signal \"combat/stop\". Thus, we can
determine when a fight has ended by adding a merry:act:combat/stop to
the nipper.

\<font class=\"query\"\>GENERAL DESCRIPTION\</font\>

Fighting NPC\'s has got to be the most commonly occuring thing in the
universe, next to blonde swedish gals. Any computer game out there with
an \'action\' label on it (and the majority of those that don\'t) has
them in some shape or form. Hopefully, this system will turn out an easy
implementation without too much tweaking A.I. values.

\<font class=\"query\"\>LIBRARIES\</font\>

    [Library]         [Description]
    fighting            The general fighting lib

\<font class=\"query\"\>TECHNICAL COMMENTS\</font\>

The previous technical comments here are discarded in favor of the
general comments in the \"how will it work\" section above.

\<font class=\"query\"\>LIST OF INTERESTED PARTIES\</font\>

If this subject interests you, please add yourself to the list below.
The more interest, the higher priority a subject will get. And also, by
doing so, we will be able to notify you specifically when this
subject\'s status has changed.

    [Your Name]      [Your Email]
    TonySmith           Disdercardo@blueyonder.co.uk

    [insert a separate line above this one]

\-- Main.KalleAlm - 02 Jun 2003

\<font class=\"query\"\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT
THIS SUBJECT\</font\>\<br\> (Please, don\'t forget to add your name to
your comment, preferably your TWiki-name.)
