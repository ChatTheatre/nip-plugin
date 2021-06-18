%META:TOPICINFO{author=\"kallea\" date=\"1085250064\" format=\"1.0\"
version=\"1.4\"}% %META:TOPICPARENT{name=\"NIPChangeLog\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: replaying\</font\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Appearance](NIPCategoryAppearance)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:replaying

\<font class=\"query\"\>DEPENDENCIES:\</font\>
[emoting](NIPLibRefEmoting)

\<font class=\"query\"\>COMPATIBILITY:\</font\> None/All.

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None known.

\<font class=\"query\"\>KNOWN ISSUES:\</font\>

Confirmed () issues with this library. (Unconfirmed issues should be
reported in the feedback section at the bottom of this document.)

\<font class=\"query\"\>FEATURES\</font\>

Replaying of NPC behavior data in order (as opposed to \'randomly\').

\<font class=\"query\"\>DESCRIPTION\</font\>

Functionality to replay pre-recorded NPC parser usage, freemotes and
delays (pauses).

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:handler_replay\</font\> \<UL\> The
replay handler, called from within the NPC as such,
`::handler_replay( $db: ${object}, $scene: "string" )`.

The replay handler will require the existence of the tracking link
vector in order to function properly. \</UL\>

\-- Main.KalleAlm - 19 May 2004

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
