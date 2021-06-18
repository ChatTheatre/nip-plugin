%META:TOPICINFO{author=\"kallea\" date=\"1141676071\" format=\"1.0\"
version=\"1.6\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: librarian\</font\>

\<font class=\"query\"\>CATEGORY:\</font\> [Example](NIPCategoryExample)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:librarian

\<font class=\"query\"\>DEPENDENCIES:\</font\>
[emoting](NIPLibRefEmoting), [guarding](NIPLibRefGuarding)

\<font class=\"query\"\>COMPATIBILITY:\</font\> All.

\<font class=\"query\"\>INCOMPATIBILITY:\</font\>
[marrach-guards](NIPLibRefMarrachGuards)

\<font class=\"query\"\>KNOWN ISSUES:\</font\>

Confirmed () issues with this library. (Unconfirmed issues should be
reported in the feedback section at the bottom of this document.)

\<font class=\"query\"\>FEATURES\</font\>

The librarian library is used to allow NPC\'s to stop people who are
trying to leave with an object that is \"marked\". This is written to
work on libraries and library books, but can be used in any similar
instance.

\<font class=\"query\"\>DESCRIPTION\</font\>

The librarian library can be used in a setting where an NPC \"watches
over\" items. The area can be completely public, and characters will be
able to enter and leave as they wish, as long as they do not try to
leave with a marked item in their inventory.

The code is based on StoryCoder Gilmere\'s librarian code for the Castle
Marrach female librarian NPC, and will behave identically.

The string property \"nip:trait:librarian:stamp\" must be set in the
librarian NPC to the property-name which defines whether an item belongs
in the specific area or not. This can be any string, and as long as the
property is set to anything but 0 or nil, the NPC will detect it in
objects even if they are deep-inventoried (i.e. in a person\'s pouch\'s
pouch\'s wallet\'s purse\'s box) and refuse to allow anyone to leave
without dropping the particular item.

Behavior data must be recorded for the NPC in order to behave whenever
someone attempts to leave carrying a marked item. The DBO must be set in
the \"nip:behavior:librarian\" object, and must contain a behavior
recording for \"LIBRARIAN-CATCH\". The recording may optionally contain
either or all of the following scene roles: \* **thief** - the person
trying to leave carrying an item \* **item** - the item that is being
detected (the first item, if multiple are detected) \* **container** -
the top-most container upon the actor in which the item is located \*
**where** - the exit through which the actor is trying to leave

If a library (or its equivalent) contains multiple rooms, each of the
rooms belonging to the library itself must have the
\"detail:library-interior\" property set to 1. Do this by doing +setp
\[exit\] \"library-interior 1\". Alternatively, you may set
\"details:\[the exit id\]:library-interior\" in the room itself instead,
which is essentially the same thing. Doing this will prevent the NPC
from stopping someone trying to walk around inside the library itself
carrying marked items.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

`string <font class="lib">nip:trait:librarian:stamp</font>` \<ul\> The
property-name of the stamp that is present in marked items. If this
property is set to \"mark:library\", then all items in the library
should have the property \"mark:library\" set. \</ul\>

`BDO(object) <font class="lib">nip:behavior:librarian</font>` \<ul\>
Behavior data object pointing to the location where behavior data is
recorded for the librarian. \</ul\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:handler:request-authority\</font\>
\<ul\> Handler for the [guarding](NIPLibRefGuarding) implementation for
the librarian instance. \</ul\>

\-- Main.KalleAlm - 24 Jan 2006

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br/\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)

\<br\> \<font color=\"green\"\>For example, ABN would like to setup an
ice skating area in the winter where a NIPped NPC rents out ice skates.
He would want to prevent those attempting to leave the area with his
rented skates until they hand them back over. But those who OWN their
own skates can come and go freely.

Our first usage of this library will be to set a guard dog, Napoleon, to
keep students from exiting the Orne Library with a University book.
Students may be holding other non-University-owned books, but we would
like those that the library owns to stay within the library. Napoleon
will be set to stand guard at the single entrance to the library. Anyone
passing out will hopefully be caught and held at bay until the student
returns the book. That way we do not have to OOC\'ly run about
+summoning books back to the library on a routine cleaning when players
check out a book, but don\'t return it. This will also prevent the need
for us to code a library book check-out system. After all, this is
Arkham By Night, not Skotos\' Cthulhu library online.

I suppose should we want to get fancy with the scene we can NIP a
librarian human to show up and demand the book back or even have a
pinkerton (cop for hire type) show up and drag the fool off to a special
room until the book is returned.

It has been talked about allowing a successful sneak or thiefery skill
to get by such guard points. But I consider that to be a future
enhancement, and not something I\'d want to have happen automatically in
every NIP I setup with this library. For example, the skate man, sure,
steal his skates. But steal the Necronomicon? No. I\'ll setup a special
plotter-run scenario for that if I want it. Otherwise I\'ll have a
nightmare of stolen books on my hands.

\~ Willow ( Main.KathyPlamback )\</font\>

The ice skating scenario would be easily implemented using this same
library. As for the rest, yeah, improvements can definitely be made when
the time is right for them.

\- Main.KalleAlm - 24 Jan 2006

What stops a player from taking the book, then logging out? Waiting half
an hour, and logging back into their guestroom, complete with stolen
book?

I\'m sure there will be other ways of cheating the system, too. Like
teleporting (if that\'s an ability you have), or any other way of moving
rooms that don\'t do the normal checks.

Also, if there are two exits (in different, linked rooms), I assume that
we need a librarian in each?

A possible extension would be to have a list of books that the librarian
is aware of, and the location that they should stay (third shelf?) -
then every day or so, the librarian could check where the books are,
leave them if they are being used by someone in the library, tidy them
to their location if they are unused and in the room, and\...maybe
teleport them to their location if they have somehow escaped? (a player
takes the book, logs out, and never returns?)

This would also allow the possibility of borrow-able items (rent a gun
for the day, only \$50, no need to buy one, and you can get your revenge
then return it)

\-- Main.TonyDemetriou - 24 Jan 2006

Good point, Tony. The library rooms of course have to be flagged as
sticky (I think that\'s the safe flag), just like prison cells and such.

As for two exits in different locations, yes, would need two librarians,
but they\'d use the same stamp so not a big deal really. The books would
only be marked once anyway.

I like the extension idea. :)

\-- Main.KalleAlm - 25 Jan 2006

Bug regarding the [guarding](NIPLibRefGuarding) library fixed, which
affects this library. CM and LC have been NCS updated so all existing
nippers should be fixed already.

\-- Main.KalleAlm - 06 Mar 2006
