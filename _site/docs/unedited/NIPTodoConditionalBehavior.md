%META:TOPICINFO{author=\"tonys\" date=\"1057836569\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPTodoStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>TODO: Conditional behavior\</FONT\>

\<QUERY\>PROJECT STATUS\</QUERY\> WORKING

\<QUERY\>STATUS NOTES\</QUERY\>

This tool is finished. See the appropriate library reference and/or how
to\'s for information on how to use it.

\<QUERY\>ASSIGNED CODER(S)\</QUERY\>

  --------------- ---------- ----------------------------
  **Who**         **From**   **Contact information**
  Main.KalleAlm   Marrach    <kalle@marrach.skotos.net>
  --------------- ---------- ----------------------------

\<QUERY\>WHAT?\</QUERY\> Conditional behavior, such as how to react/act
in certain situations and with certain conditions.

\<QUERY\>PRIORITY\</QUERY\> VERY HIGH

\<QUERY\>ETA?\</QUERY\> Done.

\<QUERY\>HOW WILL IT WORK?\</QUERY\> The conditional behavior is an
add-on to the recording tool, where you may set up a scene and act
accordingly. For instance, if you would wish to define how a guard
should act when allowing or denying someone entrance you could set up a
scene with a \"who\" and a \"where\".

You would then start recording as usual, but whilst recording you could
now also act towards the \"who\" object/nref and the \"where\"
object/nref.

\<QUERY\>GENERAL DESCRIPTION\</QUERY\>

The conditional behavior is an extension to the +NIP command, and an
add-on to the record. It is also a feature implemented in the
[eating](NIPLibRefEating) library.

\<QUERY\>TECHNICAL COMMENTS\</QUERY\>

The tool to create conditional behavior data is an add-on to the
\'record\' tool, whereas the +nip command \'scene\' is used to determine
the setting.

During the scene set up, the user will set things up like \"George is
\'who\', the north door is \'where\'.\" and will then interact with
these set objects. The resulting behavior data will add symbols, where
in the aforementioned example, the object George would be turned into
\"(who)\" and the north door would be turned into \"(where)\". Any unset
objects apart from \'here\' and any parts of the actor themselves are
invalid.

\<QUERY\>LIST OF INTERESTED PARTIES\</QUERY\>

If this subject interests you, please add yourself to the list below.
The more interest, the higher priority a subject will get. And also, by
doing so, we will be able to notify you specifically when this
subject\'s status has changed.

    [Your Name]      [Your Email]
    TonySmith           Disdercardo@blueyonder.co.uk
    [insert a separate line above this one]

\-- Main.KalleAlm - 15 Jun 2003

\<QUERY\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT THIS
SUBJECT\</QUERY\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
