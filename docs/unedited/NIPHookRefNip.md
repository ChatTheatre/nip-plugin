%META:TOPICINFO{author=\"kallea\" date=\"1068727315\" format=\"1.0\"
version=\"1.1\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>SIGNAL/HOOK REFERENCE: NIP\</FONT\>

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:hooks:nip

\<font class=\"query\"\>HOOK(S):\</font\> nip

\<font class=\"query\"\>COMPATIBILITY:\</font\>
[interaction](NIPLibRefInteraction)

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>MAIN PURPOSE\</font\>

To submit and/or to accept interaction requests.

\<font class=\"query\"\>DESCRIPTION\</font\>

This is the hook used by [the interaction library](NIPLibRefInteraction)
to request/accept interaction with other NPC\'s in the room.

\<font class=\"query\"\>SIGNAL/HOOK SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:nip:decide\</font\> \<UL\> (Hook
\'nip\'; signal \'DECIDE\')

\"This sig-hook looks for broadcasts from other NPC\'s in the room. If
it finds one, it has appropriate behavior set up, and if it decides to
grab it, it will interact with that NPC.\" \</UL\>

\<font class=\"lib\"\>merry:lib:nip:internal\</font\> \<UL\> (Hook
\'nip\'; signal \'INTERNAL\')

\"This sig-hook is responsible for broadcasting the NPC\'s wish to
interact with any other NPC in the same room.\" \</UL\>

\-- Main.KalleAlm - 13 Nov 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
