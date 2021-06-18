%META:TOPICINFO{author=\"kallea\" date=\"1085145431\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>LIBRARY REFERENCE: mountrider\</FONT\>

\<font class=\"query\"\>CATEGORY:\</font\>
[External](NIPCategoryExternal)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:mountrider

\<font class=\"query\"\>DEPENDENCIES:\</font\>
[mounting](NIPLibRefMounting)

\<font class=\"query\"\>COMPATIBILITY:\</font\> None/All.

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

The mountrider lib contains inherit scripts for the rider of a mounted
NPC. **Note: This library should not be loaded in an NPC; it is taken
care of automatically by the [mounting](NIPLibRefMounting) library.**

\<font class=\"query\"\>DESCRIPTION\</font\>

The mountrider lib is not an actual NIP library, in that it is never
loaded to an NPC directly. It is, however, used by the NIP library
[mounting](NIPLibRefMounting) to put a set of inherits into a body which
mounts the NPC.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

None.

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:act-post:enter\</font\> \<UL\> This script
handles all movement through rooms. It is inherited by the rider.
\</UL\>

\<font class=\"lib\"\>merry:act:approach\</font\> \<UL\> This script
deals with approach issues. It is inherited by the rider. \</UL\>

\<font class=\"lib\"\>merry:act:dismount\</font\> \<UL\> This script
will, when the rider types \'dismount\', remove him/her from the NPC and
unload the inherits. It is inherited by the rider. \</UL\>

\<font class=\"lib\"\>merry:act:leave\</font\> \<UL\> This script deals
with leave issues. It is inherited by the rider. \</UL\>

\<font class=\"lib\"\>merry:act:stance\</font\> \<UL\> This script deals
with stance issues. It is inherited by the rider. \</UL\>

\-- Main.KalleAlm - 08 Jun 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
