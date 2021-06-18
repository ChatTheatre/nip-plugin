%META:TOPICINFO{author=\"kallea\" date=\"1161786561\" format=\"1.0\"
version=\"1.1\"}% \<UpdateIssue\> [NIPUpdateRefStyle]{.twiki-macro
.INCLUDE}

\<font class=\"title\"\>SYSTEM ISSUE \#43:\</font\>

\<font class=\"query\"\>DATE:\</font\> October 25th, 2006.

\<font class=\"query\"\>UPDATE AFFECTS:\</font\>
[Death](NIPLibRefDeath).

\<font class=\"query\"\>UPDATED BY:\</font\> Main.KalleAlm

\<font class=\"query\"\>PROBLEM\</font\>

Nippers using [death](NIPLibRefDeath), but not [prey](NIPLibRefPrey),
would fail to lose volition upon death.

\<font class=\"query\"\>REQUIRED USER-MEASURES\</font\>

Perform NCS update as normally.

\<font class=\"query\"\>SOLUTION\</font\>

The [death](NIPLibRefDeath) library now sets volition when a child is
spawned, which allows the UrParent to have non-volition. This in turn
allows the individual children to unset volition upon death.

\-- Main.KalleAlm - 25 Oct 2006

\<font class=\"query\"\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT
THIS SUBJECT\</font\>\<br\> (Please, don\'t forget to add your name to
your comment, preferably your TWiki-name.)
