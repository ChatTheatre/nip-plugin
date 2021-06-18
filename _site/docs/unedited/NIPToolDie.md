%META:TOPICINFO{author=\"kallea\" date=\"1058383145\" format=\"1.0\"
version=\"1.1\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPToolStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>+NIP TOOL: die\</FONT\>

\<QUERY\>SYNTAX:\</QUERY\> +nip \<npc\> \"die\"

\<QUERY\>AFFECTED / CONCERNED LIBS/ETC.:\</QUERY\> None.

\<QUERY\>GENERAL DESCRIPTION:\</QUERY\>

\'die\' is used to signal to an NPC that it should shut down. This
feature is indirect, in that it only informs the NPC\'s heartbeat thread
that it has to go down. The heartbeat thread **will finish whatever
it\'s working with** before shutting down.

\-- Main.KalleAlm - 16 Jul 2003

\<QUERY\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT THIS
SUBJECT\</QUERY\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
