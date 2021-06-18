%META:TOPICINFO{author=\"kallea\" date=\"1067892540\" format=\"1.0\"
version=\"1.1\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
\<UpdateIssue\> [NIPUpdateRefStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>SYSTEM ISSUE \#9:\</FONT\>

\<font class=\"query\"\>DATE:\</font\> Nov 1st, 2003.

\<font class=\"query\"\>UPDATE AFFECTS:\</font\> All NPC\'s.

\<font class=\"query\"\>UPDATED BY:\</font\> Main.KalleAlm

\<font class=\"query\"\>PROBLEM\</font\>

Pre-update \#9, NIP would handle spawning of NPC\'s in a
brute-force-copy NIP and NIP-CORE namespace properties down into the
child. This worked, but had a few side-effects that were undesirable.

For instance, urinheritage was completely discarded this way. Also, any
updates to the parent of the spawn(s) would **not** be applied to the
child automagically. This resulted in some complications for instance
when an NPC with a lot of spawns had to be modified. The procedure to do
this would involve having to slay and re-spawn all the children, thereby
losing all their then-customized data.

\<font class=\"query\"\>REQUIRED USER-MEASURES\</font\>

This update is automatic, but will, despite this, require some user
interaction to be fully incorporated into NPC\'s. Your NPC\'s have
probably crashed. Or, new spawns of NPC\'s will crash with an error
output similar to the following:

    --
    <b>Index on bad type</b>
    /base/obj/thing#105072 [NIP:bodies:servants:guard:short-male]#105072
    53 /core/lib/core_scripts perform_delayed_call
    /usr/SkotOS/data/mcontext#-1
    35 /usr/SkotOS/data/mcontext merry_continuation
    100 /usr/SkotOS/lib/merryapi run_merry
    /usr/SkotOS/data/merry#-1
    243 /usr/SkotOS/data/merry evaluate
    /usr/SkotOS/merry/9e259fba01208029b7e4423a352c0f75 M<[NIP:bodies:servants:guard:short-male]#105072/lib:core:sysupdate>
    67 /usr/SkotOS/lib/merrynode evaluate
    27 /usr/SkotOS/merry/9e259fba01208029b7e4423a352c0f75 merry
    400 /usr/SkotOS/lib/merrynode Call
    100 /usr/SkotOS/lib/merryapi run_merry
    /usr/SkotOS/data/merry#-1
    243 /usr/SkotOS/data/merry evaluate
    /usr/SkotOS/merry/9a1238ccb728625f20f86b9f2f556a9f M<[NIP:bodies:servants:guard:short-male]#105072/lib:update:5>
    67 /usr/SkotOS/lib/merrynode evaluate
    12 /usr/SkotOS/merry/9a1238ccb728625f20f86b9f2f556a9f merry
    ---

When this occurs, you will need to summon the parent NPC, and update it.
This is done the following way:

\* 1. +summon npc:woe:name \* 2. +nip *NPC* \"update\" \* 3. +unsummon
npc:woe:name

All spawns of the NPC must be destroyed and re-created. This is a
one-timer, and an unfortunate one. After all, this is what this issue is
here to deal with \-- so that we won\'t ever have to slay spawns again.

\<font class=\"query\"\>SOLUTION\</font\>

This was solved by exporting the namespaces NIP and NIP-CORE. This is
done automatically. A *coder* doesn\'t have to worry about this update
at all. He/She can still set NIP and NIP-CORE properties as he pleases,
and these will be transferred to the exported namespace automatically.
They will additionally be available as usual through the NIP or NIP-CORE
namespaces, as exported properties are, naturally.

\-- Main.KalleAlm - 03 Nov 2003

\<font class=\"query\"\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT
THIS SUBJECT\</font\>\<br\> (Please, don\'t forget to add your name to
your comment, preferably your TWiki-name.)
