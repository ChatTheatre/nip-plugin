%META:TOPICINFO{author=\"kallea\" date=\"1151683791\" format=\"1.0\"
version=\"1.10\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPTodoStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>TODO: Relationships\</FONT\>

\<font class=\"query\"\>PROJECT STATUS\</font\> DEPRECATED

\<font class=\"query\"\>STATUS NOTES\</font\>

\<font color=\'indigo\'\>This system has been disbanded in favor of the
new relations system, which provides a more solid implementation for
this technology. Please see the related documentation for further
information.\</font\>

\<font class=\"query\"\>ASSIGNED CODER(S)\</font\>

  --------------- ---------- ----------------------------
  **Who**         **From**   **Contact information**
  Main.KalleAlm   Skotos     <kalle@marrach.skotos.net>
  --------------- ---------- ----------------------------

\<font class=\"query\"\>WHAT?\</font\> Individual/group relationships.

\<font class=\"query\"\>PRIORITY\</font\> HIGH

\<font class=\"query\"\>ETA?\</font\> End of August, 2003.

\<font class=\"query\"\>HOW WILL IT WORK?\</font\> Depending on the
settings, relations will improve or get worse depending on the actions
of those around the NPC. There will be a dynamic, customizable amount of
relation levels (\"loved\", \"trusted\", \"friend\", \"none\",
\"unfriend\", \"distrusted\", \"hated\" is one example) and upon that
there will be a numeric representation of where on the ladder a person
resides.

When the numeric relation reaches a certain level the actual relation
will be modified.

**EXAMPLE CHART**

  -------------- ----------------------- -----------------------
  **Relation**   **Level to decrease**   **Level to increase**
  loved          -600                    n/a
  trusted        -400                    6000
  friendly       -300                    3000
  none           -200                    2000
  unfriendly     -200                    2500
  distrusted     -200                    3000
  hated          -200                    4000
  -------------- ----------------------- -----------------------

Each time someone\'s level is modified, the numeric relation is reset to
0.

Thoughts: this system, while based off of the somewhat \'proven\' one
already residing in an animal NPC at Marrach, may be too static. I\'m
going to put some heavy thought into this and try to come up with a
number of different situations in which it would be used.

\<font class=\"query\"\>GENERAL DESCRIPTION\</font\>

The local farm-boy is infatuated with the lord\'s daughter. Sheesh,
what\'s she been up to, fluttering her eyelashes at him every chance she
gets. Oh, and did you hear that all the girls are crazy about Sir
Handsome. Unfortunately, he\'s got some issues now with every father in
the village\...

\<font class=\"query\"\>LIBRARIES\</font\>

    [Library]         [Description]
    relations         The general relations lib.

\<font class=\"query\"\>SIGNALS\</font\>

    [SIGNAL]            [Priority] [Description]
    RELATIONS         ~200       The relations signal.

\<font class=\"query\"\>HOOKS\</font\>

    [Hook]            [Using signals]             [Description]

\<font class=\"query\"\>TECHNICAL COMMENTS\</font\>

The system will only modify the relations towards the various characters
in the NPC\'s life. There is [a separate system](NIPTodoRelConBehavior)
in the making for relation-based behavior.

A tool to layout/define the NPC\'s behavior will be created for +NIP.

The relations system will be set up to use a predefined relations
database, which contains the configuration for the NPC\'s relations. It
is done this way because a lot of NPC\'s will use the same type of
system, and to save time, the configurations will be retrievable from a
secondary source.

A relations database is a simple propertycontainer with a few
properties. Example:

    relation:start            = "none"

    relation:type:loved     = ({ 20, 20, 16, 14, nil,            10000, "trusted",   -600,   40 })
    relation:type:trusted    = ({ 19, 18, 15, 13, "loved",      6000,  "friendly",  -400,    25 })
    relation:type:friendly  = ({ 16, 15, 13, 11, "trusted",  4000,  "none",      -250,   10 })
    relation:type:none       = ({ 14, 13, 11, 8,  "friendly",   2000,  "unfriendly", -200,   0 })
    relation:type:unfriendly = ({ 11, 10, 8,  6,  "none",        2500,  "distrusted", -200, -5 })
    relation:type:distrusted = ({ 9,  7,  5,  4,  "unfriendly", 3000,  "hated",     -200,   -20 })
    relation:type:hated     = ({ 7,  4,  3,  0,  "distrusted", 4000,  nil,           -20000, -45 })

The above may seem confusing at first, but isn\'t all that complicated.
\* The initial line (relation:start) specifies which relation is the
initial one that everyone starts out at. \* The next group of properties
map out the relations and specify the caps for each of them to improve
or degrade depending on the next batch of settings (described below);
within the ({ array }). The array content is defined as follows: \*
relation:type:RELATION = ({ R+ allow, T+ allow, R- allow, T- allow,
IMPROVE_NAME, IMPROVE_AT, DEGRADE_NAME, DEGRADE_AT, INITIAL_EFFECT })

-   **R+ allow:** This is the max strength of R+ allowed before the NPC
    regards the action as negative.
-   **T+ allow:** Same, for T+.
-   **R- allow:** This is the max strength of R- which the NPC accepts,
    before modifying its relationship towards a person.
-   **T- allow:** Same, for T-.
-   **IMPROVE_NAME:** is the name of the relation which this
    relationship would improve unto; if this is nil, there is no
    possible way to ascend beyond the specified relationship.
-   **IMPROVE_AT:** defines the amount of \"relation points\" required
    to ascend to the previously defined level.
-   **DEGRADE_NAME:** specifies the name of the relation which this
    relationship would degrade unto; if this is nil, there is no
    possible way to get a worse relationship.
-   **DEGRADE_AT:** defines the number of points below which a person
    will lose favor (i.e. descend into the aforementioned relationship).
-   **INITIAL_EFFECT:** determines how the NPC feels about a person to
    which he is thusly related, being in the room.

The next set of configurations will eventually be set up using a +NIP
tool, but their layout is defined here nonetheless. These properties
define what a person does to improve or degrade their relation points
with the NPC.

    relation:do:smile   = "r+5"
    relation:do:frown   = "r-4"
    relation:do:kiss     = "t+20"
    relation:do:kick     = "t-20"

Again, it might seem complicated but it\'s not. Briefly; \* \"r\" stands
for \"ranged\" \* \"t\" stands for \"touching\" \* \"+\" stands for
\"positive\" or \"improving\" \* \"-\" stands for \"negative\" or
\"degrading\"

Thus, \* \"r+\" stands for \"positive ranged\" \* \"r-\" stands for
\"negative ranged\" \* \"t+\" stands for \"positive touching\" \* \"t-\"
stands for \"negative touching\"

Examples for each are, \* \"smile\", \"grin\", \"wave\", \"bow\",
\"wink\" are all positive, ranged actions \-- \"r+\" \* \"frown\",
\"yell\", \"screech\", \"growl\", \"grunt\" are all negative, ranged
actions \-- \"r-\" \* \"kiss\"; \"hug\", \"caress\" are all positive,
touching actions \-- \"t+\" \* \"kick\", \"hit\", \"slap\", \"poke\" are
all negative, touching actions \-- \"t-\"

Now, a bunch of presumption goes on there. Someone could poke someone
fondly or slap someone playfully etc. and depending on the NPC\'s
nature, these all differ slightly. Some NPC\'s could enjoy a good tickle
while others would hate the same treatment. It also depends a lot on the
adverb used, which is the base of the next batch of properties:

    relation:as:smilingly = ({  0.1,  0.1, -0.1, -0.1, nil })
    relation:as:playfully = ({  0.1,  0.0, -0.2, -0.2, "reverse=-5" })
    relation:as:harshly = ({ -0.1, -0.1,  0.1,  0.3, "reverse=+5" })
    relation:as:hatefully = ({ -0.5, -0.5,  0.5,  0.5, "reverse=+10" })
    relation:as:lovingly  = ({  0.5,  0.5, -0.2, -0.2, "reverse=-6" })

Okay. To explain; the above defines how the NPC modifies the action
based on the adverb. So, frowning playfully will be different from
simply frowning. The ({ array }); \* The first entry defines how ranged
positive actions should be modified. In the first case (smilingly), they
would be strengthened by 10%. \* The second entry defines how touching
positive actions should be modified. Kiss (touching positive with
strength 20) smilingly (+10%) would have the strength 22 (20+10%). \*
The third entry defines how ranged negative actions should be modified.
\* The fourth entry defines how touching negative actions should be
modified. Kick (touching negative with strength 20) smilingly (-10%)
would get strength 18 (20-10%). \* The fifth, optional, entry defines
any modifier-flags. It needs to be explained further: \* The \"reverse\"
trigger turns positive into negative actions, and vice versa. \* The
reverse trigger is given a value (e.g. \"-5\") which determines;

-   Which type of action is reversed \-- + (positive), - (negative)
    or \* (both)
-   The maximum strength of that type of action required for the reverse
    to take effect. \* Thus, this: \<PRE\>relation:as:playfully = ({
    0.1, 0.0, -0.2, -0.2, \"reverse=-5\" })\</PRE\>will turn any
    negative actions into positive, if their strength is less than 5. \*
    And this: \<PRE\>relation:as:hatefully = ({ -0.5, -0.5, 0.5, 0.5,
    \"reverse=+10\" })\</PRE\>will turn any positive actions into
    negative, if their strength is less than 10.

Thus, we could frown (negative ranged, strength 4) playfully
(reverse=-5) at someone and the action would be interpreted as a
positive ranged, not a negative ranged. But if we kick (negative
touching, strength 20) playfully (reverse=-5) at someone, the action
would remain negative, as 20 is not less than 5.

The next set of options define details (body-parts) of the NPC which
affect the action. Using these settings, we can for instance say that
any touching actions, positive or negative, are regarded as negative if
the detail targeted is \"eye\" or \"eyes\";

    relation:detail:eye = "reverse=t+99"
    relation:detail:eyes  = "reverse=t+99"
    relation:detail:groin = "reverse=+99"

\* The first entry sets it up so that any touching, positive actions in
which the \'eye\' of the NPC is targeted, are reversed (made negative)
if the strength is less than 99 (which effectively means \'all\'). \*
The second entry does the same as the first, for the \'eyes\' detail. \*
The third entry reverses all positive actions (ranged or touching)
targeting the NPC\'s groin.

\<font class=\"query\"\>LIST OF INTERESTED PARTIES\</font\>

If this subject interests you, please add yourself to the list below.
The more interest, the higher priority a subject will get. And also, by
doing so, we will be able to notify you specifically when this
subject\'s status has changed.

    [Your Name]      [Your Email]
     RichardY            Richard_s_yale@hotmail.com
    [insert a separate line above this one]

\-- Main.KalleAlm - 10 Aug 2003

\<font class=\"query\"\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT
THIS SUBJECT\</font\>\<br\> (Please, don\'t forget to add your name to
your comment, preferably your TWiki-name.)
