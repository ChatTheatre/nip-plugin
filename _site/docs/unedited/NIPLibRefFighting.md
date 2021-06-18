%META:TOPICINFO{author=\"kallea\" date=\"1085145486\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: fighting\</font\>

\<font class=\"query\"\>CATEGORY:\</font\> [Service](NIPCategoryService)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:fighting

\<font class=\"query\"\>DEPENDENCIES:\</font\> None.

\<font class=\"query\"\>COMPATIBILITY:\</font\>
[fighting-marrach](NIPLibRefFightingMarrach)

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>KNOWN ISSUES:\</font\>

Confirmed () issues with this library. (Unconfirmed issues should be
reported in the feedback section at the bottom of this document.)

\<font class=\"query\"\>FEATURES\</font\>

Combat handler for an external combat system.

\<font class=\"query\"\>DESCRIPTION\</font\>

Fighting is an NPC-vs-PC/NPC-vs-NPC wrapper for NIP, which makes use of
an external, time-based combat system. (A turn-based combat system
wrapper will be put in place at some point, as well, but will be an
entirely different library.)

The library requires that you set it up according to the rules of the
combat system. One way of doing this (the preferred way) is to create a
secondary library. One example of such is
[fighting-marrach](NIPLibRefFightingMarrach), which makes use of the
Castle Marrach duelling system.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

`mapping <font class="lib">nip:trait:fighting:condition_map</font>`
\<UL\> Map of external conditions which affect the nipper\'s
decision-making. Property syntax:\<pre\>(\[ \"\<property in NPC\>\" : ({
\<middle value\>, \<effect\>, &ltpositive list\>, \<negative list\> })
\])\</pre\>

E.g.\<pre\>(\[ \"duelling:fatigue\":({ 50, 0.2, ({ \"cut\", \"jab\",
\"feint\" }), \"rest\" }) \])\</pre\> \</UL\>

`mapping <font class="lib">nip:trait:fighting:delay_map</font>` \<UL\>
Map of delay-time in between actions, with min-to-max values. Property
syntax:\<pre\>(\[ \"\<command\>\" : ({ \<min time\>, \<max time\> })
\])\</pre\>

E.g.\<pre\> (\[ \"advance\":({ 0.5, 1.0 }), \"cut\" :({ 2.1, 3.0 }),
\"dodge\" :({ 1.1, 2.0 }), \"feint\" :({ 2.1, 3.0 }), \"guard\" :({ 0.5,
4.0 }), \"jab\" :({ 2.1, 2.5 }), \"lunge\" :({ 3.5, 5.5 }), \"rest\" :({
0.1, 0.3 }), \"retire\":({ 0.5, 1.0 }), \"slip\" :({ 4.0, 6.0 }) \])
\</pre\> \</UL\>

`mapping <font class="lib">nip:trait:fighting:imperative_map</font>`
\<UL\> Map of imperatives with probability values. See
[fighting-marrach](NIPLibRefFightingMarrach) for explanative example.
\</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

`<font class="lib">core_fight_done()</font>` \<UL\> When a fight is
ended, the core_fight_done() function **must** be called, in order to
disable the internal combat thread. As soon as a fight has ended, no
matter how it ended, this function should be called as soon as possible.
\</UL\>

`<font class="lib">core_fight_init()</font>` \<UL\> Initiate combat.
This function will take control over the NPC for the duration of the
fight, and attempt to perform various combat-related commands to win a
fight. \</UL\>

\-- Main.KalleAlm - 09 May 2004

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
