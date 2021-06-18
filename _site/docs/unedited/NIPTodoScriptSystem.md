%META:TOPICINFO{author=\"kallea\" date=\"1092840866\" format=\"1.0\"
version=\"1.4\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPTodoStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>TODO: Script system\</FONT\>

\<font class=\"query\"\>PROJECT STATUS\</font\> COMPLETED

\<font class=\"query\"\>STATUS NOTES\</font\>

See [library: replaying](NIPLibRefReplaying).

Replaying and recording updated. New +nip tools added
(connect/disconnect). A wide range of documentation is available on this
topic.

\<font class=\"query\"\>ASSIGNED CODER(S)\</font\>

  --------------- ---------- -----------------------------
  **Who**         **From**   **Contact information**
  Main.KalleAlm   Skotos     <kalle@mortalis.skotos.net>
  --------------- ---------- -----------------------------

\<font class=\"query\"\>WHAT?\</font\> A script system for prerecorded
interaction between NPC\'s.

\<font class=\"query\"\>PRIORITY\</font\> MEDIUM

\<font class=\"query\"\>ETA?\</font\> Completed May 21st, 2004.

\<font class=\"query\"\>HOW WILL IT WORK?\</font\>

**Deployment:**

The system is intended to create scenes between NPC\'s, by creating a
scene, and initiating a recording session in both NPC\'s.

A new control character (\'@\') will be introduced into the recording
system, and will be used to determine delays between actions.

A behavior data object will be used for each participating nipper, and
an external data target will be used to store script-specific
information (such as delays, behavior objects, scenario symbols, etc).

\<font class=\"query\"\>GENERAL DESCRIPTION\</font\>

**Functionality:**

This library/tool will first and foremost be used in situations where
NPC \"scenes\" need to be replayed. Due to the static nature of
prerecording the events, it is not recommended for use in situations
where a player may wish to alter the course of the scene, as such will
be ignored.

\<font class=\"query\"\>TECHNICAL COMMENTS\</font\>

This is mostly a tool, rather than an actual library. It involves an
extension of the recording tool, and a new +NIP-tool (available through
a Merry-call as well).

The \"replaying\" library need to be loaded in at the NPC which
initiates the playback of the recording. All other NPC\'s only need the
appropriate appearance libraries.

\<font class=\"query\"\>LIST OF INTERESTED PARTIES\</font\>

If this subject interests you, please add yourself to the list below.
The more interest, the higher priority a subject will get. And also, by
doing so, we will be able to notify you specifically when this
subject\'s status has changed.

    [Your Name]      [Your Email]
    [insert a separate line above this one]

\-- Main.KalleAlm - 24 Feb 2004

\<font class=\"query\"\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT
THIS SUBJECT\</font\>\<br\> (Please, don\'t forget to add your name to
your comment, preferably your TWiki-name.)
