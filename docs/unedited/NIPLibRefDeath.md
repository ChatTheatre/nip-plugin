%META:TOPICINFO{author=\"kallea\" date=\"1161785832\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: death\</font\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Behavior](NIPCategoryBehavior)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:death

\<font class=\"query\"\>DEPENDENCIES:\</font\> None.

\<font class=\"query\"\>COMPATIBILITY:\</font\> [Prey](NIPLibRefPrey),
[fighting-fake](NIPLibRefFightingFake).

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>KNOWN ISSUES:\</font\>

Confirmed () issues with this library. (Unconfirmed issues should be
reported in the feedback section at the bottom of this document.)

\<font class=\"query\"\>FEATURES\</font\>

Extends the \"death\" concept of libraries to include decaying and
rotting and, eventually, disintegration of the nipper after it has been
killed and left in-game (as opposed to it being killed and gutted or
eaten or whatever).

\<font class=\"query\"\>DESCRIPTION\</font\>

The \'death\' library adds a single action handler called
\'act:nip/die\', which overrides existing act:nip/die inherits. The
nip/die action shuts the nipper down and puts it through a process of
decaying, rotting, and disintegration specified via a number of
specialized description types. These types are: \* dead-examine \*
dead-look \* dead-brief \* dead-pbrief \* rotting-brief \*
rotting-examine \* rotting-look \* rotting-pbrief \* skeleton-brief \*
skeleton-examine \* skeleton-look \* skeleton-pbrief

If these descriptions are found in the killable nipper, they will
replace the descriptions when the nipper enters the \"stage\" in
question. The stages are: \* dead \* rotting \* skeleton

The time interval between each stage can be defined using the
\"nip:trait:death:XXX_time\" properties (see NIP PROPERTIES section for
further information), and default to: \* dead -\> rotting in 1 day
(86400 seconds). \* rotting -\> skeleton in 3.5 days (302400 seconds).
\* skeleton -\> disintegrates in 1 week (604800 seconds).

\<font class=\"query\"\>NIP PROPERTIES\</font\>

`object <font class="lib">nip:trait:death:dead</font>` \<ul\> When the
nipper dies, if this property is set to a valid object, the nipper\'s
UrParent will be set to the object in question, and the remaining
functionality of the death library will be disabled. \</ul\>

`int <font class="lib">nip:trait:death:rot_time</font>` \<ul\> The
number of seconds from the point of death that it will take before this
nipper begins to use the \'rotten\' descriptions. \</ul\>

`int <font class="lib">nip:trait:death:skeleton_time</font>` \<ul\> The
number of seconds it will take for this nipper to go from the rotting
state to the skeleton state. \</ul\>

`int <font class="lib">nip:trait:death:disintegrate_time</font>` \<ul\>
The number of seconds it will take for this nipper to go from the
skeleton state to it disintegrating (read: it is slain). \</ul\>

`boolean <font class="lib">npc:is_dead</font>` \<ul\> If this property
is **unset** while the death library is processing the nipper, the death
processing is aborted. The death library sets this property upon
initializing. \</ul\>

`int <font class="lib">npc:death:time</font>` \<ul\> Timestamp when the
nipper died. \</ul\>

`int <font class="lib">npc:death:state</font>` \<ul\> State of the
nipper\'s decaying. \* 1 = freshly dead \* 2 = rotten \* 3 = skeleton
\</ul\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:act:nip/die\</font\> \<ul\> Perform the
rotting, skeleton-turning, and disintegration of the nipper. \</ul\>

\-- Main.KalleAlm - 03 Aug 2006

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br/\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)

Fixed bug where death-but-not-prey nippers did not properly lose
volition upon death.

Main.KalleAlm 2006-10-25.
