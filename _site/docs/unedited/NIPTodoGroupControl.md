%META:TOPICINFO{author=\"soledadb\" date=\"1153754187\" format=\"1.0\"
version=\"1.5\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPTodoStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>TODO: Group control/behavior\</FONT\>

\<font class=\"query\"\>PROJECT STATUS\</font\> INITIATED

\<font class=\"query\"\>STATUS NOTES\</font\>

This system has been initiated.

\<font class=\"query\"\>ASSIGNED CODER(S)\</font\>

  --------------- ---------- ----------------------------
  **Who**         **From**   **Contact information**
  Main.KalleAlm   Skotos     <kalle@marrach.skotos.net>
  --------------- ---------- ----------------------------

\<font class=\"query\"\>WHAT?\</font\> NPC group control/behavior (the
masses).

\<font class=\"query\"\>PRIORITY\</font\> MEDIUM

\<font class=\"query\"\>ETA?\</font\> Mid-March, 2004.

\<font class=\"query\"\>HOW WILL IT WORK?\</font\>

The group/control NIP-system will use NPC\'s sorted into categories (by
the builder), such as \* 1. couriers \* 2. servants \* 3. commoners \*
4. men \* 5. humans

These categories will be used (in list order) to include NPC\'s into a
group, based on the group NPC\'s settings.

Settings would be things like \"minimum amount of NPC\'s in group\"
(before it\'s disbanded/required for it to be formed).

The system would also include and consider such things as factions. Two
NPC\'s from different factions would never merge into a single group.

NPC\'s that enter a group will be disabled (and actually transported out
of the environment) until the NPC\'s either leave the group (randomly
requested by the group itself), or if the group is disbanded.

\<font class=\"query\"\>GENERAL DESCRIPTION\</font\>

The system will be used to describe masses of people/whatever in an
environment, without keeping each and every NPC running and spamming the
environment with descriptions etc. The group would act as a mass of
NPC\'s on its own.

\<font class=\"query\"\>LIBRARIES\</font\>

    [Library]         [Description]
    group               The main group library, which will include features to
                          join/leave/disband/create groups, etc.

\<font class=\"query\"\>SIGNALS\</font\>

    [SIGNAL]            [Priority] [Description]
    GROUP-CONTROL    60000      The main group-control signal will check for NPC's to
                                         include in the group, and will force others to leave it
                                         at random.

\<font class=\"query\"\>HOOKS\</font\>

    [Hook]            [Using signals]             [Description]
    group-control    DELAY, GROUP-CONTROL       The sig-hook object for GROUP-CONTROL

\<font class=\"query\"\>TECHNICAL COMMENTS\</font\>

None, yet.

\<font class=\"query\"\>LIST OF INTERESTED PARTIES\</font\>

If this subject interests you, please add yourself to the list below.
The more interest, the higher priority a subject will get. And also, by
doing so, we will be able to notify you specifically when this
subject\'s status has changed.

    [Your Name]      [Your Email]
    Annie Warren!!! ocannee@mchsi.com 
    KathyN  katherin.noble@sbcglobal.net
    SoledadB reveur@marrach.skotos.net

    [insert a separate line above this one]

\-- Main.KalleAlm - 15 Nov 2003

\<font class=\"query\"\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT
THIS SUBJECT\</font\>\<br\> (Please, don\'t forget to add your name to
your comment, preferably your TWiki-name.)
