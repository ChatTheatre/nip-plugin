%META:TOPICINFO{author=\"kallea\" date=\"1154680080\" format=\"1.0\"
version=\"1.1\"}% \<UpdateIssue\> [NIPUpdateRefStyle]{.twiki-macro
.INCLUDE}

\<font class=\"title\"\>SYSTEM ISSUE \#42:\</font\>

\<font class=\"query\"\>DATE:\</font\> August 3, 2006.

\<font class=\"query\"\>UPDATE AFFECTS:\</font\> [Prey](NIPLibRefPrey),
[fighting-fake](NIPLibRefFightingFake).

\<font class=\"query\"\>UPDATED BY:\</font\> Main.KalleAlm

\<font class=\"query\"\>PROBLEM\</font\>

Staffers had mentioned bugs where NPC\'s using the
[fighting-fake](NIPLibRefFightingFake) library did not die all the time.
The reason for this was that the [prey](NIPLibRefPrey) library had an
isolated function for handling death, which was not shared among the
libraries. The death concept of the [prey](NIPLibRefPrey) library was
moved out and turned into its own NIP lib, called simply
[death](NIPLibRefDeath). This poses several problems to exsting nippers,
where the most prominent is that NPC\'s will need the \"nip/die\" action
handler or they will fail to shutdown when killed.

\<font class=\"query\"\>REQUIRED USER-MEASURES\</font\>

Nothing. If nippers appear to have become immortal in your game (where
they are killed but don\'t stop moving around), doing a `+ncs update`
should solve the issue permanently.

\<font class=\"query\"\>SOLUTION\</font\>

The [prey](NIPLibRefPrey) library\'s death functionality was turned into
[its own NIP lib](NIPLibRefDeath), as it turned out to be useful in
other cases as well ([fighting-fake](NIPLibRefFightingFake)). The
[prey](NIPLibRefPrey) library now uses a much simplified death handler,
but all current prey-enabled nippers will add the
[death](NIPLibRefDeath) library, as it has been the default until this
point.

This update is in fact 3 separate updates (40-42) which juggle things
around a bit. For instance the \"nip:trait:prey:rot_time\" (and such)
properties have been moved out of the prey library and thus have been
renamed to \"nip:trait:death:rot_time\".

\-- Main.KalleAlm - 04 Aug 2006

\<font class=\"query\"\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT
THIS SUBJECT\</font\>\<br\> (Please, don\'t forget to add your name to
your comment, preferably your TWiki-name.)
