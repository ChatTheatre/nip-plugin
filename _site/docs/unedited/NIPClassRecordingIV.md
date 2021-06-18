%META:TOPICINFO{author=\"kallea\" date=\"1149553944\" format=\"1.0\"
version=\"1.6\"}% %META:TOPICPARENT{name=\"NIPClassRecordingIII\"}%
[NIPClassStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>CLASS: Recording and behavior - \[IV - Tracking
and replaying.\]\</font\>

\<font class=\"query\"\>AUDIENCE:\</font\> EXPERIENCED

\<font class=\"query\"\>PREREQUISITE KNOWLEDGE:\</font\>

\* You should be familiar with the +nip tool. Specifically the
\"record\" and \"scene\" functions. \* You should know what a BDO is. \*
You should know how to record behavior data. \* You should know the
basics of Merry. \* You should know what a scene model is. \* You should
know how to set up and manipulate scenes, and be somewhat clear on how
these interoperate with the behavior system.

\<font class=\"query\"\>SUMMARY:\</font\>

In this brief chapter, we\'re going to take a quick look at what the BDO
tracker link is, and its uses, namely recording an ordered behavior
sequence rather than, as is the default, one randomly aligned.

[]{.twiki-macro .TOC}

------------------------------------------------------------------------

## Ordered versus random behavior sequence.

An ordered behavior sequence might for example be\...

    Lucy officially straightens.

    Lucy strides formally to you.

    Lucy advertises her badge pointedly, "You're under arrest!"

If we recorded the above three things in a regular BDO, things would
\"occur\" in a hopelessly nonsensical order in most cases, unless we
were \"fortunate.\"

    Lucy strides formally to you.

    Lucy strides formally to you.

    Lucy officially straightens.

    Lucy strides formally to you.

    Lucy advertises her badge pointedly, "You're under arrest!"

    Lucy strides formally to you.

    Lucy officially straightens.

And so on. Nonsensical, stupid, useless, etc.

In order to do this accurately, we need to enable tracking before we
begin to record.

------------------------------------------------------------------------

## The +nip tracking function.

The +nip \"tracking\" function can be called in the following two
ways:\<verbatim\>+nip \"tracking on\"\</verbatim\>and\<verbatim\>+nip
\"tracking off\"\</verbatim\>

Whilst enabled, the recording tool will include something called a
tracking vector which keeps track of the order in which we record our
data. By using the tracking vector, we can then **replay** the behavior
data in the correct order.

------------------------------------------------------------------------

## Random versus ordered sequence behavior data.

When requesting a random sequence behavior data (RSBD) execution (where
RSBD equals everything we\'ve done so far), NIP will find and perform a
behavior data entry at random from the list of entries in the BDO. After
performing, NIP will simply call it a day and return to normal.

It\'s not that simple when it comes to ordered sequence behavior data
(OSBD), however. It won\'t do to simply execute one of the entries at
random. After all, that\'s not very ordered of us, is it? Instead, NIP
has to explicitly perform each entry listed in the BDO before it is
done.

This introduces another minor problem. In the case of RSBD execution,
the time **between** each entry\'s execution is not an issue, because
RSBD execution only executes one entry at a time. But OSBD execution
involves executing **every entry in the BDO page**. How will NIP know
how much time to wait in between each entry? The answer is simple - it
can\'t. Therefore, you have to explicitly feed it this information.

------------------------------------------------------------------------

## Pause specifier.

Thus we introduce the final record tool symbol \-- @ (\"at\").

The @ symbol is used to specify the amount of seconds to pause between
the previous entry and the entry which comes thereafter.

    <b>> say "!Five and a half second will pass before I say so."</b>
    You say, "!Five and a half second will pass before I say so."
    [STO:4]
    <b>> "@5.5</b>
    You say, "@5.5."
    [DELAY:7]
    <b>> say "!So!</b>
    You say, "!So!"
    [STO:5]

If we execute the above, the NPC will first say \"Five and a half second
will pass before I say so.\" Then 5.5 seconds will pass, after which the
NPC will say \"So\"

------------------------------------------------------------------------

## Result.

The usage of tracking requires the library
[replaying](NIPLibRefReplaying). Thus, we need to add this library to
any/all NPC\'s which are to execute ordered sequence behavior data.

1 Create a new BDO page by switching the session identifier to something
unused. I\'ll be using \"sequentialstuff\" as the session
ID.\<verbatim\>+nip \"record switch sequentialstuff\"\</verbatim\>(If
you have disabled recording entirely, type
`+nip "record start <i>woename</i> sequentialstuff"` instead.) 2 Enable
tracking.\<verbatim\>+nip \"tracking on\"\</verbatim\> 3 Record between
two and half a dozen actions. (Remember to include pause information in
between each action) 4 Stop recording.\<verbatim\>+nip \"record
stop\"\</verbatim\> 5 Disable tracking.\<verbatim\>+nip \"tracking
off\"\</verbatim\> 6 At this point, we\'ve created ordered sequence
behavior data. Now all we need to do is execute it. We\'ll do this by
creating a small Merry script in our NPC.\<verbatim\>+to me ed
%woename-for-npc react-post:smile-iob\</verbatim\> 7 Type in the
following, then click Submit CHANGES:\<verbatim\>::handler_replay( \$db:
this.\"nip:behavior:db\", \$scene: \"sequentialstuff\" );\</verbatim\> 8
Add the NIP library \"replaying\" to the NPC.\<verbatim\>+setp
\<nipper\> \"add replaying\"\</verbatim\>

That\'s it. Now try to smile at the NPC and see if it\'s reacting as it
should.

------------------------------------------------------------------------

## Log start-finish.

    ---
    <b>> +nip "record switch sequentialstuff</b>
    Mood/condition changed from myScene to sequentialstuff in &lt;Kalle:charles&gt;.
    <b>> +nip "tracking on</b>
    NIP record tracking vector enabled.
    <b>> smile "!</b>
    You smile, "!"
    [Tracker link set up. See troll TWiki for details.]
    [STO:1]
    <b>> "@2.5</b>
    You say, "@2.5."
    [DELAY:1]
    <b>> wave "!Halo.</b>
    You wave, "!Halo."
    [STO:2]
    <b>> "@2</b>
    You say, "@2."
    [DELAY:2]
    <b>> introduce me happi "!I'm Charles.</b>
    You introduce yourself happily, "!I'm Charles."
    [STO:3]
    <b>> +nip "record stop</b>
    Stopped recording in &lt;Kalle:charles&gt;.
    <b>> +nip "tracking off</b>
    NIP record tracking vector disabled.
    <b>> +to me ed %Kalle:charles react-post:smile-iob</b>
    Editing source in popup window.
    <b>> +setp me "add replaying</b>
    Setting 'add' in &lt;Kalle:charles&gt;;
    - from: nil
    - to: "replaying"
    [cut]
    The 'replaying' library was loaded. You can use this to replay entire recordings, provided these 
    have a track link vector present. From within Merry, all you do is, e.g. ::handler_replay( $db: 
    ${My:bdb}, $scene: "HAPPY-GILMORE" ); -- this will replay the entire recording sequence named 
    "HAPPY-GILMORE", located in the object &lt;My:bdb&gt;.
    &lt;Lib:NIP:lib:replaying&gt; loaded successfully.
    <b>+poss nickademis</b>
    > You inhabit Nickademis.
    <b>> smile at charles</b>
    You smile at a phoenix.
    A phoenix smiles.
    A phoenix waves, "Halo."
    A phoenix introduces himself happily, "I'm Charles."
    ---

------------------------------------------------------------------------

## Post summary.

In this chapter, we covered the concept of tracking vectors, which are
necessary in ordered sequence behavior data. We talked about the
difference between ordered (OSBD) versus random (RSBD). We learnt about
the pause symbol (@), why we use it and how we use it. And finally, we
created a brief example in which we used the
[replaying](NIPLibRefReplaying) library to replay a BDO page orderedly.

\* The +nip \"tracking\" function. \* RSBD and OSBD. \* The pause
specifier (@).

To read about the setting model, [proceed to Chapter
V](NIPClassRecordingV). If you feel unsure about the basics of
recording, you may want to head back to [Chapter I](NIPClassRecording),
[II](NIPClassRecordingII) and/or [III](NIPClassRecordingIII).
Alternatively, you may choose either of the chapters in the list below:

\* [Chapter I - Making it \"behave.\"](NIPClassRecording) \* [Chapter II
- Freemoting.](NIPClassRecordingII) \* [Chapter III - The scene
model.](NIPClassRecordingIII)

\* [Chapter V - The setting model.](NIPClassRecordingV)

\-- Main.KalleAlm - 22 May 2004

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
CLASS\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)

Maybe its just me, (seems to be the case alot) but the Tracking/Replay
commands doesnt work at all. Whenever I attempt to use it I receive the
message stating the tracking function is not listed in the function
library. Nor s it listed under the +nip list. \--
Main.StoryBuilderLilith - 05 Jun 2006

It may not be loaded on your server. Which server are you on?

-Kalle.

I\'m in the Lazarus system, which I believe is the same server as Castle
Marrach. \-- Main.StoryBuilderLilith - 05 Jun 2006

Fixed on Lazarus. There were un-registered calls in +nip. +nip tracking
should work now.

-Kalle.
