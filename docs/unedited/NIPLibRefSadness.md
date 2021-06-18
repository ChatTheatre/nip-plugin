%META:TOPICINFO{author=\"kallea\" date=\"1085145329\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>LIBRARY REFERENCE: sadness\</FONT\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Behavior](NIPCategoryBehavior)

\<QUERY\>WOE NAME:\</QUERY\> Lib:NIP:lib:sadness

\<QUERY\>DEPENDENCIES:\</QUERY\> [MOOD](NIPHookRefMood)

\<QUERY\>COMPATIBILITY:\</QUERY\> None/All.

\<QUERY\>INCOMPATIBILITY:\</QUERY\> None.

\<QUERY\>FEATURES\</QUERY\>

Sadness provides the mood \'sad\' to the NPC.

\<QUERY\>DESCRIPTION\</QUERY\>

The sadness mood uses the default MOOD system to include the \'sad\'
mood. See **nip:mood:registry** in any NPC using the system. Also see
\<LIB\>Lib:NIP:signals:MOOD\</LIB\>/**lib:core:add_mood** and
\<LIB\>Lib:NIP:signals:MOOD\</LIB\>/**lib:core:sub_mood** for more
details on how to create a new mood.

\<QUERY\>NIP PROPERTIES\</QUERY\>

None.

\<QUERY\>LIBRARY SCRIPT REFERENCE(S)\</QUERY\>

\<LIB\>merry:lib:init\</LIB\> \<UL\> NIP Library init script. \</UL\>

\<LIB\>merry:lib:sadness:mood\</LIB\> \<UL\> (Signal MOOD; hook
sadness)\<br\> This script looks at how the NPC feels at the moment
(e.g.i.a. hunger) and adjusts the mood \'SAD\' accordingly. \</UL\>

\-- Main.KalleAlm - 07 Jun 2003

\<QUERY\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</QUERY\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
