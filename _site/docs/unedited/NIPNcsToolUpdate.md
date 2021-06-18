%META:TOPICINFO{author=\"kallea\" date=\"1115918039\" format=\"1.0\"
version=\"1.1\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPToolStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>+NCS TOOL: Update\</font\>

\<font class=\"query\"\>SYNTAX:\</font\>

`+ncs update`

\<font class=\"query\"\>AFFECTED / CONCERNED LIBS/ETC.:\</font\>

All.

\<font class=\"query\"\>GENERAL DESCRIPTION:\</font\>

The `+ncs update` command is specifically used to update all running
nippers \"on-the-fly.\" This is vital to live environments when a new
update has been released. The system attempts to figure out which is the
actual master NPC object, but sometimes this fails. As such, it is a
good idea to have a special room in which all the game\'s master NPC
objects are located. A host could then teleport to that room and perform
a +nip \<npc\'s\> \"update\" to ensure that all the masters are updated.

The introduction of `+ncs update` ensures that any running NPC is using
the latest update.

\-- Main.KalleAlm - 12 May 2005

\<font class=\"query\"\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT
THIS SUBJECT\</font\>\<br/\> (Please, don\'t forget to add your name to
your comment, preferably your TWiki-name.)
