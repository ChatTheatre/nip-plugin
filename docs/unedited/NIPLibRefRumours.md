%META:TOPICINFO{author=\"kallea\" date=\"1085145329\" format=\"1.0\"
version=\"1.4\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: rumours\</font\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Behavior](NIPCategoryBehavior)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:rumours

\<font class=\"query\"\>DEPENDENCIES:\</font\> [asking](NIPLibRefAsking)

\<font class=\"query\"\>COMPATIBILITY:\</font\>
[presents](NIPLibRefPresents)

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

Asking an NPC about something (e.g. \"ask npc about queen\")

\<font class=\"query\"\>DESCRIPTION\</font\>

The rumours library is the replacement of the currently existing (but
fairly unused) \"ask \<npc\> about \<topic\>\" feature.

A tutorial on the usage of this library can be found
[here](NIPHowRumours).

\<font class=\"query\"\>NIP PROPERTIES\</font\>

\<font class=\"lib\"\>nip:trait:rumour:database\</font\> \<UL\> (object)
The reference to the data object which contains the rumour database.
(see aforementioned tutorial for more information) \</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:handler:ask-about\</font\> \<UL\> \"The
rumour-handler; this script is called whenever someone asks an NPC (with
the \'rumours\' library implemented) about **something**. It will look
in the specified data object (\'nip:trait:rumour:database\') for the
topic in question, or say \"(S)He doesn\'t know anything about that.\"
if it was not found.\" \</UL\>

\-- Main.KalleAlm - 13 Nov 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)

Updated to abide the documentation. (doc says \"topic:*name*\", code
looked for \"**rumour**:*name*\" \-- code now looks for
\"**topic**:*name*\")

\-- Main.KalleAlm - 23 Feb 2004
