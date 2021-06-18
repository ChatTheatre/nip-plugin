%META:TOPICINFO{author=\"kallea\" date=\"1085145459\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: spawn-control\</font\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Internal](NIPCategoryInternal)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:spawn-control

\<font class=\"query\"\>DEPENDENCIES:\</font\> None.

\<font class=\"query\"\>COMPATIBILITY:\</font\> All.

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

Re-spawning of slain NPC\'s, with various settings for how this should
be done.

\<font class=\"query\"\>DESCRIPTION\</font\>

The spawn-control library uses an area object in which a number of
settings are located.

The area object reference is set in the \"nip:trait:spawn:area\"
property, as an object pointer.

The area object supports the following properties:

  ------------------- ----------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Property name**   **Property type**                                     **Description**
  nip:delay:min       integer                                               The minimum amount of seconds before a similar NPC is re-spawned
  nip:delay:max       integer                                               The maximum amount of seconds.
  nip:spawn-point     room OR ({ rooms }) OR (\[ room : entry-message \])   One or several objects (rooms) into which the new NPC should be spawned (randomly, if \>1). If a mapping, the entry-message will be emitted to the room. In the entry-message, the word \"(npc)\" may be used, which will be replaced with the NPC\'s brief on the fly.
  ------------------- ----------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\<font class=\"query\"\>NIP PROPERTIES\</font\>

\<font class=\"lib\"\>nip:trait:spawn:area\</font\> \<UL\> Object
pointer to the area object. \</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:act:stop\</font\> \<UL\> This script is
automatically triggered whenever an NPC is slain. It calls the
lib:system script in Lib:NIP:EXT:spawn, which re-spawns a new NPC after
a specified amount of time. \</UL\>

\-- Main.KalleAlm - 25 Nov 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
