%META:TOPICINFO{author=\"kallea\" date=\"1085145486\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>LIBRARY REFERENCE: mounting\</FONT\>

\<font class=\"query\"\>CATEGORY:\</font\> [Service](NIPCategoryService)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:mounting

\<font class=\"query\"\>DEPENDENCIES:\</font\> None.

\<font class=\"query\"\>COMPATIBILITY:\</font\> None/All.

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

(Horse)-back riding library.

\<font class=\"query\"\>DESCRIPTION\</font\>

The mounting library (w/. the [mountrider](NIPLibRefMountrider) lib)
makes it possible to mount the NPC and move around in the room/through
rooms, sitting on its back.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

\<font class=\"lib\"\>nip:trait:mounting:rider-gait\</font\> \<UL\> The
gait, set whenever a character mounts the NPC. This gait should be
something like \"rides\", as it will show as:\<PRE\>**George \<gait\>
out through the north gate.**\</PRE\> This property restores whatever
the gait was, when NPC is dismounted. \</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:init\</font\> \<UL\> NIP Library init
script.\<br\> This script figures out the NIP object name for
\'mountrider\', for future reference, and stores this in
**\"nip:trait:mounting:riderlib\"** \</UL\>

\<font class=\"lib\"\>merry:react:mount-dob\</font\> \<UL\> This react
script puts the person on the NPC, provided some checks turn out right,
e.g. whether the NPC is already mounted and/or whether the person is
mounting something already. \</UL\>

\-- Main.KalleAlm - 08 Jun 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
