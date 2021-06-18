%META:TOPICINFO{author=\"kallea\" date=\"1065796492\" format=\"1.0\"
version=\"1.1\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPToolStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>+NIP TOOL: Update\</FONT\>

\<QUERY\>SYNTAX:\</QUERY\>

    +nip &lt;npc> "update"

\<QUERY\>AFFECTED / CONCERNED LIBS/ETC.:\</QUERY\>

None/All.

\<QUERY\>GENERAL DESCRIPTION:\</QUERY\>

Perform any NIP updates on the target NPC manually.

Do note that this feature occurs automatically whenever an NPC is
(re-)started (see [+NIP TOOL: Live](NIPToolLive)). However, some NPC\'s
heartbeat threads are never executed and thus, this update tool was
made.

Further note that if an NPC crashes within a minute of the execution of
an update, this may be due to instability caused by (cached) process
data, which is resolved by restarting the NPC. To ensure stability,
update the NPC by stopping and restarting the heartbeat thread (again,
see [+NIP TOOL: Live](NIPToolLive)).

\-- Main.KalleAlm - 10 Oct 2003

\<QUERY\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT THIS
SUBJECT\</QUERY\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
