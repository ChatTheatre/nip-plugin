%META:TOPICINFO{author=\"soledadb\" date=\"1146146413\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPTodoStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>TODO: Fake fighting\</font\>

\<font class=\"query\"\>PROJECT STATUS\</font\> DONE

\<font class=\"query\"\>STATUS NOTES\</font\>

Done.

\<font class=\"query\"\>ASSIGNED CODER(S)\</font\>

  --------------- ---------- -----------------------------
  **Who**         **From**   **Contact information**
  Main.KalleAlm   Skotos     <kalle@mortalis.skotos.net>
  --------------- ---------- -----------------------------

\<font class=\"query\"\>WHAT?\</font\> A fake-fighting system for
non-dueling situations, e.g. rats attacking a person.

\<font class=\"query\"\>PRIORITY\</font\> MEDIUM

\<font class=\"query\"\>ETA?\</font\> April 25, 2006.

\<font class=\"query\"\>HOW WILL IT WORK?\</font\>

The system will simply be two features \-- target-person, wound-person,
and receive-wound. The receive-wound feature will determine if the
nipper dies by the wound or survives. In short, it\'s fighting, but on a
blow-to-blow level rather than e.g. a dueling system.

\<font class=\"query\"\>GENERAL DESCRIPTION\</font\>

There is demand for a system which can be implemented into non-humanoid
non-sword wielding nippers, which effectively makes them \"dangerous\"
to be around, but also ensures they are \"mortal\". (A dangerous nippers
that cannot be killed is rather a suicidal move from a game designer\'s
point of view.)

Thus, the fighting-fake library, which implements a way to make nippers
target people, and attempt to kill them by emitting an attack against a
person, then rolling a die and, if successful, emit the successful
wounding and do the equivalent of +wound upon the target; or, if
unsuccessful, simply emit the result.

The system also implements a way for people to attack the nipper back.
This will default to \"wield a weapon, any weapon, and you can do
\'slash \[nipper\]\' to get the same deal; attempt, die-roll,
success/failure.

\<font class=\"query\"\>LIBRARIES\</font\>

    [Library]         [Description]
    fighting-fake    The main library.

\<font class=\"query\"\>HOOKS\</font\>

    [Hook]            [Using signals]             [Description]
    fighting-fake    DECIDE                       Determine what to do.

\<font class=\"query\"\>TECHNICAL COMMENTS\</font\>

Since signals are only triggered every 20 seconds or so, the
fighting-fake decide hook will in fact trigger an internal
loop-mechanism which handles the combat itself. This, too, can be
customized with a min and max value for how often the nipper attempts to
attack.

\<font class=\"query\"\>LIST OF INTERESTED PARTIES\</font\>

If this subject interests you, please add yourself to the list below.
The more interest, the higher priority a subject will get. And also, by
doing so, we will be able to notify you specifically when this
subject\'s status has changed.

    [Your Name]      [Your Email]
    Reveur    reveur@marrach.skotos.net
    [insert a separate line above this one]

\-- Main.KalleAlm - 25 Apr 2006

\<font class=\"query\"\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT
THIS SUBJECT\</font\>\<br/\> (Please, don\'t forget to add your name to
your comment, preferably your TWiki-name.)
