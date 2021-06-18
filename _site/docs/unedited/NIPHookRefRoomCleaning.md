%META:TOPICINFO{author=\"kallea\" date=\"1121803140\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>SIGNAL/HOOK REFERENCE: room-cleaning\</FONT\>

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:hooks:room-cleaning

\<font class=\"query\"\>HOOK(S):\</font\> room-cleaning

\<font class=\"query\"\>COMPATIBILITY:\</font\>
[trash-taker](NIPLibRefTrashTaker)

\<font class=\"query\"\>DEPENDENCIES:\</font\>
[trash-taker](NIPLibRefTrashTaker)

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>MAIN PURPOSE\</font\>

To (spontaneously) clean up rooms.

\<font class=\"query\"\>DESCRIPTION\</font\>

The room-cleaning hook randomly picks up trash from rooms the NPC
encounters, unless these rooms have the property \"trash:protected\"
set.

Note: the old \"npc:disable-clean\" property is deprecated, but is still
respected. It should be replaced with \"trash:protected\" at some point,
however.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

\<font class=\"lib\"\>nip:trait:trash:frequency\</font\> \<UL\> How
frequently will we clean? 1 = always, 2 = 50% of the time, 3 = 33% of
the time, etc. \</UL\>

\<font class=\"query\"\>SIGNAL/HOOK SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:room-cleaning:decide\</font\> \<UL\>
(Hook \'room-cleaning\'; signal \'DECIDE\')

\"The room-cleaning decide hook-script. This script will randomly pick
up trash from \"the current room.\" An object is defined as trash
according to the SkotOS Trash System rules.\" \</UL\>

\-- Main.KalleAlm - 13 Nov 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)

Updated to use virtual trashcan and sscanf rules \"\[%s\]\#%d\". See
NIPLibRefTrashTaker for further information.

\-- Main.KalleAlm - 28 Oct 2004

This system is now compatible with the SkotOS TrashSystem.

\-- Main.KalleAlm - 19 Jul 2005
