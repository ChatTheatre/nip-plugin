%META:TOPICINFO{author=\"kallea\" date=\"1115915560\" format=\"1.0\"
version=\"1.12\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<STYLE\> HR { border: solid \#aaaaaa 3px; width: 75%; height: 1px; }
\</STYLE\>

\<A NAME=\"top\"\>\<FONT CLASS=\"title\"\>Frequently Asked
Questions\</FONT\>\</A\>

This is the FAQ for the NIP system. The Q/A\'s in here will probably
grow to quite a number in time, but only if you bother to ask the
questions. If something you\'re trying to figure out **is not described
here**, I would be very thankful if you \<A
HREF=\"[mailto:kalle\@marrach.skotos.net](mailto:kalle@marrach.skotos.net)\"\>poked
me about it so I can try to add it\</A\>. Thanks!

[]{.twiki-macro .TOC}

------------------------------------------------------------------------

## How do I turn my object into a nipper?

Figure out its woename (`+obname <npc>`), then type:\<verbatim\>+nip
\"set woe:name\"\</verbatim\>

------------------------------------------------------------------------

## It doesn\'t ever eat/drink/act! What\'s wrong?

Check if your NPC is alive. If you get this,

    <B>> +delays NPC</B>
    There are no running delays on &lt;...>.

\- your NPC is not running. Start it up by typing,

    <B>> +nip NPC 'live'</B>

\<A HREF=\"\#top\"\>Top\</A\>

------------------------------------------------------------------------

## I start it, but then after a little while it just dies on me.

You\'ve probably encountered a bug. It shouldn\'t die unless you
specifically tell it to. \<A
HREF=\"[mailto:kalle\@marrach.skotos.net](mailto:kalle@marrach.skotos.net)\"\>Let
me know about this\</A\> so we can fix it.

If you\'ve been doing **a lot of tweaking**, perhaps removing the signal
DELAY (ouch) or setting the \$NPC_PAUSE property insanely (very low),
the system will turn itself off, thinking it\'s gone insane (which in
that case is true).

\<A HREF=\"\#top\"\>Top\</A\>

------------------------------------------------------------------------

## I\'d like to see some more debug stuff when I work with this.

There is built-in support for warnings/errors redirection, but it\'s by
default disabled. The ease-of-use for this will be improved over time,
but you can currently do the following to see the debug info:

\* **For warnings:** \<VERBATIM\>+setp NPC \"merry:setprop-post:warning
X\[M\] EmitTo( \${Your:woe:name}, this.warning );\"\</VERBATIM\>

\* **For errors:** \<VERBATIM\>+setp NPC \"merry:setprop-post:error
X\[M\] EmitTo( \${Your:woe:name}, this.error );\"\</VERBATIM\>

\<A HREF=\"\#top\"\>Top\</A\>

------------------------------------------------------------------------

## I try to add a library but I keep getting \"Libraries are needed:\" errors.

Some libraries depend on others to function properly. You will have to
add the library in question to make it work. If it says it needs
\<Lib:NIP:lib:something\>, you should +setp NPC \"add something\"
(without Lib:NIP:lib:).

\<A HREF=\"\#top\"\>Top\</A\>

------------------------------------------------------------------------

## I\'m trying to add a library, but the system can\'t find it.

The system uses a thing called a \"library path\" to find the libraries
you\'re attempting to add/remove. As such, you can\'t place a library
\'anywhere\', you have to put it in one of the paths listed.

Some of these paths contain aliases for \"your theatre id\". If the
library in question is private for your game, you can place it in for
instance *yourtheatre*:NIP:lib.

A complete list of possible locations for libraries can be found
[here](NIPRefLibraries15), which is a page in the [library reference
document](NIPRefLibraries).

\<A HREF=\"\#top\"\>Top\</A\>

------------------------------------------------------------------------

## I\'ve got problems getting my behavior database to work.

\* 1. Did you make a behavior db? It should be a propertycontainer,
which should look like either of the examples in <Data:NIP:behavior>.

\* 2. Does it contain anything at all? It should have a series of very
bizarre looking properties.

\* 3. If you\'re using moods,

\* - does your NPC ever use the mood you specified in the +nip command?
(*+nip \"record start Woe:for:db***MOOD***\"*)\<BR\>Check by typing
\<VERBATIM\>+stat NPC \"property:npc:mood\"\</VERBATIM\>

\* 4. Did you use the universal mood **DB** when you recorded? The
properties in the behavior database should start with **\"db:\"**

\* 5. Did you specify the DB in the NPC? Property
**\"nip:behavior:db\"**, optionally **\"nip:behavior:\<MOOD\>\"**.

\* 6. Is your NPC alive? \<A
HREF=\"\#My_NPC_doesn_t\_ever_eat_drink_ac\"\>Hop here\</A\>.

\* 7. Did you add the emoting library to your npc? **+setp \<npc\> \"add
emoting\"**

\<A HREF=\"\#top\"\>Top\</A\>

------------------------------------------------------------------------

## How do I use this/that library?

If the library is in the standard NIP collection, it should be well
documented. If it\'s not, feel free to \<A
HREF=\"[mailto:kalle\@marrach.skotos.net](mailto:kalle@marrach.skotos.net)\"\>give
me a poke about it\</A\> and I\'ll try to write one up for you.

\<A HREF=\"\#top\"\>Top\</A\>

------------------------------------------------------------------------

## How do I make my own library?

Learn by doing. :) Also, there are an ever growing list of library docs
available. Check out either of the library references for an idea what a
library is supposed to do. Also be sure to read the [Creating a
library](NIPRefLibraries) tech ref doc.

\<A HREF=\"\#top\"\>Top\</A\>

------------------------------------------------------------------------

## What\'s the difference between a signal and a hook?

A signal is just an identifier and a priority. That\'s all there is to
signals, whereas hooks are \"packages\" of scripts associated with
either/all of the existing signals.

\<A HREF=\"\#top\"\>Top\</A\>

------------------------------------------------------------------------

## I want to spawn several copies of the npc I just made; will there be any problems or things I should be aware of?

Yes. When spawning a NIP object, the spawn will become a child of the
parent, **but** the child will not retrieve customizations done to the
parent automatically. UrInheritance, for merry scripts, detail
descriptions, etc. will work just as normal, however.

\<A HREF=\"\#top\"\>Top\</A\>

------------------------------------------------------------------------

## I\'m trying to add a library, but it\'s crashing! What do I do?

The system has a lot of debug data when you manipulate the libraries,
hooks and/or signals. You won\'t see it, unless you **+possess the NPC**
and do +setp me \"add \<libraryname\>\".

If things seem to be going wrong when you\'re trying to add a library,
simply \* +possess the NPC \* start logging \* add the library to
yourself \* stop logging \* \<a
href=\"[mailto:kalle\@marrach.skotos.net](mailto:kalle@marrach.skotos.net)\"\>mail
it to me\</a\>, preferably with some info on what you did and where,
which server, etc.

Of course, you don\'t need to email me if you manage to figure out the
issue by looking at the debug output. Otherwise, I\'ll gladly assist.

------------------------------------------------------------------------

## I\'m trying to record, but keep getting \"Action ignored as only own details and \'here\' are accepted targets.\" messages.

When recording with \"external entities\" (anything that is not
**always** \'there\'), you need to set up a scene using the +nip
\"scene\" tool. Further information on these topics:

\* [Class: recording and behavior.](NIPClassRecording) \* [+nip-tool
\"scene\"](NIPToolScene) \* [Tutorial: Setting up a
scene.](NIPTutorialScenery)

On recording in general,

\* [+nip-tool \"record\"](NIPToolRecord) \* [How-to: Recording a
behavior database.](NIPHowRecord) \* [How-to: Recording
freemotes.](NIPHowRecordFreemotes)

------------------------------------------------------------------------

## It won\'t pick up or accept food! What\'s wrong?

and

## My merchant npc won\'t give me things!

and

## My trash-taking npc won\'t take trash from me!

You may have done the classy mistake of not giving the NPC proper
capacity. This is in the bulk settings of the woe object. Set capacity
and max weight to something appropriate and try again.

------------------------------------------------------------------------

## I am writing communications data with families and such. How do I write behavior for when my nipper doesn\'t understand what is being said to them?

Add a new family to the comm db, and set it to `({ })`. This family will
catch everything that is being said to your NPC. Be sure to put this at
the very end of your `nip:families` array, since it\'ll override
everything after it otherwise.

------------------------------------------------------------------------

\-- Main.KalleAlm - 15 Nov 2003
