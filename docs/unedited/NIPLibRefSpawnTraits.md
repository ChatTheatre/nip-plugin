%META:TOPICINFO{author=\"kallea\" date=\"1202982120\" format=\"1.0\"
version=\"1.5\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: spawn-traits\</font\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Internal](NIPCategoryInternal)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:spawn-traits

\<font class=\"query\"\>DEPENDENCIES:\</font\> None.

\<font class=\"query\"\>COMPATIBILITY:\</font\> All.

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

A simple system to apply a number of random traits to a spawned NPC.

\<font class=\"query\"\>DESCRIPTION\</font\>

The spawn-traits library is used to set a variety of traits to NPC\'s,
so that when spawned, they will each look slightly different from each
other.

For instance, if you set the brief for a cat NPC
to:\<pre\>\$(this.appearance:color) cat\</pre\>- then you could use the
spawn-traits system to make each spawned cat look randomly different, by
setting the nip:spawn:traits property to e.g.:\<pre\>(\[
\"appearance:color\" : ({ \"brown\", \"white\", \"black\", \"grey\" })
\])\</pre\>

Thus, spawning a cat would result in either a brown cat, a white cat, a
black cat or a grey cat, randomly.

Slightly static at the moment, but there is a merry script available for
making these traits into adjectives as well. It **requires** that the
property begins with \"appearance:\" (hence, \'slightly static\'). If it
does, or if you can make it so, setting
`merry:inherit:setprop-post:appearance` to
`<Lib:NIP:extra:spawn-traits>` in the nipper should do the trick. You
also have to set a property or it won\'t know which details should have
what:

For example, if you have `appearance:size` which might be one of *small,
medium* or *large* and you want the `default` detail to get the
appropriate adjective, you would set `nip:trait:appearance:adjectives`
to `([ "appearance:size" : ({ "default" }) ])`.

If you have `appearance:nick` which is the nick-name of the NPC, and you
want the default detail to have the nick as sname so people can type
\'smile at slydawg\' if `appearance:nick` happens to be \'slydawg\', you
would set `nip:trait:appearance:names` to
`([ "appearance:nick" : ({ "default" }) ])`.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

\<font class=\"lib\"\>nip:spawn:traits\</font\> \<UL\> This is the
single property used by the spawn-traits system. It is a mapping of the
following format:

\<pre\>(\[ \"\<property-name\>\" : ({ \"\<alternate string\>\",
\"\<alternate two\>\", \... }) \])\</pre\>

If the property was set to:\<pre\>(\[ \"foo\" : ({ \"One\", \"Two\",
\"Three\" }) \])\</pre\> then the property \"foo\" in the CNPC would be
set to \"One\", \"Two\" or \"Three\", at random.

Were it set to:\<pre\>(\[ \"color\" : ({ \"red\", \"green\", \"blue\"
}), \"size\" : ({ \"small\", \"medium\", \"large\" }) \])\</pre\> then
the property \"color\" would be one of \"red\", \"green\" or \"blue\",
and the property \"size\" would be one of \"small\", \"medium\" or
\"large\". \</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:handler:start:traits\</font\> \<UL\>
\"The random traits start-handler\" called by the internal \"act:start\"
script when a CNPC is spawned. \</UL\>

\<font class=\"lib\"\>merry:lib:init\</font\> \<UL\> (NIP library
initialization script.)\<br\> This script adds the \"start:traits\"
handler to the list of spawn-handlers. \</UL\>

\-- Main.KalleAlm - 21 Nov 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
