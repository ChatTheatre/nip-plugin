%META:TOPICINFO{author=\"kallea\" date=\"1085145329\" format=\"1.0\"
version=\"1.4\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>LIBRARY REFERENCE: sleeping\</FONT\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Behavior](NIPCategoryBehavior)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:sleeping

\<font class=\"query\"\>DEPENDENCIES:\</font\> None.

\<font class=\"query\"\>COMPATIBILITY:\</font\> [MOOD](NIPHookRefMood)

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

The sleeping library features sleeping. A couple of properties can be
adjusted (see below) to determine the NPC\'s sleeping rhythm, etc. It
also features (if applicable) the mood \'SLEEPY\', which is loaded and
set accordingly, if [MOOD](NIPHookRefMood) is used.

\<font class=\"query\"\>DESCRIPTION\</font\>

Two separate states are introduced with the sleeping library, found in
the property **\"npc:state\"**. Initially, these are either
\"**awake**\" or \"**sleep**\".

If the NPC is asleep, the DELAY signal (which determines how much
resources the NPC uses) is substantially slowed down (four times slower,
to be exact).

\<font class=\"query\"\>NIP PROPERTIES\</font\>

\<font class=\"lib\"\>nip:trait:sleeping:effect\</font\> \<UL\> This
property decides how efficiently sleeping reduces weariness (increases
fatigue). \* 1 means the property is 100% efficient. If the NPC is awake
for 8 hours, it has to sleep for 8 hours to regain itself. \* 2 means
the property is 200% efficient. This is the default value, and is most
appropriate for a human. Awake for 16 hours, sleep for 8. \</UL\>

\<font class=\"lib\"\>nip:trait:sleeping:interval\</font\> \<UL\> The
interval property decides how weary the NPC can be before it goes to
bed. The NPC weariness is measured in \"seconds awake\". This property
is by default set to 57600 (16 hours). \</UL\>

\<font class=\"lib\"\>nip:trait:sleeping:states\</font\> \<UL\> Which
states are present. It is recommended, at least initially, to keep the
two states \"sleep\" and \"awake\". However, it is possible (but
untried) to remove or alter these states however you\'d like.\<BR\>
\</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:act:sleep:state\</font\> \<UL\> This
script is executed whenever the NPC changes state (awake/asleep) through
the usage of e.g. the library\'s own \<font
class=\"lib\"\>sleeping:decide\</font\>-script.\<br\> It will call the
appropriate handler in \'this\' (the NPC), namely
\"**merry:lib:handler:state:\<state\>**\"\<br\> \</UL\>

\<font class=\"lib\"\>merry:lib:handler:state:awake\</font\> \<UL\> The
standard awakening-script. It will emit a simple \"\<NPC\> wakes up.\",
set the state to awake and stance to \"standing\". \</UL\>

\<font class=\"lib\"\>merry:lib:handler:state:sleep\</font\> \<UL\> The
standard sleep-script. It will emit a simple \"\<NPC\> falls asleep.\",
set the state to asleep and stance to \"lying\". \</UL\>

\<font class=\"lib\"\>merry:lib:hook:init-post\</font\> \<UL\> This
script is attached to a special hook called \"hook\" which is triggered
whenever a hook is loaded, where \$HID is the hook ID. \</UL\>

\<font class=\"lib\"\>merry:lib:sleeping:decide\</font\> \<UL\> (Signal
DECIDE; hook sleeping)\<br\> This sig-hook-script will check whether the
NPC is, \* too tired to stay awake (in which case it will go to sleep)
\* rested enough to wake up (in which case it should wake up) Of course
depending on whether it is sleeping or if it\'s awake. \</UL\>

\<font class=\"lib\"\>merry:lib:sleeping:delay\</font\> \<UL\> (Signal
DELAY; hook sleeping)\<br\> This script will, if the NPC is sleeping,
multiply the delay time by four. This means the NPC will \"think\" four
times slower whilst asleep, than it would whilst awake. \</UL\>

\<font class=\"lib\"\>merry:lib:sleeping:internal\</font\> \<UL\>
(Signal INTERNAL; hook sleeping)\<br\> This script will increment
weariness if the NPC is awake, or decrement it if the NPC is sleeping.
\</UL\>

\<font class=\"lib\"\>merry:lib:sleeping:mood\</font\> \<UL\> (Signal
MOOD; hook sleeping)\<br\> This script will handle the mood \'SLEEPY\'
according to how tired the NPC is. \</UL\>

\-- Main.KalleAlm - 07 Jun 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
