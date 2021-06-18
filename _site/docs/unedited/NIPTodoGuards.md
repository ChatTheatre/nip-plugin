%META:TOPICINFO{author=\"kallea\" date=\"1055801052\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPTodoStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>TODO: Guarding code\</FONT\>

\<QUERY\>PROJECT STATUS\</QUERY\> WORKING

\<QUERY\>STATUS NOTES\</QUERY\>

The guard system is, although very limited in features, in place and
working. As ready as \"ready to replace the guards in Marrach\" would be
to the reader.

\<QUERY\>ASSIGNED CODER(S)\</QUERY\>

  --------------- ---------- ----------------------------
  **Who**         **From**   **Contact information**
  Main.KalleAlm   Marrach    <kalle@marrach.skotos.net>
  --------------- ---------- ----------------------------

\<QUERY\>WHAT?\</QUERY\> A customizable codebase for guards,
moving/still-standing etc.

\<QUERY\>PRIORITY\</QUERY\> VERY HIGH

\<QUERY\>ETA?\</QUERY\> Completed.

\<QUERY\>HOW WILL IT WORK?\</QUERY\> This is a customized guarding
library for Marrach. However, parts of or the library in its entirety
will be displayed publicly as an example. The library is divided into
two libraries, whereas one is a very simple \"guarding layer\" and the
other , Marrach-specific, adds on to the first.

\<QUERY\>GENERAL DESCRIPTION\</QUERY\>

The reason for the multi-lib solution is simple enough. The guarding
library is supposed to be useful to anyone, regardless of theme,
setting, environment, etc. while the Marrach-customized add on lib is
specifically for the Marrach environment.

This does not mean a similar (or not-so similar) theatre/game could use
a modified version of the Marrach library.

\<QUERY\>LIBRARIES\</QUERY\>

    [Library]         [Description]
    guarding            Standard guarding library.
    marrach-guards  Marrach-specific guarding library.

\<QUERY\>TECHNICAL COMMENTS\</QUERY\>

The guarding library currently hooks the witness:enter-into script to
enable entrance authority (by precedence in the case of Marrach). Its
default behavior is quite useless; the handler
(lib:handler:request-authority) simply emotes a social informing the
actor of his action. All actions are allowed in the default guarding
library.

An add-on, such as marrach-guards, would contain a secondary
lib:handler:request-authority-script, placed in the init:merry array in
the library. The add-on would depend on guarding, dependency:needs = ({
\<Lib:NIP:lib:guarding\> }), and would at load-time replace the original
handler with something a bit more useful.

\<QUERY\>LIST OF INTERESTED PARTIES\</QUERY\>

If this subject interests you, please add yourself to the list below.
The more interest, the higher priority a subject will get. And also, by
doing so, we will be able to notify you specifically when this
subject\'s status has changed.

    [Your Name]      [Your Email]
    [insert a separate line above this one]

\-- Main.KalleAlm - 07 Jun 2003

\<QUERY\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT THIS
SUBJECT\</QUERY\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
