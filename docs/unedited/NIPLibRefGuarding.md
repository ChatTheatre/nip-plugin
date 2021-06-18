%META:TOPICINFO{author=\"kallea\" date=\"1085145486\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: guarding\</font\>

\<font class=\"query\"\>CATEGORY:\</font\> [Service](NIPCategoryService)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:guarding

\<font class=\"query\"\>DEPENDENCIES:\</font\> None.

\<font class=\"query\"\>COMPATIBILITY:\</font\> All.

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

Handle someone entering a precedence-set entrance, and other things
(more to come, by request).

\<font class=\"query\"\>DESCRIPTION\</font\>

A base guarding shell library, which is entirely dependent on an
external library, to perform various guard duties. The marrach guard
library will be made available in time, to show an example of this.

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:handler:request-authority\</font\>
\<UL\> \<pre\>\"Authority request script. This is generic and useless in
most cases, and a secondary library should override it.

Expected input: \$who: (object) Who is acting? \$what: (string) What is
\$who doing? \$where: (NRef) Upon what/where is \$who doing \$what?

Returned values: TRUE to allow; FALSE to deny.\"\</pre\>

This script is supposed to be replaced by an external library (simply
make a \"lib:handler:request-authority\" script and make the library
depend on the guarding lib). \</UL\>

\<font class=\"lib\"\>merry:witness:enter-into%nip:core\</font\> \<UL\>
\<pre\>\"Make sure someone is authorized to enter an exit.\"\</pre\>

This script will call the handler:request-authority script like
so:\<pre\>\$authority = Call( this, \"handler:request-authority\",
\$who: \$actor, \$what: \"enter\", \$where: \$target );

return \$authority;\</pre\>

If the script returns TRUE; the action will go through. If not, the
action will be aborted. \</UL\>

\-- Main.KalleAlm - 08 Dec 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
