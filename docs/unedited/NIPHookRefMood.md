%META:TOPICINFO{author=\"kallea\" date=\"1055012203\" format=\"1.0\"
version=\"1.1\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>SIGNAL/HOOK REFERENCE: MOOD\</FONT\>

\<QUERY\>WOE NAME:\</QUERY\> Lib:NIP:signals:MOOD

\<QUERY\>SIGNAL:\</QUERY\> MOOD

\<QUERY\>INITIAL PRIORITY:\</QUERY\> 100

\<QUERY\>HOOK(S):\</QUERY\> mood

\<QUERY\>DEPENDENCIES:\</QUERY\> None.

\<QUERY\>COMPATIBILITY:\</QUERY\> [anger](NIPLibRefAnger),
[eating](NIPLibRefEating), [emoting](NIPLibRefEmoting),
[freemoting](NIPLibRefFreemoting), [happiness](NIPLibRefHappiness),
[musician](NIPLibRefMusician), [sadness](NIPLibRefSadness),
[sleeping](NIPLibRefSleeping)

\<QUERY\>INCOMPATIBILITY:\</QUERY\> None.

\<QUERY\>MAIN PURPOSE\</QUERY\>

The MOOD signal implements, together with the signal-hook \'mood\', the
aspect of a mood registry in an NPC. This mood registry can then be
heavily customized and used in various ways to make an NPC\'s current
mood vary depending on whichever internal/external circumstances there
might be.

\<QUERY\>DESCRIPTION\</QUERY\>

Initially, MOOD sets the mood registry with one single mood
(\"NEUTRAL\") which can then be added to either manually by calling the
appropriate functions (see below) or by adding either of the \"mood\"
libraries, for instance [anger](NIPLibRefAnger).

Making your own mood is an easy enough thing to do. Simply: \* create a
library, \* call it something appropriate (e.g. \"irritation\"), \* add
a hook, which you also call irritation, \* put a
\<LIB\>merry:lib:irritation:mood\</LIB\> sig-hook to it which adjusts
**this.\"nip:moodvals\"\[\"IRRITATED\"\]** (the higher, the stronger) \*
and finally, put a \<LIB\>merry:lib:init\</LIB\> script in it, which in
the above case would do: **Call( this, \"core:add_mood\", \$mood:
\"IRRITATED\" );**

See further documentation on how to create signals, libraries and signal
hooks for more information, or simply look at either of the existing
scripts for reference.

\<QUERY\>NIP PROPERTIES\</QUERY\>

\<LIB\>npc:mood\</LIB\> \<UL\> String reference to the current mood,
e.g. \"HAPPY\" \</UL\>

\<LIB\>nip:moodvals\</LIB\> \<UL\> Mapping, mood registry property. The
moods in this property are all reset to 0 (except \"NEUTRAL\" which is
set to 1) initially (e.g. **(\[ \"HAPPY\" : 0, \"NEUTRAL\" : 1,
\"SLEEPY\" : 0 \])**) after which various sig-hooks attached to the MOOD
signal modify the values.\<br\> \</UL\>

\<QUERY\>SIGNAL/HOOK SCRIPT REFERENCE(S)\</QUERY\>

\<LIB\>merry:lib:core:add_mood\</LIB\> \<UL\> Script that may be used to
add a mood to the mood registry.\<br\> Call( this, \"core:add_mood\",
\$mood: \"MOOD\" ); \</UL\>

\<LIB\>merry:lib:core:sub_mood\</LIB\> \<UL\> Script that may be used to
remove a mood from the mood registry.\<br\> Call( this,
\"core:sub_mood\", \$mood: \"MOOD\" ); \</UL\>

\<LIB\>merry:lib:init-post\</LIB\> \<UL\> NIP Library init-script.\<br\>
Specifically, this script uses the (internal) function \"core:add_mood\"
to add the NEUTRAL mood to the NPC. \</UL\>

\<LIB\>merry:lib:mood:delay\</LIB\> \<UL\> (Signal DELAY; hook
mood)\<BR\> Makes the NPC think slower if the mood is \"neutral.\" (1.5
times higher delay) \</UL\>

\<LIB\>merry:lib:mood:mood-exec\</LIB\> \<UL\> (Signal MOOD; hook mood;
type EXEC)\<br\> This sig-hook grabs the result of the various mood
sig-hooks\' modifications to the **\"nip:moodvals\"** mapping, picks the
strongest mood and sets the **\"npc:mood\"** accordingly. \</UL\>

\<LIB\>merry:lib:mood:mood-init\</LIB\> \<UL\> (Signal MOOD; hook mood;
type INIT)\<br\> This script resets the **\"nip:moodvals\"** mapping.
Initially, the NEUTRAL mood has 1 strength, all others start at 0.
\</UL\>

\-- Main.KalleAlm - 07 Jun 2003

\<QUERY\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</QUERY\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
