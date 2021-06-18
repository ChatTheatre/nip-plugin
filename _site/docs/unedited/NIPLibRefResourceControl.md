%META:TOPICINFO{author=\"kallea\" date=\"1085145459\" format=\"1.0\"
version=\"1.4\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: resource-control\</font\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Internal](NIPCategoryInternal)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:resource-control

\<font class=\"query\"\>DEPENDENCIES:\</font\> None

\<font class=\"query\"\>COMPATIBILITY:\</font\> All

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None

\<font class=\"query\"\>FEATURES\</font\>

Resource-control controls when to disable and enable a NPC. The NPC will
completely shut down when the time since an object entered or logged is
greater than the defined ttl (time to live), if there is not an object
in the area with volition (that is not an NPC also).

The NPC will also restart when an object with volition enters the area
or logs into the area.

\<font class=\"query\"\>DESCRIPTION\</font\>

See features.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

\<font class=\"lib\"\>nip:trait:resource-control:ttl\</font\> \<UL\>
Stores the time to live value in seconds. When the time since an object
entered the area or logged in is greater than the TTL, then the NPC
checks for shutdown. Default value is 1800 (30 minutes). \</UL\>

\<font class=\"lib\"\>nip:trait:resource-control:ttl_increase\</font\>
\<UL\> If there is a non-npc object in the area with volition, this
value is added to the npc:resource-control:live_time property and the
cycle repeats. Default value is 600 (10 minutes). \</UL\> \<font
class=\"lib\"\>npc:resource-control:live_time\</font\> \<UL\> Anytime an
object enters the area or logs into the area, this property is updated
with the current time() timestamp on the NPC. \</UL\> \<font
class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:entering\</font\> \<UL\> This script is
used to record the timestamp when an object enters the area of the NPC
or logs in. This script will also restart the NPC if it was previously
in a state of shutdown.

Both witness-post:login%nip:resource-control and
witness-post:enter-from%nip:resource-control use this script. \</UL\>

\<font class=\"lib\"\>merry:lib:resource-control:internal\</font\>
\<UL\> This is the guts of the lib. This script determines if an NPC
should be checked for shutdown status and shutdown. \</UL\>

\-- Main.JessieBrickner - 25 Nov 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)

The script \'witness-post:teleport%resource-control\' was added.

\-- Main.KalleAlm - 23 Mar 2004
