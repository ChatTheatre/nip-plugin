%META:TOPICINFO{author=\"kallea\" date=\"1085145372\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>LIBRARY REFERENCE: musician\</FONT\>

\<font class=\"query\"\>CATEGORY:\</font\> [Example](NIPCategoryExample)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:musician

\<font class=\"query\"\>DEPENDENCIES:\</font\> [MOOD](NIPHookRefMood),
[commanding](NIPLibRefCommanding)

\<font class=\"query\"\>COMPATIBILITY:\</font\>
[emoting](NIPLibRefEmoting), [freemoting](NIPLibRefFreemoting)

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

The musician library specifically sets an NPC up so that whenever
someone orders the NPC to \"play\", it will *want to* play. This is done
by adding a mood called \"**PLAY**,\" which is stimulated when the
NPC\'s should play, and is suppressed when they\'re not.

\<font class=\"query\"\>DESCRIPTION\</font\>

The musicians are (soon) used live on Marrach. They can be directed when
to play and when not to, simply by telling them. They currently use
static data such as **marrach:precedence** to determine whether a person
is allowed to order them or not. A person must also speak Northern or
Teanga, and do so as skilled as or more skilled than a
**fellowcraftsman**.

Especially the **marrach:precedence** check must be converted to use a
more dynamic form of authority-check. This is a low priority upgrade
until someone voices interest in using the musician lib.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

None.

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:command:music:begin\</font\> \<UL\> This
script uses the [commanding library](NIPLibRefCommanding)\'s command
chain feature, and is called when someone says \'begin\', \'start\', or
\'proceed\' to the NPC. The script will set the boolean
**\"npc:playing\"** to TRUE, which will be used (described below) by the
\<font class=\"lib\"\>merry:lib:musician:mood\</font\> sig-hook. \</UL\>

\<font class=\"lib\"\>merry:lib:command:music:end\</font\> \<UL\> This
script is a clone of the script described above, except it will set the
**\"npc:playing\"** property to FALSE. \</UL\>

\<font class=\"lib\"\>merry:lib:init\</font\> \<UL\> NIP Library init
script.\<br\> The mood \'PLAY\' is added using **core:add_mood**, the
commands \"**music:begin**\" and \"**music:end**\" are added using the
**core:add_command** script. \</UL\>

\<font class=\"lib\"\>merry:lib:musician:mood\</font\> \<UL\> (Signal
MOOD; hook musician)\<BR\> This script will set the mood \'PLAY\' to \*
20, if the property **\"npc:playing\"** is TRUE \* 0, if the property
**\"npc:playing\"** is FALSE \</UL\>

\-- Main.KalleAlm - 07 Jun 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
