%META:TOPICINFO{author=\"kallea\" date=\"1116568320\" format=\"1.0\"
version=\"1.8\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPClassStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>CLASS: Recording and behavior - \[I - Making it
\"behave.\"\]\</font\>

\<font class=\"query\"\>AUDIENCE:\</font\> BEGINNERS

\<font class=\"query\"\>PREREQUISITE KNOWLEDGE:\</font\>

You need no knowledge prior to reading this class, except a basic
understanding on how the SkotOS works, with staff (+)-commands, etc.

\<font class=\"query\"\>SUMMARY:\</font\>

This class is divided into five chapters (this being the first). Each
chapter covers one fundamentally isolated part of the NIP record system.

\* Chapter I - Making it \"behave.\" \* [Chapter II -
Freemoting.](NIPClassRecordingII) \* [Chapter III - The scene
model.](NIPClassRecordingIII) \* [Chapter IV - Tracking and
replaying.](NIPClassRecordingIV) \* [Chapter V - The setting
model.](NIPClassRecordingV)

You are currently reading Chapter I - Making it \"behave.\" This chapter
is comprised of the following:

[]{.twiki-macro .TOC}

------------------------------------------------------------------------

## Introduction to behavior.

One of the major points of the NIP system is the flexibility and ease of
use regarding the concept of behavior. The NIP system divides behavior
into three classes: \* Parsing. \* Free-emoting. \* Pausing.

Parsing is the act of behaving through the usage of the internal game
parser. This is done by creating a set of complex properties which all
make up each possible parser action.

Free-emoting is the act of behaving through emitting text.

Pausing is the act of waiting. We will not cover pausing at all in this
chapter, so you can safely ignore this for now.

Behaving is a fundamental requirement for all living beings in a
text-based environment (it\'s not entirely as important for the dead -
like chairs and coffee cups). As such, it is important to understand the
behavior system structure.

The most logical thing to do would be to begin with the most basic form
of behavior. We won\'t do that, though, because the most logical form,
codewise, is not necessarily the most intuitive form to the user. As
such, we\'re going to begin with the parser-based recording. We will set
up, record into, and use something called a behavior data object (BDO).

------------------------------------------------------------------------

## Correcting invalidly recorded data.

Sometimes, you spot a typo or the action just doesn\'t come out right.
To remove it and (possibly) re-record it corrected, you use the \'\#\'
feature.

\* If you wish to remove this: `smile happily "!Hi tehre!"` you would
type: `say "#!"` \* To remove this: `say ">Kalle looks ahppy."` type:
`say "#>"`

Each time you invoke a \"\#\<type\>\" command, you remove the latest
entry of that type. You may do this multiple times to remove several
entries.

------------------------------------------------------------------------

## The +nip record tool.

Available to make things a little easier for us is the +nip tool.
Specifically, we\'re going to use +nip\'s \"record\" function to control
our recording session(s). Further on, we\'ll expand our usage of the
+nip tool a little, but for now, let\'s look at the usage for +nip
\"record\" (which is the most complex syntax of all +nip tools, thus
far):

`+nip "record [start|stop|switch] [<woename>] <i>PAGE</i>"`

Yes, that does look a little messy. Split it up into examples and it
makes a little more sense:

`1. +nip "record start Kalle:npc:behavior HAPPY"`

`2. +nip "record switch SAD"`

`3. +nip "record stop"`

Conclusively, the record tool is used to initiate and end recording
sessions. Recording sessions consist of three parts - receiver,
commander and session identifier. \* Receiver = the behavior data object
(BDO). \* Commander = the **possessed body** from which the +nip
\"record\" command was issued. \* Session identifier = also known as
\"MOOD\" or \"SITUATION\", this is the identifier which distinguishes
between multiple topics in the same BDO.

Each of these three parts are required in order to begin a recording
session. The +nip \"record switch\" function is used to switch between
session identifiers without switching the defined receiver.

There is one special session identifier that you should know about.
It\'s called \"DB,\" and it is used in place of almost all other
identifiers, if they are not present in the NPC. We\'re going to use the
\"DB\" identifier throughout the first part of this chapter.

------------------------------------------------------------------------

## Setting up a new behavior data object.

\<table align=\"center\" width=\"75%\" style=\"border: solid \#ff0000
1px;\"\>\<tr\>\<td\>\<font color=red\>Note:\</font\>\<br/\> Whichever
body you\'re currently possessing will serve as the commander throughout
this class. You should consistently use the same body throughout it,
however, and not jump between bodies unless necessary. Once you\'re a
bit more experienced with how recording works, you can do a little as
you wish, but do recall that recording session data is stored in **your
body**. To begin recording in another body, you\'d have to establish a
new recording session in that body.\</td\>\</tr\>\</table\>

1 The first thing we want to do is create a new property container,
which will serve as our BDO - the receiver. So we type:\<verbatim\>+cobj
propcontainer *Yourgame*:coders:*yourname*:myFirstBDO\</verbatim\> (In
my case, that would be
`+cobj propcontainer Mortalis:coders:kalle:myFirstBDO`.) 2 Secondly, we
need to establish a recording session by connecting our currently
possessed body with the property container we just
created:\<verbatim\>+nip \"record start
*Yourgame*:coders:*yourname*:myFirstBDO DB\"\</verbatim\>As you see, the
very last word in the command is `"DB"`. We are establishing a recording
session in our body, connecting ourselves with the property container.
Whenever we record, we will feed this through the `"DB"` session
identifier into the property container. (This sounds complex, but it\'s
as simple as it gets, and perfectly reasonable in due time. For now,
just nod and smile if you don\'t get it all immediately.)

Voila. We\'ve just set up and connected with a BDO. We\'re now ready to
begin the actual recording.

------------------------------------------------------------------------

## Recording syntax

If you start moving around, saying things, smiling, etc. you will notice
that there\'s little difference now than before you connected with the
BDO. This is because by default, the recorder will ignore all input,
unless you specifically request otherwise. If we wish for our NPC to
smile, at times, we would then do the following:

    \> smile
    You smile

*Nothing happens, because we need to request that the recorder records.*

    \> smile "!"
    You smile, "!"
    [STO:1]

Take note of the difference between the two smiles above. Only the
second smile, in which the user added an exclamation mark () as an evoke
to the parser, was there any type of indication that the recorder
noticed the action. The `[STO:1]` line specifically means, \"I stored a
regular parse - we now have 1 regular parses in total for this
session/BDO.\" As you continue recording, you will notice that the
number after `STO:` increments by one each time.

Evokes (spoken sentences) are added by beginning the sentence with an
exclamation mark (), and then continuing as usual.

    \> smile "I like soup!"
    You smile, "I like soup!"

*The above was not recorded. It did not begin with a !*

    \> smile "!I like soup!"
    You smile, "!I like soup!"
    [STO:2]

\<table align=\"center\" width=\"75%\" style=\"border: solid \#ff0000
1px;\"\>\<tr\>\<td\>\<font color=red\>Warning:\</font\>\<br/\> Presume
that you make a BDO for a shark, and use your regular humanoid body to
create the BDO data. The system is going to presume that you know what
you\'re doing when you assign BDO\'s to bodies, and will crash **hard**
when it tries to e.g. wiggle its arm, whilst possessing a quite arm-less
shark. Similarly, you will have little luck in trying to use any
non-humanoid details which a shark might possess (such as fins) unless
you possess a shark object while doing the recording. In general, it is
recommended that you possess the odd bodies before you record for
them.\</td\>\</tr\>\</table\>

------------------------------------------------------------------------

## Disabling the recorder.

The recorder should be disabled when we\'re done. If it\'s not, the
session is going to remain until we either 1) establish a new session to
another BDO (two sessions cannot exist simultaneously), or 2) we disable
the recorder.

To disable the recorder, we use the aforementioned +nip \"record stop\"
functionality.

    +nip "record stop"

------------------------------------------------------------------------

## Results.

Presuming you\'ve recorded a couple of parser moves, we\'re now going
ahead to configure our body as a nipper, using the
[emoting](NIPLibRefEmoting) library.

1 First off, we need to turn our regular woe object into a nipper
object. We do this through another +nip tool \-- \"set\".
Type:\<verbatim\>+nip \"set Woename\"\</verbatim\>- where Woename is the
woename for your object. (If you\'ve already got an NPC set up and just
want the configurative stuff, jump down to 4.) 2 Secondly, summon the
object unless it\'s in your environment already.\<verbatim\>+summon
*Woename*\</verbatim\> 3 Add the [emoting](NIPLibRefEmoting) library to
the NPC, unless the NPC is using it already.\<verbatim\>+setp \<nipper\>
\"add emoting\"\</verbatim\> 4 Now we need to tell the nipper that it
should use our new BDO when it acts. We do this simply by setting the
property `nip:behavior:db` in the nipper to the object reference for the
BDO itself, `<<i>Yourgame</i>:coders:<i>yourname</i>:myFirstBDO>`. Thus,
we type:\<verbatim\>+setp \<nipper\> \"nip:behavior:db
\<Mortalis:coders:kalle:myFirstBDO\>\"\</verbatim\> 5 For testing
purposes, we\'re going to temporarily set the emoting frequency to 1
(100/1 % chance).\<verbatim\>+setp \<nipper\>
\"nip:trait:emoting:frequency 1\"\</verbatim\> 6 Finally, we enable the
nipper and wait around a minute. It should start spamming us like crazy
with random selections from the recorded actions we performed a moment
ago.\<verbatim\>+nip \<nipper\> \"live\"\</verbatim\>

If you feel confident that things worked as they should, feel free to
ignore the \"Log start-finish\" section in each chapter, as it is mostly
there as a secondary demonstration of what we\'re doing.

------------------------------------------------------------------------

## Log start-finish.

At the end of each chapter, there is a log describing the (visible)
actions that we did, in order.

    ---
    <b>> +cobj propcontainer Kalle:myFirstBDO</b>
    Done!
    <b>> +nip "record start Kalle:myFirstBDO DB</b>
    Begun recording for mood/condition 'DB' in &lt;Kalle:thug-rabbit>. When you are done, type: +nip "record stop"
    <b>> smile</b>
    You smile.
    <b>> smile "!</b>
    You smile, "!"
    [STO:1]
    <b>> smile "I like soup!</b>
    You smile, "I like soup!"
    <b>> smile "!I like soup!</b>
    You smile, "!I like soup!"
    [STO:2]
    <b>> +nip "record stop</b>
    Stopped recording in &lt;Kalle:thug-rabbit>.
    <b>> +obname me</b>
    &lt;Kalle:thug-rabbit>; detail "default"
    <b>> +nip "set Kalle:thug-rabbit</b>
    WELCOME TO THE 'NIP' CNPC SYSTEM!

    Hold one moment while the core library is set up in &lt;Kalle:thug-rabbit> ...
    --> Implementing base.
    --> Adding base libraries.
    [cut]
    --> Inserting system signals.
    [cut]
    --> Setting revision according to current system state.
    Done!
    <b>> +setp me "add emoting</b>
    Setting 'add' in <Kalle:thug-rabbit> to "emoting".
    [cut]
    The 'emoting' library/hook has been loaded. Before your NPC will react, however, you must use (and make, if you haven't already) a behavior database.
    &lt;Lib:NIP:lib:emoting> loaded successfully.
    <b>> +setp me "nip:behavior:db &lt;Kalle:myFirstBDO></b>
    Setting 'nip:behavior:db' in &lt;Kalle:thug-rabbit> to &lt;Kalle:myFirstBDO>.
    <b>> +setp me "nip:trait:emoting:frequency 1</b>
    Setting 'nip:trait:emoting:frequency' in &lt;Kalle:thug-rabbit> to 1.
    <b>> +nip me "live</b>
    [live] -> a violent looking trash-bunny
    NIP HEARTBEAT thread starting up...
    Scanning for updates ...
    Update Target = Kalle:thug-rabbit
    ... updates finished.
    Calculating sighook-path ...
    Connecting with NCS ...
    ... connected.
    Heartbeat loop starting now. "My name is 001, how do you do?"
    In a couple of minutes I'm going to hand you some stats on how this thread is doing.
    <b>> +possess kalle</b>

    You inhabit Kalle.
    A violent looking trash-bunny smiles.
    A violent looking trash-bunny smiles.
    A violent looking trash-bunny smiles, "I like soup!"
    A violent looking trash-bunny smiles.
    A violent looking trash-bunny smiles, "I like soup!"
    <b>> +nip bunny "die</b>
    [term] -> a violent looking trash-bunny
    ---

------------------------------------------------------------------------

## Post summary.

In this chapter, we examined the following aspects of the NIP record
tool:

\* The concept of \'behavior\'. \* +nip \"record\" tool - how to start
and stop recording. \* BDO\'s (behavior data object) \* Parser recording
syntax

To read about freemoting, [proceed to Chapter II](NIPClassRecordingII).
Alternatively, you may jump to either of the other chapters:

\* [Chapter II - Freemoting.](NIPClassRecordingII) \* [Chapter III - The
scene model.](NIPClassRecordingIII) \* [Chapter IV - Tracking and
replaying.](NIPClassRecordingIV) \* [Chapter V - The setting
model.](NIPClassRecordingV)

To read more about recording behavior, read the [how to on the
topic.](NIPHowRecord)

\-- Main.KalleAlm - 21 May 2004

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
CLASS\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
