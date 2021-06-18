%META:TOPICINFO{author=\"kallea\" date=\"1085145329\" format=\"1.0\"
version=\"1.5\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>LIBRARY REFERENCE: happiness\</FONT\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Behavior](NIPCategoryBehavior)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:happiness

\<font class=\"query\"\>DEPENDENCIES:\</font\> [MOOD](NIPHookRefMood)

\<font class=\"query\"\>COMPATIBILITY:\</font\> None/All.

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

Happiness provides the mood \'happy\' to the NPC.

\<font class=\"query\"\>DESCRIPTION\</font\>

The happiness mood uses the default MOOD system to include the \'happy\'
mood. See **nip:mood:registry** in any NPC using the system. Also see
\<LIB\>Lib:NIP:signals:MOOD\</LIB\>/**lib:core:add_mood** and
\<LIB\>Lib:NIP:signals:MOOD\</LIB\>/**lib:core:sub_mood** for more
details on how to create a new mood.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

None.

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<LIB\>merry:lib:happiness:mood\</LIB\> \<UL\> (Signal MOOD; hook
happiness)\<BR\> This sig-hook script scans various properties in the
NPC and adjusts the \'HAPPY\' mood accordingly. \</UL\>

\<LIB\>merry:lib:init\</LIB\> \<UL\> NIP Library init script. \</UL\>

\-- Main.KalleAlm - 07 Jun 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.) %META:TOPICMOVED{by=\"kallea\"
date=\"1055012274\" from=\"Builders.NIPLibRefHappinesss\"
to=\"Builders.NIPLibRefHappiness\"}%
