%META:TOPICINFO{author=\"kallea\" date=\"1122866217\" format=\"1.0\"
version=\"1.4\"}% %META:TOPICPARENT{name=\"NIPClassRecordingII\"}%
[NIPClassStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>CLASS: Recording and behavior - \[III - The
scene model.\]\</font\>

\<font class=\"query\"\>AUDIENCE:\</font\> EXPERIENCED

\<font class=\"query\"\>PREREQUISITE KNOWLEDGE:\</font\>

\* You should be somewhat familiar with the +nip tool, especially the
\"record\" function. \* You should know what a BDO is. \* You should
know the basic concept of recording behavior data - parser recording,
freemote recording, or both. \* You should know the basics of Merry, and
what a react-script is.

\<font class=\"query\"\>SUMMARY:\</font\>

In this chapter we\'re going to cover the concept of scene models, how
you can make use of scene models in your NPC\'s and the various
techniques and tools there are available to make this process as
efficient and easy as possible.

This chapter comprises of: []{.twiki-macro .TOC}

------------------------------------------------------------------------

## Introduction to scene models.

When behavior data is recorded, the recording system does not presume a
lot. For instance, it won\'t presume that a pair of fluffy, pink mittens
are going to be in your hands, always, even if they\'re there at the
time of recording.

Thus, you cannot target your fluffy, pink mittens at all, when you
record. In fact, if you try, the system will respond, \<verbatim\>
Action ignored as only own details and \'here\' are accepted targets. If
you have set up a scene, the targets defined there may be used as well
but Kalle\'s pair of fluffy, pink mittens was not listed if
so.\</verbatim\>

The recording system allows you to target two things. \* Details of your
own body. The recording tool presumes that any details in your body that
you target will be present in the body of all NPC\'s which will use the
resulting BDO. \* \"Here\", the room you\'re in. This will be
substituted with whatever room the NPC is in when it evaluates any
behavior data in which the room is targeted. However, no details in the
room other than the room itself may be targeted.

Most of the time, this is enough. It may be limiting, but in all
honesty, unless we have a particular situation, we don\'t need more than
our own details and the room we\'re in. Of course, we might have clothes
and such in our inventory, but that\'s admittedly a small issue.

In some cases, you record into a BDO for a particular reason. An example
is a guard stopping a character from entering a room, because the
character is not allowed to enter. In this example, we need to be able
to target more than just \"here\" and \"ourselves\". In this case, we
have what is called an **external entity** - the character.

In order for our guard to be able to target the character when we
record, we need to set up a scene. A scene is any number of objects -
scene actors - which each have a symbolic identifier. These symbolic
identifiers are stored when we interact with the scene actors. Later on,
when we wish to replay the recorded behavior, each symbolic identifier
will be available to use in run-time as \$(identifier).

`<i>Figure 3-1</i>`\<br/\> \<img
src=\"%ATTACHURLPATH%/bdoscenemodel.png\" alt=\"bdoscenemodel.png\"/\>

In figure 3-1, we have four objects. \* The BDO (\*), \* the
environment, \* and two scene actors (\~) - \"Lefty\" and \"Righty.\"

If we say that \"Lefty\" is the guard, and \"Righty\" is the person
trying to enter the room, we have ourselves a scene. \"Lefty\" and
\"Righty\" are, of course, silly symbolic identifiers. We would most
likely give the character which is attempting to enter the symbolic
identifier \"victim\", \"person\" or perhaps \"actor\". Since we\'re
recording exclusively from the guard\'s perspective, the guard won\'t
have a symbolic identifier at all. (We will look into when and why we
would give the acting entity a symbolic identifier in chapter IV.)

------------------------------------------------------------------------

\<table align=\"center\" width=\"75%\" style=\"border: solid \#ff0000
1px;\"\>\<tr\>\<td\>\<font color=red\>Note:\</font\>\<br/\> Whilst
recording, it is important to remember that the conditions of the
recording session differs from the conditions in which the recorded data
will be used. For instance, if you\'re recording data for a tiger NPC in
your coder office, the conditions and surroundings will assuredly differ
from the environment in which the tiger will eventually **make use** of
the recorded data. For example a jungle.

As such, when you\'re setting up scenes, remember that the objects you
use as scene actors do not matter. What does matter is the symbolic
identifier each of these receive. You could be using your office desk or
a fellow staffer as for instace prey in a \"predator and prey\" scene
recording. \</td\>\</tr\>\</table\>

## The +nip scene tool.

To assign a scene role to an object, you would use the +nip \"scene\"
tool. It\'s fairly straightforward.\<verbatim\>+nip \<nipper\> \"scene
\<symbolic identifier\>\"\</verbatim\>to set a role,\<verbatim\>+nip
\<nipper\> \"scene -\"\</verbatim\>to remove a particular actor from the
scene, and\<verbatim\>+nip \"scene \--\"\</verbatim\>to delete a scene
completely (or rather - the scene actor information).

------------------------------------------------------------------------

## An example.

Why go through this trouble, then? What\'s the point? Let\'s look at a
brief example:

    ---
    <b>> smile at bunny "!</b>
    You smile at a violent looking trash-bunny, "!"
    Action ignored as only own details and 'here' are accepted targets. If you have set up a scene, the 
    targets defined there may be used as well but a violent looking trash-bunny was not listed if so.
    <b>> +nip bunny "scene bunny</b>
    Scene role (bunny) set to a violent looking trash-bunny.
    <b>> smile at bunny "!</b>
    You smile at a violent looking trash-bunny, "!"
    [STO:3]
    ---

In the BDO, if we examine the **db:obj** property, it will look
something like this:\<verbatim\> ({ nil, nil, ({ ({ \"(bunny)\" }) })
})\</verbatim\>

I gave the violent-looking trash-bunny the symbolic identifier \"bunny\"
in my scene. As you see in the property above, when I smiled at the
violent-looking trash-bunny, it resolved into the BDO as `"(bunny)"`.
When this BDO is interpreted by the NIP parser at run-time, it will
transform `(bunny)` into the object reference hopefully found in the
Merry variable `$bunny`. (If this does not make perfect sense so far,
that\'s OK. We\'ll get back to what this means further down.)

------------------------------------------------------------------------

## Live scene examples.

This all looks really good in theory, but does it work in practice? And
the various uses of this may or may not be too clear at this point.
Using a scene, you are allowed to target more than just \"here\" and
\"yourself.\" Then, what? How will you let the NPC know what this new
scene role should be pointing at?

One example is the [marrach-guards](NIPLibRefMarrachGuards) library.
This is a library specifically for the Castle Marrach game, where the
guard performs various checks to see if a person has precedence enough
to enter a particular room. Furthermore, the system will use a BDO which
has four pages (conditions/moods) - \"REFUSE-LOW\", \"REFUSE-HIGH\",
\"ALLOW-LOW\" and \"ALLOW-HIGH\".

The two LOW pages will be used when a low-ranked person is refused or
allowed entry. The two HIGH pages will be used when a high-ranked person
is refused or allowed entry.

The [guarding](NIPLibRefGuarding) library will call the
\"request-authority\" script found in
[marrach-guards](NIPLibRefMarrachGuards), feeding it three arguments. \*
\$who - the person trying to enter. \* \$what - what the person is
trying to do (enter). \* \$where - the NRef pointer to the exit.

If you\'ve followed me thus far, things should be dawning right about
now. The library which handles the guard duties sets a number of
\$variables \-- \$variables can be used as object pointers to scene
actors by giving an object a symbolic identifier equal to the variable
name. What, then, if we initiate a recording session using the above
conditions, and include a scene actor with the symbolic identifier
\"who\"? Any actions we performed toward the corresponding object would
be automatically resolved and used by the guard, on the fly. If we add a
scene actor with the role \$where, we will be able to target the
attempted exit as well.

------------------------------------------------------------------------

## Doing it ourselves.

In order to comprehend this entirely, we\'re going to create a tiny
script in our NPC. This script will in turn trigger a BDO call, using
symbolic identifiers. Before we do this, however, we\'re going to set up
a new scene.

Let us for a moment imagine that we\'re in the shoes of whatever NPC
we\'ve made (in my case, a bunny). Let us also imagine that someone,
anyone, just yelled something at us. How would we react to this? In
order to be able to react appropriately, we\'re going to set up the
scene.

Clear whatever current scene you have, if any,\<verbatim\>+nip \"scene
\--\"\</verbatim\>

Locate an appropriate object in the room that will serve as the scene
actor. In my case, I\'m going to target Lucy, who simply happens to be
in the room with me at the moment. The symbolic identifier we\'ll be
using for this target we name \"yeller.\" \<verbatim\>+nip \<object\>
\"scene yeller\"\</verbatim\>

We need to enable recording, but before we do that, remember that
you\'ve been using the `"DB"` page throughout the examples? Well, we
won\'t use `"DB"` here. Instead, we\'re calling this `"myScene"`. The
rest is as it\'s always been.\<verbatim\>+nip \"record start
*Yourgame*:coders:*yourname*:myFirstBDO myScene\"\</verbatim\>

We\'re ready to record some \"reactions\" for someone yelling at us.
Remember that these recorded actions are in no way used in chronological
order. They\'re in fact fetched and used at random, so two subsequent
actions are practically impossible to record, as they will most likely
be used out of order.

    ---
    <b>> growl at lucy annoyed "!Shut it.</b>
    You growl at Lucy annoyedly, "!Shut it."
    [STO:1]
    <b>> grunt at lucy "!</b>
    You grunt at Lucy, "!"
    [STO:2]
    <b>> yell at lucy responsive "!LALALALALALA!!!!!</b>
    You yell at Lucy responsively, "!LALALALALALA!!!!!"
    [STO:3]
    ---

Stop recording (`+nip "record stop"`) and prepare yourself to write one
line of Merry code.

We\'re going to make the script \"react-post:yell-iob\" in the NPC body
directly. We won\'t bother making libraries etc. for this.

    > +to me ed %woename-for-your-nipper react-post:yell-iob

In the text box, type in:\<verbatim\> Call( this,
\"handler:emoting:parse\", \$db: this.\"nip:behavior:db\", \$mood:
\"myScene\", \$yeller: \$actor );\</verbatim\>and hit Submit CHANGES.

Presuming that went well, we\'re ready to test our little experiment.

    ---
    <b>> yell at bunny</b>
    You yell at a violent-looking trash-bunny.
    A violent looking trash-bunny grunts at you.
    <b>> yell at bunny</b>
    You yell at a violent looking trash-bunny.
    A violent looking trash-bunny grunts at you.
    <b>> yell at bunny</b>
    You yell at a violent looking trash-bunny.
    A violent looking trash-bunny yells at you responsively, "LALALALALALA!!!!!"
    <b>> rub my ear</b>
    You rub your small right ear.
    ---

\<table align=\"center\" width=\"75%\" style=\"border: solid \#ff0000
1px;\"\>\<tr\>\<td\>\<font color=red\>Warning:\</font\>\<br/\> I might
tell you right off the bat that writing a bunch of react-scripts with
corresponding behavior data is a bad idea. The above only serves as an
example and would be an insane way to implement behavior for an NPC. But
hopefully, it might give you a hint as to how scene models work and why
they\'re useful. \</td\>\</tr\>\</table\>

If you feel confident in your knowledge about scene models, jump down to
\"Post summary\".

------------------------------------------------------------------------

## Log start-finish.

    ---
    <b>> +nip "scene --"</b>
    Scene deleted.
    <b>> +nip lucy "scene yeller</b>
    Scene role (yeller) set to Lucy.
    <b>> +nip "record start Kalle:myFirstBDO myScene</b>
    Begun recording for mood/condition 'myScene' in <Marrach:players:K:kalle>. When you are done, type: +nip "record stop"
    <b>> growl at lucy annoyedly "!Shut it.</b>
    You growl at Lucy annoyedly, "!Shut it."
    [STO:1]
    <b>> grunt at lucy "!</b>
    You grunt at Lucy, "!"
    [STO:2]
    <b>> yell at lucy responsive "!LALALALALALA!!!!!</b>
    You yell at Lucy responsively, "!LALALALALALA!!!!!"
    [STO:3]
    <b>> +nip "record stop</b>
    Stopped recording in <Marrach:players:K:kalle>.
    <b>> +obname bunny</b>
    &lt;Kalle:thug-rabbit&gt;; detail "default"
    <b>> +to me ed %Kalle:thug-rabbit react-post:yell-iob</b>
    Editing source in popup window.
    <b>> yell at bunny</b>
    You yell at a violent looking trash-bunny.
    A violent looking trash-bunny yells at you responsively, "LALALALALALA!!!!!"
    ---

------------------------------------------------------------------------

## Post summary.

In this chapter, we\'ve covered the concept of NIP scene models. In
detail, we examined the following aspects:

\* Limited targets - internal (here, me) versus external entities
(everything else). \* The usage of scene actors. \* Manipulating
(creating, modifying, deleting) scenes. \* The relationship between
scene actors\' symbolic identifiers and `$variables`. \* The +nip scene
tool. \* Executing a BDO call externally (from a Merry script), using
symbolic identifiers to interpret the situation.

To read about tracking and replaying, [proceed to Chapter
IV](NIPClassRecordingIV). If you feel unsure about the basics of
recording, you may want to head back to [Chapter I](NIPClassRecording)
and/or [II](NIPClassRecordingII). Alternatively, you may choose either
of the other chapters:

\* [Chapter I - Making it \"behave.\"](NIPClassRecording) \* [Chapter II
- Freemoting.](NIPClassRecordingII)

\* [Chapter IV - Tracking and replaying.](NIPClassRecordingIV) \*
[Chapter V - The setting model.](NIPClassRecordingV)

Read more about [setting up a scene.](NIPTutorialScenery)

\-- Main.KalleAlm - 22 May 2004

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
CLASS\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
%META:FILEATTACHMENT{name=\"bdoscenemodel.png\" attr=\"h\" comment=\"\"
date=\"1085220207\" path=\"bdo scene model.png\" size=\"8713\"
user=\"kallea\" version=\"1.2\"}%
