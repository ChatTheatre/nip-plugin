%META:TOPICINFO{author=\"kallea\" date=\"1085145329\" format=\"1.0\"
version=\"1.4\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: Predator\</font\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Behavior](NIPCategoryBehavior)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:predator

\<font class=\"query\"\>DEPENDENCIES:\</font\> None.

\<font class=\"query\"\>COMPATIBILITY:\</font\>
[eating](NIPLibRefEating), [prey](NIPLibRefPrey),
[emoting](NIPLibRefEmoting), [sleeping](NIPLibRefSleeping)

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

The predator aspects of \"wildlife hunting NPC\'s\", like cats, wolves,
crocodiles, lions, snakes, etc.

\<font class=\"query\"\>DESCRIPTION\</font\>

The predator library gives the NPC the following features: \* Predator
attacking - that is, attacking prey, attempting to kill it. \* Eating
offers handler replacement - see Scavenger. \* Scavenger - the option of
whether the NPC is a scavenger or not. If not, (default) the NPC will
not accept nor take food that it **did not kill, itself**. \*
Agility/Offensive strength \"skills\" - a basic form of \"skills\"
system, used to define the various skills with which NPC\'s hunt prey.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

\<font class=\"lib\"\>nip:stats:agility\</font\> \<UL\> Integer,
defaults to: 10\<br\> The \'agility\' skill determines how fast the NPC
is. This skill is the only common skill that both prey and predator has,
which is used to determine if an NPC, despite offensive weakness, may
take down prey due to its speed. \</UL\>

\<font class=\"lib\"\>nip:behavior:predator\</font\> \<UL\> Object
pointer, defaults to: nil\<br\> This property should point to a data
object which contains the behavior data for the predator. This behavior
data is specific to predators, but may reside in a common behavior
object, if the NPC designer so wish.\<br\> The following mood/situation
need to be recorded for, in the behavior data object: \* KILL - When the
NPC kills a prey (\"break rat\'s neck sharply\")

(More moods/situations may occur in this later, if the system is
redefined/enhanced.) \</UL\>

\<font class=\"lib\"\>nip:stats:offense\</font\> \<UL\> Integer,
defaults to: 10\<br\> The offense skill is the actual skill used to
determine if the NPC successfully kills the intended prey, or if the
prey manages to defend itself. \</UL\>

\<font class=\"lib\"\>nip:trait:predator:prey\</font\> \<UL\> String
array, defaults to: ({ \"prey\" })\<br\> This property contains a list
of **all** types of prey that the NPC would regard as valid targets. For
example a cat\'s \"predator:prey\" value might look like this:\<pre\>({
\"prey\", \"rodent\", \"small\" })\</pre\> The predator\'s predator:prey
string array must contain **all** values which reside in the target
prey\'s prey:type.\<br\> (See [prey](NIPLibRefPrey), specifically the
nip:trait:prey:type property description, for more information on this.)
\</UL\>

\<font class=\"lib\"\>nip:trait:predator:scavenger\</font\> \<UL\>
Boolean, defaults to: 0 (FALSE)\<br\> The scavenger flag is set (1) if
the NPC is a scavenger. By default, an NPC only eats food which it
killed itself. \</UL\>

\<font class=\"lib\"\>nip:trait:predator:cannibal\</font\> \<UL\>
Boolean, defaults to: 0 (FALSE)\<br\> The cannibal flag is set (1) if
the NPC would consider other NPC\'s with the same urparent (of the same
type) as valid prey. \</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:act:predator:attack\</font\> \<UL\>
(DECIDE handler for attacking prey.)\<br\> This script calls the
\"defend\" handler in the prey, to see if the predator succeeds in
attacking the prey, or not. If the predator succeeds, the script acts
out a \"KILL\" behavior from the predator behavior, after which the
\"die\" script in the prey is called.

This script was intentionally kept as very simple and you are encouraged
to make your own replacement for this. A specific information page on
how to replace features in existing libraries is available
\[-BEING_WRITTEN-\]. \</UL\>

\<font class=\"lib\"\>merry:lib:handler:offer:eating\</font\> \<UL\>
(Replacement for the eating handler script in the
[eating](NIPLibRefEating) library.)\<br\> The predator eating offers
handler simply adds an additional check on whether or not the NPC is a
scavenger, and if it\'s not, the NPC makes sure that whatever offered
was originally killed by the NPC. \</UL\>

\<font class=\"lib\"\>merry:lib:hook:init-post\</font\> \<ul\> (NIP hook
init-post script.)\<br\> This script, called each time a new hook is
added, immediately replaces the eating offers handler (if the eating
hook is loaded) with its own. \</ul\>

\<font class=\"lib\"\>merry:lib:predator:decide\</font\> \<ul\> (Signal
DECIDE; hook predator)\<br\> This is the \"decide\" sig-hook script for
the predator hook. The system checks how hungry the NPC is (if
applicable), whether it\'s awake (if applicable), whether there is prey
in the area, and whether it matches the NPC predator\'s prey settings.
If the NPC finds valid prey, the predator:decide sig-hook will make it
attack. \</ul\>

\-- Main.KalleAlm - 20 Nov 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
