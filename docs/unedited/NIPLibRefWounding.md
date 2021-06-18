%META:TOPICINFO{author=\"kallea\" date=\"1085145329\" format=\"1.0\"
version=\"1.5\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: wounding\</font\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Behavior](NIPCategoryBehavior)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:wounding

\<font class=\"query\"\>DEPENDENCIES:\</font\> None.

\<font class=\"query\"\>COMPATIBILITY:\</font\>
[Wounding-mgeneric](NIPLibRefWoundingMGeneric)

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>KNOWN ISSUES:\</font\>

Confirmed () issues with this library. (Unconfirmed issues should be
reported in the feedback section at the bottom of this document.)

\<font class=\"query\"\>FEATURES\</font\>

NPC-to-PC wounding.

\<font class=\"query\"\>DESCRIPTION\</font\>

Wounding implements a wrapper for calling an external wound-system by
constructing a map of arguments using the secondary handler. As of the
time of writing, there is only one such system available \--
[wounding-mgeneric](NIPLibRefWoundingMGeneric).

This system **does not** cause an NPC to wound a PC on its own. Some
external code must make a call to the ::wound() function.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

\<font class=\"lib\"\>nip:trait:wound:map:arg\</font\> \<UL\> (Unless
you intend on writing your own wound-wrapper, you don\'t need to know
what this does.)\<br/\> Argument mapping { args\[X\] = args\[Y\] } - for
potential use by the external handler. \</UL\>

\<font class=\"lib\"\>nip:trait:wound:map:set\</font\> \<UL\> (Unless
you intend on writing your own wound-wrapper, you don\'t need to know
what this does.)\<br/\> Hardcoded setprop mapping { args\[X\] = Y } -
for potential use by the external handler. \</UL\>

\<font class=\"lib\"\>nip:trait:wound:map:ref\</font\> \<UL\> (Unless
you intend on writing your own wound-wrapper, you don\'t need to know
what this does.)\<br/\> This.reference mapping { args\[X\] = this.Y } -
for potential use by the external handler. \</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:wound\</font\> \<UL\> Resolve the wound
maps and call the resulting object \$handler, and the resulting function
\$function. \</UL\>

\-- Main.KalleAlm - 17 Mar 2004

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
