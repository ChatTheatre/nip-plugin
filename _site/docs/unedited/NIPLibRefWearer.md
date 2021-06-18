%META:TOPICINFO{author=\"kallea\" date=\"1202964021\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: wearer\</font\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Behavior](NIPCategoryBehavior)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:wearer

\<font class=\"query\"\>DEPENDENCIES:\</font\>
[Offers](NIPLibRefOffers).

\<font class=\"query\"\>COMPATIBILITY:\</font\>
[Emoting](NIPLibRefEmoting), [freemoting](NIPLibRefFreemoting).

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None known.

\<font class=\"query\"\>KNOWN ISSUES:\</font\>

Confirmed () issues with this library. (Unconfirmed issues should be
reported in the feedback section at the bottom of this document.)

\<font class=\"query\"\>FEATURES\</font\>

\* Making the nipper wear specific items when offered. \* Making the
nipper unwear and hand specific items over to the actor when requested.
\* Internal and/or external handler support for giving and taking of
items.

\<font class=\"query\"\>DESCRIPTION\</font\>

The wearer library is the Barbie-doll aspect of NIP. It allows the
builder to customize, control and restrict the art of
dressing/undressing the nipper. Due to the wide range of options in how
exactly this should be handled, the library is written to support
external handlers for one or both of the giving and taking aspects.
*Undressing nippers is actually not implemented in this system (yet).
Code is available e.g. from Mortalis Victus, but this code needs tuning
as it depends on factors exclusive to that game (\"only that one who
tamed me may dress/undress me\", for example).*

The most obvious example where this library would come in handy is a dog
and a collar, or a horse and a saddle. The ideal solution is if she
would wear the saddle when you give it to her, and somehow remove and
give it to you if you tried to take it from her body.\<pre\>

------------------------------------------------------------------------

\> give my saddle to horse You offer your saddle to a brown steed. Type
\'revoke a brown steed\' to abort this action.

A brown steed takes a saddle from you. A brown steed wears a saddle.

\> take horse\'s saddle A brown steed removes a saddle. You take the
saddle from a brown steed.

------------------------------------------------------------------------

\</pre\>

\<font class=\"query\"\>NIP PROPERTIES\</font\>

`object <font class="lib">nip:behavior:wear</font>` \<ul\> If set, the
wearer library will presume that behavior data is available for the
moods \'GIVE\' and \'TAKE\'. \</ul\>

`mapping <font class="lib">nip:trait:wearer:accepts</font>` \<ul\>
(Note: this property is a part of the internal handler for \'give\'.
Thus, if you write your own handler and do not include the code in the
original handler, this property is useless.)

Property-to-value list of options. For instance,\<pre\>(\[
\"nip:item:wearable\" : 1 \])\</pre\>would mean that the **property**
\"nip:item:wearable\" in the item being offered must be set to
1.\<pre\>(\[ \"nip:item:foo\" : \"bar\" \])\</pre\> means the property
\"nip:item:foo\" must be set to \"bar\"\<pre\>(\[ \"nip:item:wearable\"
: 1, \"nip:item:foo\" : \"bar\" \])\</pre\>means that the property
\"nip:item:wearable\" must be set to 1 **or** the property
\"nip:item:foo\" must be set to \"bar\"

Warning: Make sure you do the above properly. By default you MUST set
\"nip:item:wearable\" to 1 in whatever it is the NPC should wear. If
it\'s a horse, you are encouraged to CHANGE that to e.g.
\"nip:item:wearable:horse\" or whatever, so that HORSES don\'t wear DOG
COLLARS and DOGS don\'t wear SADDLES and so on. I\'m sure you can see
the dilemma here, if you use \"nip:item:wearable\" for all nippers!

Warning again: Don\'t forget to use \"export:\" when you set this
property in items. If you set \"nip:item:wearable\" in
Game:clothing:collar, then spawn Game:clothing:collar and try to make
your dog wear it, the dog will refuse, because \"nip:item:wearable\" is
only set in the master. Fix this by setting \"export:nip:item:wearable\"
in Game:clothing:collar instead. \</ul\>

`boolean <font class="lib">nip:trait:wearer:silent-give</font>` \<ul\>
(Default: 0)

This property describes whether the wearer library should use the
default emits when someone gives something to be worn, to the nipper. If
set, no internal output will be given. \</ul\>

`boolean <font class="lib">nip:trait:wearer:silent-take</font>` \<ul\>
(Default: 0)

This property describes whether the wearer library should use the
default emits when someone successfully takes something from the nipper.
If set, no internal output will be given. \</ul\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:handler:offer:wearer\</font\> \<ul\>
\"The \'wearer\' library handler for the \'offer\' feature.\"

This script ensures the nipper is not asleep, and, if the \'give\'
handler returns TRUE, it accepts and wears the offered item. \</ul\>

\<font class=\"lib\"\>merry:lib:handler_wearer_give\</font\> \<ul\>
\"This is the default \'wearer\' give-handler. It is triggered whenever
someone tries to give something to a nipper which is using the
\'wearer\' library. This handler makes use of the documented
\'nip:trait:wearer:accepts\' mapping, but in order to more finely
determine what and who, you should consider writing a NIP library which
replaces this handler.

This handler is sent the object pointers \$offer and \$actor.\" \</ul\>

\<font class=\"lib\"\>merry:lib:handler_wearer_take\</font\> \<ul\>
\"You need to create a handler which determines whether a person may or
may not take items from the nipper. This handler refuses all persons.\"

This is a dummy handler, only here to act as a placeholder until a real
take handler is created (probably by yourself, unless your game team has
one already). \</ul\>

\<font class=\"lib\"\>merry:react-pre:take-from\</font\> \<ul\>
\"Determine whether \$actor is allowed to take something from us and if
so, unwear it and move it into the actor\'s inventory.\"

This script makes use of the \'take\' handler mentioned above. If the
take handler is permissive (returns TRUE), we will accept everything
listed in the property \$what, which also contains a list of the offered
items.

Thus; the \$what property may contain more than one object. Thus,
checking if \$what\[0\] is accepted is not enough. You need to check and
**remove** any entries in \$what that aren\'t acceptable. Even if there
are unacceptable elements in \$what, one acceptable entry is enough to
return TRUE. \</ul\>

\-- Main.KalleAlm - 17 Aug 2004

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br/\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
