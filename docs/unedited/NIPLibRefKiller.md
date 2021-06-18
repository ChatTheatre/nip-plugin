%META:TOPICINFO{author=\"kallea\" date=\"1085145486\" format=\"1.0\"
version=\"1.7\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: killer\</font\>

\<font class=\"query\"\>CATEGORY:\</font\> [Service](NIPCategoryService)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:killer

\<font class=\"query\"\>DEPENDENCIES:\</font\>
[wounding](NIPLibRefWounding), [movement](NIPLibRefMovement),
[predator](NIPLibRefPredator)

\<font class=\"query\"\>COMPATIBILITY:\</font\>
[eating](NIPLibRefEating), [emoting](NIPLibRefEmoting),
[freemoting](NIPLibRefFreemoting)

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None/All.

\<font class=\"query\"\>KNOWN ISSUES:\</font\>

Confirmed () issues with this library. (Unconfirmed issues should be
reported in the feedback section at the bottom of this document.)

\<font class=\"query\"\>FEATURES\</font\>

PC-wounding NPC default library.

\<font class=\"query\"\>DESCRIPTION\</font\>

Killer is as much an example as it is a functional library. It is used
to determine whether a nipper will attack or flee from a \'living\'
being (volitional). The core is based off of hunger, which means, if the
nipper is hungry enough, it\'ll attack **anything**. If it\'s not
hungry, it will most likely flee from the scene if it encounters another
living being.

If the [eating](NIPLibRefEating) library is not used, the NPC will
always attack if it encounters a volitional being.

This is based off of a \"wild\" animal, and should probably not be used
(unless modified accordingly) with any tame nippers.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

`pointer <font class="lib">nip:behavior:killer</font>` \<UL\> If set to
a woe object reference, behavior for \'ATTACK\' may be recorded and will
then be used whenever a nipper attacks a PC. The \"victim\" scene object
role must be set to a subject representing the target during recording.
[(further information on sceneries)](NIPTutorialScenery)

Take note that if set, the system presumes [emoting](NIPLibRefEmoting)
is enabled. A crash will occur if this is not the case and this property
is set. \</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

`<font class="lib">merry:lib:predator:decide</font>` \<UL\>
(Modification to [predator](NIPLibRefPredator) script.)\<br/\> All of
the predatorial behavior, with the additional \"fight or flight\"
behavior of the killer library. \</UL\>

\-- Main.KalleAlm - 29 Mar 2004

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)

Looks fantastic! Can\'t wait to try it out. Will there be a separate
library possible for domestic beasts? For example, in Oasis, we have
camels and donkeys that probably wouldn\'t bite unless they were
particularly mean or provoked. But I can see applications of a
\"gentler\" version of this library for domestic beasts (dogs, cats,
horses, etc.). \-- Main.ToddNilson - 30 Mar 2004

That would definitely be possible, but would most likely be an entirely
different NIP library. This is for \"predators\" in the hunting aspect,
while what you talk about is more along the lines of \"provoced
reactions\". \-- Main.KalleAlm - 30 Mar 2004

Minor bug fix. Currently, the killer lib is outside of the consent
boundaries, for obvious reasons. Games that have \"risks\" wouldn\'t be
very risky if the NPC nicely asked for consent to wound the adventurous
adventurer, now would they? :) But if the need for a consent-based
killer-lib is something we want, it can be arranged. \-- Main.KalleAlm -
17 May 2004
