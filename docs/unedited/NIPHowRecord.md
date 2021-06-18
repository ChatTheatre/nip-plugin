%META:TOPICINFO{author=\"kallea\" date=\"1084988806\" format=\"1.0\"
version=\"1.6\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>How to record a behavior
database?\</FONT\>\<br\> *Also known as \"Proper Usage Of The Virtual
Cam\"*

**First off,** what is a behavior db?\<BR\> Simply put, it\'s an object
containing a set of very complex properties which, interpreted by the
system, makes it possible for the NPC to \"act out\" pre-made parser
moves (\'A parrot smiles adoringly at you, \"Hi there schweetie\"\').

**So, how do I make one?**

\* First make sure you have added the emoting library to the npc -
`+setp npc "add emoting"` \* Create a propcontainer
(`+cobj propcontainer`) and give it an appropriate name, which
preferably (but not necessarily) go by the naming convention
\<Theatre\>:<Data:NIP:behavior:%3Ctopic>\>. \* Execute from the parser,
`+nip 'record start <i>WOENAME</i> DB'` \* *WOENAME* = the woename for
your aforementioned property container. \* *DB* = the name of the record
\"mood/situation\". DB is an alias for \"everything.\"

(At this point, you have begun recording. Note that it doesn\'t matter
if you record FROM your own or any other body. The data is stored in the
object, not in your own body. However, if your NPC is missing limbs, so
to say, or if it has extra details (wings, fur, tail, etc.) it is
certainly recommended that you +possess the NPC before you start
recording.)

\* Begin by using the parser to act as the NPC would do. To actually
record, however, your evoke must begin with an exclamation mark ().

E.g.

    ---
    > smile happily "!
    [STO:1]
    You smile happily, "!"

    > grin thoughtfully "!
    [STO:2]
    You grin thoughtfully, "!"

    > glance contemplatively "!I like muffins!"
    [STO:3]
    You glance contemplatively, "I like muffins!"

    > bounce around here ecstatically "!
    [STO:4]
    You bounce around StoryCoder Kalle's laboratory ecstatically, "!"
    ---

When you\'re done recording, disable recording by typing
`+nip "record stop"`

To specify that the NPC should use your newly created behavior database,
you need to: `+setp <NPC> "nip:behavior:db <Woe:for:your:new:db>"`

**Take special note**: the above is for moodless NPC\'s. If you wish to
record for NPC\'s with varying moods, you may use the above method to
create a default behavior (for when there is no mood-specific data
stored). For each mood which behavior you wish to define, you must call
the `+nip "record start Woe:name MOOD"` command, where Woe:name is the
woename for the behavior db (<Data:NIP:behavior>:\...) and MOOD is the
name of the mood in question.

E.g. if you have an NPC with the moods HAPPY and HUNGRY, you could do
something like this:

    ---
    > +nip "record start Data:NIP:behavior:my_db HAPPY"
    Begun recording for mood 'HAPPY' in &lt;Marrach:players:K:kalle>.
    > smile happily, "!I'm happy!"
    [STO:1]
    You smile happily, "!I'm happy!"

    > bounce gleefully, "!Wee!"
    [STO:2]
    You bounce gleefully, "!Wee!"

    > +nip "record switch HUNGRY"
    Begun recording for mood 'HUNGRY' in &lt;Marrach:players:K:kalle>.
    > gaze hungrily "!"
    [STO:1]
    You gaze hungrily, "!"

    > peer silently at here "!
    [STO:2]
    You peer silently at StoryCoder Kalle's laboratory.

    > whine sadl "!I'm hungry!"
    [STO:3]
    You whine sadly, "!I'm hungry!"

    > +nip "record switch DB"
    Begun recording for mood 'DB' in &lt;Marrach:players:K:kalle>.
    > nod coolly "!
    [STO:1]
    You nod coolly, "!"

    > +nip "record stop"
    ---

You do not need a separate database object for each mood. All moods may
reside in the same db. In the above case, we use the +nip \"record
switch\" function, which switches between moods in the same object,
automatically.

\<table style=\"border: solid \#000000 1px;\"\> \<tr\>\<td
colspan=\"4\"\>\<center\>**Special
record-characters**\</center\>\</td\>\</tr\>
\<tr\>\<td\>**Char**\</td\>\<td\>**Indicator**\</td\>\<td\>**Example**\</td\>\<td\>**Result**\</td\>\</tr\>
\<tr\>\<td\>\</td\>\<td\>Record parser action.\</td\>\<td\>smile happily
\"\"\</td\>\<td\>\<NPC\> smiles happily.\</td\>\</tr\>
\<tr\>\<td\>\>\</td\>\<td\>Freemote record.\</td\>\<td\>say \"\>The
ground shakes violently.\"\</td\>\<td\>The ground shakes
violently.\</td\>\</tr\> \<tr\>\<td\>@\</td\>\<td\>Record delay
(pause).\</td\>\<td\>say \"\@2.5\"\</td\>\<td\>\<2.5 second
pause\>\</td\>\</tr\> \</table\>

The delay char (@) is only applicable in tracked recordings. Tracked
recordings are like regular recordings with a side-vector which tracks
the order in which each command is recorded. Tracked recordings can then
be replayed in full by the emoting parser through callback by the user.

More information on the topic of tracked recordings will appear soon.

\-- Main.KalleAlm - 19 May 2004
