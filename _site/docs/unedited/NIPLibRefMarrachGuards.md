%META:TOPICINFO{author=\"kallea\" date=\"1092344312\" format=\"1.0\"
version=\"1.1\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: marrach-guards\</font\>

\<font class=\"query\"\>CATEGORY:\</font\> [Example](NIPCategoryExample)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:marrach-guards

\<font class=\"query\"\>DEPENDENCIES:\</font\>
[Guarding](NIPLibRefGuarding), [emoting](NIPLibRefEmoting)

\<font class=\"query\"\>COMPATIBILITY:\</font\> None.

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None known.

\<font class=\"query\"\>KNOWN ISSUES:\</font\>

Confirmed () issues with this library. (Unconfirmed issues should be
reported in the feedback section at the bottom of this document.)

\<font class=\"query\"\>FEATURES\</font\>

(Dis)allowing people from entering exits based on \"marrach:precedence\"
property and a precedence setting for the exit(s). Example library, but
will eventually be used in the Castle Marrach game.

\<font class=\"query\"\>DESCRIPTION\</font\>

The marrach-guards library currently only handles the allowing and
disallowing of people from entering certain exits marked with a certain
precedence requirement. In Castle Marrach, characters are only allowed
into areas which are beneath or equal to their own in-game precedence (a
person\'s precedence is determined by their work and/or intrinsic rank
within the castle).

The [guarding](NIPLibRefGuarding) library contains a shell \'authority\'
script which is replaced by an actual script in the marrach-guards
library.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

`object <font class="lib">nip:trait:exit-precedence</font>` \<ul\> Data
object containing information regarding exits and their precedence. If
you wish to set one such up, initialize it properly by setting the
property `nip:precedence` to `([ ])`. \</ul\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:handler:request-authority\</font\>
\<ul\> Script replacing the shell authority script in the
[guarding](NIPLibRefGuarding) library. \</ul\>

\<font class=\"lib\"\>merry:lib:init\</font\> \<ul\> NIP library
initialization script, called once every time the library is added to an
NPC configuration. Sets the NPC\'s skill in Teanga to Grand Master, its
current language to Teanga and enables the scriptrunner flag for the
witness scripts. \</ul\>

\<font class=\"lib\"\>merry:lib:marrach:court_pass\</font\> \<ul\>
Simple court-pass check script, used specifically when a person tries to
enter a precedence-1 set door with precedence 0. \</ul\>

\-- Main.KalleAlm - 12 Aug 2004

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br/\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
