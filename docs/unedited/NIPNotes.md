%META:TOPICINFO{author=\"kallea\" date=\"1161788384\" format=\"1.0\"
version=\"1.54\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
\<NIPNotesSearchPoint \-- do not delete\> October 25: Upgraded
[eating-animalistic](NIPLibRefEatingAnimalistic), fixing the zombie bug.
Sorry, Lovecraft-people, better luck next time. Also fixed
[death](NIPLibRefDeath), which had issues unsetting volition in nippers
when they died, if they were not also using [prey](NIPLibRefPrey).

April 26: The [act-interpreter](NIPLibRefActInterpreter) library was
made obsolete. If you were using this library, refer to its new location
Lib:NIP:obsolete:lib:act-interpreter \-- but be warned that this
functionality is no longer supported by the maintainer.

March 22: Added \"log-to\" functionality in
[communicate](NIPLibRefCommunicate) library, which can be used to detect
commonly asked phrases and improve the NPC communications with PC\'s.

March 13: Fixed serious bug in respawn act:stop script, where if an NPC
\"stopped\" (the social action), it was respawned. Also added \"External
systems\" category to main NIPSystemReference page, and described [the
spawn system](NIPExtSpawn).

March 6: Bug regarding the [guarding](NIPLibRefGuarding) library fixed,
which also affects the [librarian](NIPLibRefLibrarian) library. CM and
LC have been NCS updated so all existing nippers should be fixed there
already.
