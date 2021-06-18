%META:TOPICINFO{author=\"kallea\" date=\"1145031083\" format=\"1.0\"
version=\"1.8\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>LIBRARY REFERENCE: freemoting\</FONT\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Appearance](NIPCategoryAppearance)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:freemoting

\<font class=\"query\"\>DEPENDENCIES:\</font\> None.

\<font class=\"query\"\>COMPATIBILITY:\</font\>
[Emoting](NIPLibRefEmoting), [MOOD](NIPHookRefMood).

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

The freemoting library, contrary to the [emoting
library](NIPLibRefEmoting), uses a stored set of simple strings of emits
and emits those at random. New as of August 2004, the library also
supports variable resolving.

A proper recording feature is not yet implemented in this system.

\<font class=\"query\"\>DESCRIPTION\</font\>

The freemoting library is basically the same thing as the emoting
library, except the emoting library uses a complex database of stored
parser moves, while the freemoting library has already-made strings of
emits.

As of August 2004, the freemoting library supports variable resolving.
Variable resolving enables you to for example write a freemoting action
like this:\<pre\>\"\>Harry looks at \$(actor) and grunts.\"\</pre\> The
variable resolving will convert objects, nrefs and arrays of objects
and/or nrefs into a description of those. If the variable type is a
string, the resolving will simply insert that string as is.

Hint: The NPC itself can be referred to as \$(this) or \$(npc).

As of April 2006, the freemoting library supports un-nested SAM oneof
expressions.\<pre\>The dog {bounces\|skips\|hops} in a {flurry\|frenzy}
upon receiving the {sausage\|food}.\</pre\>Note that nested expressions
such as \<pre\>{in a {flurry\|frenzy}\|with joy}\</pre\> are NOT
SUPPORTED.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

`int <font class="lib">nip:trait:freemoting:frequency</font>` \<UL\> The
freeemoting frequency. The default value is 10, which means the NPC will
freeemote on average every 200th second (i.e. every 3m20s\'d).

The lower the value, the more frequent the NPC\'s freemotes will be
(every (20 \* frequency)\'th second, on average). \</UL\>

`object <font class="lib">nip:behavior:db</font>` \<UL\> Pointer to the
object containing the default freemotes. The property in the database
should be either **\"\<mood\>:freemotes\"** or **\"db:freemotes\"**,
where the latter is used if the former isn\'t found. \<font
color=\"\#ff0000\"\>Note that this property\'s name has changed, and the
previous name (\"nip:behavior:freemoting:db\") is deprecated, and will
be rendered invalid in the future.\</font\> \</UL\>

`object <font class="lib">nip:behavior:<mood></font>` \<UL\> Pointer(s)
to the object(s) containing mood-specific freemotes. The property
searched for is still done in the same way, first
**\"\<mood\>:freemotes\"**, then **\"db:freemotes\"**. Thus, several
mood\'s freemotes can be stored in the same object, or separated, at the
whim of the user. \<font color=\"\#ff0000\"\>Note that this property\'s
name has changed, and the previous name
(\"nip:behavior:freemoting:\<mood\>\") is deprecated, and will be
rendered invalid in the future.\</font\> \</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:freemoting:decide\</font\> \<UL\>
(Signal DECIDE, hook freemoting)\<BR\> This sig-hook script will
randomly emit a free-form text string to the NPC\'s environment based on
the various settings described above. The script will not be executed if
the NPC is [sleeping](NIPLibRefSleeping). \</UL\>

\<font class=\"lib\"\>::handler_freemote()\</font\> \<UL\> This is the
internal freemote handler, logically enough. It is called from the
freemoting:decide script when it is decided that the NPC should
freemote. It is also called from, for example, the
[replaying](NIPLibRefReplaying) library when necessary. \</UL\>

\-- Main.KalleAlm - 07 Jun 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)

\<font color=\"\#ff0000\"\>Note: the properties
\"nip:behavior:freemoting:\*\" are deprecated, and should not be used.
Use \"nip:behavior:\*\" instead.\</font\>

Updated library, separating handler from hook script. \-- Main.KalleAlm
- 19 May 2004

Updated library to enable support for variable resolving. \--
Main.KalleAlm - 18 Aug 2004

Updated library to include support for un-nested oneofs. \--
Main.KalleAlm - 14 Apr 2006
