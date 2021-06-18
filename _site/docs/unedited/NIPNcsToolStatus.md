%META:TOPICINFO{author=\"kallea\" date=\"1092251077\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPToolStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>+NCS TOOL: STATUS\</FONT\>

\<font class=\"query\"\>SYNTAX:\</font\> +ncs status

\<font class=\"query\"\>AFFECTED / CONCERNED LIBS/ETC.:\</font\> All NIP
NPC\'s running a heartbeat.

\<font class=\"query\"\>GENERAL DESCRIPTION:\</font\>

The STATUS command is used to receive general information on the
currently running NPC\'s in the game. E.g.:

    --
    > +ncs status

    +----------+----------------------+-------+---------+--------------+-----------------+
    |    ID  |       Location        | State |  Mood    |   Runtime  |       Age         |
    +----------+----------------------+-------+---------+--------------+-----------------+
    | kitten-0 | StoryPlotter Clothos | awake | NEUTRAL |  17h 38m 11s | 44d 20h 28m 23s |
    +----------+----------------------+-------+---------+--------------+-----------------+
    --

\-- Main.KalleAlm - 18 Nov 2003

\<font class=\"query\"\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT
THIS SUBJECT\</font\>\<br\> (Please, don\'t forget to add your name to
your comment, preferably your TWiki-name.)
%META:TOPICMOVED{by=\"kallea\" date=\"1092251077\"
from=\"Builders.NCSToolStatus\" to=\"Builders.NIPNcsToolStatus\"}%
