%META:TOPICINFO{author=\"kallea\" date=\"1143046199\" format=\"1.0\"
version=\"1.10\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: communicate\</font\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Behavior](NIPCategoryBehavior)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:communicate

\<font class=\"query\"\>DEPENDENCIES:\</font\>
[Emoting](NIPLibRefEmoting)

\<font class=\"query\"\>COMPATIBILITY:\</font\> [MOOD](NIPHookRefMood),
[omni-comm](NIPLibRefOmniComm)

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

NPC-to-PC response by verbal triggers.

\<font class=\"query\"\>DESCRIPTION\</font\>

Communicate, light version. Using a set of behavior recordings based on
response families, which in turn are individually constructed sentence
recognition arrays.

Additionally, each response family can be recorded for specific moods.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

\<font class=\"lib\"\>nip:trait:communicate:db\</font\> \<UL\> (Object
pointer.)\<br/\> Pointer to the data object in which the communicate
data is located, as well as the recorded behavior for the individual
families. \</UL\>

\<font class=\"lib\"\>nip:trait:communicate:log-to\</font\> \<UL\>
(Object pointer.)\<br/\> Optional pointer to an object in which entries
should be logged, whenever the NPC fails to comprehend something spoken
to it. This can be useful to in the long term improve the comprehension
levels of nippers by finding out what players ask about. The entries are
stored where the property is a UNIX timestamp of the date when the
question was asked, and in the format \"\[Describe(NPC)\] was asked by
\[Describe(actor)\] and failed to reply: \\\"\[evoke\]\\\"\". \</UL\>

\<font class=\"lib\"\>npc:comm:alt:\<family\>\</font\> \<UL\>
(String.)\<br/\> If \<family\> is triggered, and npc:comm:alt:\<family\>
exists, the behavior/situation called will be
\<family\>\<value\>.\<br/\> E.g. if the family \"i-love-you\" is
triggered, the system will look for the property
\"npc:comm:alt:i-love-you\" in the NPC. If \"npc:comm:alt:i-love-you\"
is set to e.g. \"-yes\" the family trigger will turn from \"i-love-you\"
into \"i-love-you-yes\" and if behavior data for \"i-love-you-yes\"
exists, it will be used instead. Additionally, the execution (if the
family is set to be \"executed\") will use the alternative name. Thus,
the script \"merry:lib:i-love-you-yes\" would be called. \</UL\>

\<font class=\"lib\"\>npc:comm:disabled:\<family\>\</font\> \<UL\>
(Boolean.)\<br/\> If \"npc:comm:disabled:\<family\>\" exists, \<family\>
will never be checked for a match. \</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:core:reply\</font\> \<UL\>
\<pre\>\"Process a sentence (\$evoke_to_npc) and return a result spoken
string.\"\</pre\> \</UL\>

\<font class=\"lib\"\>merry:lib:family_resolve\</font\> \<UL\>
\<pre\>\"Resolve a family array and return success/failure.

Required arguments: \$family: family data \$map_string: mapping with
string words to match \"\</pre\> \</UL\>

\<font
class=\"lib\"\>merry:react-post:evoke-dob%nip:communicate\</font\> and
\<font
class=\"lib\"\>merry:react-post:evoke-iob%nip:communicate\</font\>
\<UL\> \<pre\>\"Evoke response for the communicate lib.\"\</pre\>
\</UL\>

\-- Main.KalleAlm - 08 Dec 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)

This is pretty damn uninformative when someone wants to use it. More
docs..

\-- Main.KalleAlm - 23 Feb 2004

Fixed minor bug in family resolution.

Additionally, fixed dependency bug to include
[emoting](NIPLibRefEmoting). The system would crash without it.

\-- Main.KalleAlm - 23 Feb 2004

Fixed another bug and added [omni-comm](NIPLibRefOmniComm) as a
supplementary option.

\-- Main.KalleAlm - 24 Feb 2004

Added (previously) a few new features to this:

\* Property \"execute:\<family\>\" (boolean) - if set (1), a call to
\"merry:lib:\<family\>\" in the communications library will be made when
this family is triggered. \$npc is passed as an object representator of
the NPC object.

\* Behavior/situation \"\<family\>\<alternative\>:\<mood\>\" (behavior
data) - some complex communication requires that the NPC responds
differently at a given point. E.g. \"ask creature \'What is your
name?\'\" - creature responds with its name - \"ask creature \'What is
your name?\'\" - creature grunts \"I told you already\"

\* Property \"npc:comm:alt:\<family\>\" (string) - if set to anything
but nil, the behavior for \<family\> will be using the alternative
\<family\>\<alternative\>:\<mood\> behavior data (see above note).

\* Property \"npc:comm:disabled:\<family\>\" (boolean) - if set (1),
\<family\> is never checked for matches.

\-- Main.KalleAlm - 05 Mar 2004

Began docs ([NIPHowCommunication](NIPHowCommunication)). Also clarified
specification on the concept of alternative family executions.

\-- Main.KalleAlm - 24 Apr 2005

Added new tool, [comm](NIPToolComm), which is used to construct family
data.

\-- Main.KalleAlm - 15 May 2005

Modified code slightly. If behavior data is not found for a particular
family, the system will presume that FREEMOTE behavior data does exist.

Thus, freemotes in communication responses is currently disabled unless
no emote data exists. There are some issues with this (\"when should I
use what where? just because -this- family has freemote data doesn\'t
mean -that- one does. where should the frequency difference lie between
freemote and emote? on a per family level, per nipper level?\" and so on
and so forth).

\-- Main.KalleAlm - 07 Jun 2005

Added log-to feature.

\-- Main.KalleAlm - 22 Mar 2006
