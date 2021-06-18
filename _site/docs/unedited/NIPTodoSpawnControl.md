%META:TOPICINFO{author=\"kallea\" date=\"1069812273\" format=\"1.0\"
version=\"1.4\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPTodoStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>TODO: Spawn control\</FONT\>

\<font class=\"query\"\>PROJECT STATUS\</font\> IMPLEMENTED

\<font class=\"query\"\>STATUS NOTES\</font\>

This has been implemented (see [update reference \#9](NIPUpdateRef9) for
further information), and additionally the NIP and NIP-CORE-namespaces
have been auto-exported.

\<font class=\"query\"\>ASSIGNED CODER(S)\</font\>

  --------------- ---------- ----------------------------
  **Who**         **From**   **Contact information**
  Main.KalleAlm   Skotos     <kalle@marrach.skotos.net>
  --------------- ---------- ----------------------------

\<font class=\"query\"\>WHAT?\</font\> The aspect of +spawning NPC\'s.

\<font class=\"query\"\>PRIORITY\</font\> VERY HIGH

\<font class=\"query\"\>ETA?\</font\> September, 2003.

\<font class=\"query\"\>HOW WILL IT WORK?\</font\>

The spawn control feature would add a trigger to the core NPC library
(Lib:NIP:core) which would be executed whenever an NPC was spawned.

\<font class=\"query\"\>GENERAL DESCRIPTION\</font\>

Spawning an NPC is currently impossible. The original NPC object is the
only one working, and this is needless to say, a very bad thing.

\<font class=\"query\"\>TECHNICAL COMMENTS\</font\>

This script will create a \'act:start\' script in the core library and
this would also be added to the \"initial functions\" system property.

Note that this is not [the spawn system](NIPTodoSpawnSystem) albeit the
name may be misleading. (the spawn system library was named
\"spawn-control\")

\<font class=\"query\"\>LIST OF INTERESTED PARTIES\</font\>

If this subject interests you, please add yourself to the list below.
The more interest, the higher priority a subject will get. And also, by
doing so, we will be able to notify you specifically when this
subject\'s status has changed.

    [Your Name]      [Your Email]
    [insert a separate line above this one]

\-- Main.KalleAlm - 04 Nov 2003

\<font class=\"query\"\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT
THIS SUBJECT\</font\>\<br\> (Please, don\'t forget to add your name to
your comment, preferably your TWiki-name.)
