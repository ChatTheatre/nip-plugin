%META:TOPICINFO{author=\"tonys\" date=\"1057834627\" format=\"1.0\"
version=\"1.7\"}% %META:TOPICPARENT{name=\"NIPRefLibraries\"}%
[NIPTodoStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>TODO: Mounting NPC\'s (e.g.
\"horseback-riding\")\</FONT\>

\<QUERY\>PROJECT STATUS\</QUERY\> WORKING

\<QUERY\>ASSIGNED CODER(S)\</QUERY\>

  --------------- ---------- ----------------------------
  **Who**         **From**   **Contact information**
  Main.KalleAlm   Marrach    <kalle@marrach.skotos.net>
  --------------- ---------- ----------------------------

\<QUERY\>WHAT?\</QUERY\> Mounting an NPC, like a horse or dragon or
whatever you\'d want to be able to mount.

\<QUERY\>PRIORITY\</QUERY\> HIGH

\<QUERY\>ETA?\</QUERY\> None.

\<QUERY\>HOW WILL IT WORK?\</QUERY\> Whenever someone jumps the NPC
(currently jump, will probably be changed into a separate verb,
\'mount\' perhaps, later on), the person will end up \'sitting on\' the
NPC. When they move around in the room, the NPC will move in their
stead. Likewise, movement between rooms will occur on the horse.

\<QUERY\>GENERAL DESCRIPTION\</QUERY\>

Mainly intended for horses (but will work equally well with anything
similar), the mounting lib will deal with the aspect of making it look
like (and keep it looking like) the rider (actor) is actually riding
around on the horse.

\<QUERY\>LIBRARIES\</QUERY\>

    [Library]         [Description]
    mounting            The general mounting lib
    mountrider       The shell lib containing the act-scripts for whoever mounts the horse.

\<QUERY\>TECHNICAL COMMENTS\</QUERY\>

The mounting lib will contain the main scripts for the horse, but these
scripts will only handle the mounting/un-mounting and nothing else. The
secondary library, mountrider, will contain act:approach/act:stance and
act:enter scripts that will be placed in the **rider** as they mount the
NPC, and will similarily be removed from the rider when the rider
unmounts again.

There is the issue of conflicting act-scripts (other act scripts placed
in the rider) which is an issue that may need to be addressed. **If you
are experiencing or having issues with such a thing, please notify
either of the coders listed for this project at once so it can be
addressed immediately.**

\<QUERY\>LIST OF INTERESTED PARTIES\</QUERY\>

If this subject interests you, please add yourself to the list below.
The more interest, the higher priority a subject will get. And also, by
doing so, we will be able to notify you specifically when this
subject\'s status has changed.

    [Your Name]      [Your Email]
    KathyNoble        katherin.noble@sbcglobal.net
    TonySmith           Disdercardo@blueyonder.co.uk

    [insert a separate line above this one]

\-- Main.KalleAlm - 04 Jun 2003

\<QUERY\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT THIS
SUBJECT\</QUERY\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
