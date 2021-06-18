%META:TOPICINFO{author=\"kallea\" date=\"1076983761\" format=\"1.0\"
version=\"1.1\"}% \<UpdateIssue\> [NIPUpdateRefStyle]{.twiki-macro
.INCLUDE}

\<FONT CLASS=\"title\"\>SYSTEM ISSUE \#17:\</FONT\>

\<font class=\"query\"\>DATE:\</font\> Feb 17th, 2004

\<font class=\"query\"\>UPDATE AFFECTS:\</font\>
[freemoting](NIPLibRefFreemoting)

\<font class=\"query\"\>UPDATED BY:\</font\> Main.KalleAlm

\<font class=\"query\"\>PROBLEM\</font\>

Not really a problem, more like an insane solution to a problem that
lead to a lot of issues. That added to the feature being poorly
documented lead me to decide to rip the feature out entirely. This in
turn lead to some incompatibilities, which rendered this update
necessary.

The issue in question is the fact that \'freemoting\' behavior data
objects were supposed to be named \"nip:behavior:freemoting:\*\", while
regular \'emoting\' behavior data objects were named
\'nip:behavior:\*\". A lot of people failed to realize that they had to
set both an \"emoting\" and a \"freemoting\" property-reference.

\<font class=\"query\"\>REQUIRED USER-MEASURES\</font\>

None.

\<font class=\"query\"\>SOLUTION\</font\>

Thus, the freemoting library will now look for the
\"nip:behavior:\*\"-property, instead.

Since some have set the \"nip:behavior:**freemoting**:\*\"-properties
already, the update goes through any NPC with freemoting set, and moves
this (if applicable) to \"nip:behavior:\*\".

\-- Main.KalleAlm - 16 Feb 2004

\<font class=\"query\"\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT
THIS SUBJECT\</font\>\<br\> (Please, don\'t forget to add your name to
your comment, preferably your TWiki-name.)
