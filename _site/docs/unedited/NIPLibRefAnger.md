%META:TOPICINFO{author=\"kallea\" date=\"1139250230\" format=\"1.0\"
version=\"1.6\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>LIBRARY REFERENCE: anger\</FONT\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Behavior](NIPCategoryBehavior)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:anger

\<font class=\"query\"\>DEPENDENCIES:\</font\> [MOOD](NIPHookRefMood)

\<font class=\"query\"\>COMPATIBILITY:\</font\> None/All.

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

Anger provides the mood \'angry\' to the NPC.

\<font class=\"query\"\>DESCRIPTION\</font\>

The anger mood uses the default MOOD system to include the \'angry\'
mood. See **nip:mood:registry** in any NPC using the system. Also see
\<font
class=\"lib\"\>Lib:NIP:signals:MOOD\</font\>/**lib:core:add_mood** and
\<font
class=\"lib\"\>Lib:NIP:signals:MOOD\</font\>/**lib:core:sub_mood** for
more details on how to create a new mood.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

None.

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:anger:mood\</font\> \<UL\> (Signal MOOD;
hook anger)\<br\> This script is supposed to regulate the ANGRY mood
according to how the NPC feels. \</UL\>

\<font class=\"lib\"\>merry:lib:init\</font\> \<UL\> NIP Library init
script. \</UL\>

\-- Main.KalleAlm - 05 Jun 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)

When does a NIP become more angry? Under what conditions? And can those
conditions be controlled via +setp or should they be left alone? \--
Main.ToddNilson - 05 Feb 2006

Very much an undeveloped aspect. The only thing, to my knowledge, that
modifies anger is the [relations library](NIPLibRefRelations), which
lacks proper tools to be truly useful.
