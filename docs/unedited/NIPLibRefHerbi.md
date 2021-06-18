%META:TOPICINFO{author=\"kallea\" date=\"1085145486\" format=\"1.0\"
version=\"1.4\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: herbi\</font\>

\<font class=\"query\"\>CATEGORY:\</font\> [Service](NIPCategoryService)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:herbi

\<font class=\"query\"\>DEPENDENCIES:\</font\> None.

\<font class=\"query\"\>COMPATIBILITY:\</font\>
[predator](NIPLibRefPredator)

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> [prey](NIPLibRefPrey)

\<font class=\"query\"\>KNOWN ISSUES:\</font\>

Confirmed () issues with this library. (Unconfirmed issues should be
reported in the feedback section at the bottom of this document.)

\<font class=\"query\"\>FEATURES\</font\>

NPC library, for use by herbivores to extract food from plants. (used in
the PLANT, not the NPC)

\<font class=\"query\"\>DESCRIPTION\</font\>

When \"attacked,\" the herbi library spawns a specific object and places
it in the NPC attacker\'s hands.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

\<font class=\"lib\"\>nip:trait:herbi:extract\</font\> \<UL\> (Object
pointer.)\<br/\> The pointer to the object that should be spawned when
the NPC is attacked. \</UL\>

\<font class=\"lib\"\>nip:trait:herbi:message\</font\> \<UL\>
(String.)\<br/\> Optional. Set this to the message that should be
emitted when an NPC extracts from the herb NPC plant. Keywords
are:\<pre\> - (npc) Extracts into Describe(npc) E.g. \"a cow\" - (prey)
Extracts into Describe(extract) E.g. \"a mouthful of grass\" - (room)
Extracts into Describe(env) E.g. \"the field\" E.g. \"(npc) finds (prey)
in (room).\" would result in \"A cow finds a mouthful of grass in the
field.\"\</pre\> \</UL\>

\<font class=\"lib\"\>nip:trait:prey:type\</font\> \<UL\> (String
array.)\<br/\> The prey type list. By default set to ({ \"plant\" }),
but can be defined more accurately to distinguish plants from each
other, by whatever classification, so that herbivores can be more
selective in their food. \</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:handler:prey:defend\</font\> \<UL\>
Dummy-script for equality with [prey](NIPLibRefPrey) and compatibility
with [predator](NIPLibRefPredator) which returns \"always success.\"
\</UL\>

\<font class=\"lib\"\>merry:lib:handler:prey:die\</font\> \<UL\> This
script spawns the extract object and places it in the hands of the
attacker. \</UL\>

\-- Main.KalleAlm - 01 Mar 2004

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)

Added \"nip:trait:herbi:message\" property.

\-- Main.KalleAlm - 03 Mar 2004
