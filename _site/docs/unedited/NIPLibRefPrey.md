%META:TOPICINFO{author=\"kallea\" date=\"1154678452\" format=\"1.0\"
version=\"1.7\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: Prey\</font\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Behavior](NIPCategoryBehavior)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:prey

\<font class=\"query\"\>DEPENDENCIES:\</font\> None.

\<font class=\"query\"\>COMPATIBILITY:\</font\>
[Predator](NIPLibRefPredator), [emoting](NIPLibRefEmoting),
[sleeping](NIPLibRefSleeping), [death](NIPLibRefDeath).

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

The \'prey\' library is used to set an NPC up in various ways, so that
predator NPC\'s may target it and make dinner out of it.

\<font class=\"query\"\>DESCRIPTION\</font\>

The prey library implements the following features into the NPC: \*
Defending feature - (attempt to) defend against attacking predators. \*
Dying - and what to exactly turn the NPC into when slain. \*
Agility/Defense strength \"skills\" - a basic form of \"skills\" system,
used to define the various skills with which NPC\'s defend against
predators.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

\<font class=\"lib\"\>nip:behavior:prey\</font\> \<UL\> Object pointer,
defaults to: nil\<br\> This property should point to the behavior data
object of the NPC, which should contain data for the following
moods/situations: \* EVADE - For when the NPC successfully avoids an
attacking predator. \</UL\>

\<font class=\"lib\"\>nip:stats:agility\</font\> \<UL\> Integer,
defaults to: 10\<br\> Agility, speed, haste, the NPC\'s ability to avoid
being eaten through force of speed. This property is used to determine
whether or not the predator receives a bonus to its attack. This occurs
if the attacking predator\'s agility roll falls above the prey\'s
agility roll. \</UL\>

\<font class=\"lib\"\>nip:stats:defense\</font\> \<UL\> Integer,
defaults to: 10\<br\> The defensive skill of the NPC. If the attacking
predator\'s offense roll (including potential bonuses for agility rolls)
falls below the defending prey\'s defense roll, the prey evades the
attack, and survives. If the offense roll is higher than the defense
roll, the prey is caught and slain by the predator. \</UL\>

\<font class=\"lib\"\>nip:trait:prey:chunk-object\</font\> \<UL\> Object
pointer, defaults to: \<Lib:NIP:EXT:prey-chunk\>\<br/\> The pointer to
the object which is to be spawned as a chunk of meat for this animal.
\</UL\>

\<font class=\"lib\"\>nip:trait:prey:dead\</font\> \<UL\> Deprecated:
use [death](NIPLibRefDeath) library\'s nip:trait:death:dead property.

Object pointer, defaults to: nil\<br/\> This optional property can be
set to a version of the NPC which is its \"dead state.\" This other
object mustn\'t be a nipper, in fact, it is recommended that it isn\'t
(dead things don\'t interact very well anyway). If this property is set,
the nipper will change its UrParent to the object defined in
\"nip:trait:prey:dead\" rather than try to find alteration solutions to
itself. \</UL\>

\<font class=\"lib\"\>nip:trait:prey:descripts\</font\> \<UL\> Integer,
defaults to: 3\<br/\> Number of description types for the prey, once it
has been killed. This can be used to create SAM {?when \| \... }
constructs to describe the various states of the animal as it is being
ripped to shreds by its predators. \</UL\>

\<font class=\"lib\"\>nip:trait:prey:dead-chunks\</font\> \<UL\>
Integer, defaults to: nil\<br/\> Number of chunks before an animal has
been \"stripped\" of meat. The higher this value, the more chunks
animals will be able to rip out of it before it\'s clean. \</UL\>

\<font class=\"lib\"\>nip:trait:prey:type\</font\> \<UL\> String array,
defaults to: ({ \"prey\" })\<br\> This property contains a list of the
\"classes\" that this NPC is a part of. It is important to realize that
each and every one of these classes must be found in the predator\'s
predator:prey string array. However, the reverse is not the case, which
means a predator may have more prey types in its list, while a prey is
considered invalid if it has a single type the predator does not have.
\<br\> In the [predator](NIPLibRefPredator) library, I gave an example
of a cat with the predator:prey set to:\<pre\>({ \"prey\", \"rodent\",
\"small\" })\</pre\>\<br\> If for instance a mouse had the prey
\"nip:trait:prey:type\" value set to either of:\<pre\> - ({ \"prey\" })
- ({ \"rodent\" }) - ({ \"small\" }) - ({ \"prey\", \"rodent\" }) - ({
\"prey\", \"small\" }) - ({ \"rodent\", \"small\" }) - ({ \"prey\",
\"rodent\", \"small\" })\</pre\> then it would be valid prey for the
cat. However, if it had e.g.:\<pre\>({ \"prey\", \"rodent\", \"mouse\"
})\</pre\>it would no longer be valid prey, since the cat didn\'t have
the \"mouse\" value in its list. \</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:act:nip/die\</font\> \<UL\>
\<pre\>\"Die.\"\</pre\>

This is a simple placeholder action that shuts the nipper down and marks
it as dead. There is at the point of writing one alternative that will
extend this functionality, and that is the library
[death](NIPLibRefDeath). The [death](NIPLibRefDeath) library description
goes:

This script will do a *bunch* of things to make your NPC look dead.
First of all, it disables the heartbeat thread if one is running.
Secondly, it attempts to disable scriptrunning, and it also unsets
volition in the object.

The volition aspect brings up another point that you need to be aware of
in this case, which is the fact that none of the parents for a prey NPC
must have volition set. This means the NPC will look very odd when
summoned, but when spawned, the NPC will look \"correct.\"

Furthermore, the script will attempt to change the NPC\'s description
into a more \"unwell\" look. Unless a specific look and/or examine
description exists, these values will remain as is. But the brief will
be examined and a somewhat good guess will be made to change it
appropriately. Further documentation on this subject will be available
shortly. \</UL\>

\<font class=\"lib\"\>merry:lib:handler:prey:defend\</font\> \<UL\>
\<pre\>\"The prey defend script, which calculates the outcome of a
hunter/prey situation.

The following arguments are expected: \$predator: (object pointer) The
hunting/attacking NPC object. \$offense: (integer) The hunter\'s
offensive strength. \$agility: (integer) The hunter\'s agility.

Return value: TRUE if hunter successfully attacks prey, and FALSE if
hunter fails.\"\</pre\>

The prey:defend handler is used to determine whether or not a
predator\'s attack on a prey NPC succeeds. This script is, again, very
simple, and is so for a reason. And I encourage you to replace it with
your own feature if you require a more complicated check for this.
Personally, I think this works, since we\'re not aiming for a \"complete
simulation\", but more the \"illusion.\" \[-BEING_WRITTEN-\] \</UL\>

\<font class=\"lib\"\>merry:lib:handler:prey:die\</font\> \<UL\>
\<pre\>\"The prey die script, which turns an NPC into a dead
body.\"\</pre\>

This script used to handle decaying and such, of bodies, but this
functionality now resides in the [death](NIPLibRefDeath) library\'s
act:nip/die script.

*In order to obtain the previously-default death behavior for nippers
using this library, you must now add the death library as well.*

This script will hand over control to the \"nip/die\" action in the
nipper. \</UL\>

\<font class=\"lib\"\>merry:lib:handler:start:prey\</font\> \<UL\> This
is a start handler for the NPC act:start feature (spawn). \</UL\>

\<font class=\"lib\"\>merry:lib:init\</font\> \<UL\> (NIP library init
script.)\<br\> This script will unset volition in the object, as well as
add the \"start:prey\" handler to the act:start script chain. \</UL\>

\-- Main.KalleAlm - 20 Nov 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)

Added \"nip:trait:prey:dead\" property w/ functionality.

\-- Main.KalleAlm - 01 Mar 2004

Added the whole chunk-feature which allows predators to rip chunks of
flesh out of prey. Ew.

\-- Main.KalleAlm - 14 Feb 2006

Extracted \"die\" handler from this library and turned it into its own
library, called [death](NIPLibRefDeath).

Main.KalleAlm Aug 3 06.
