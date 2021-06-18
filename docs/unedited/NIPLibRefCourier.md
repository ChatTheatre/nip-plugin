%META:TOPICINFO{author=\"kallea\" date=\"1099051740\" format=\"1.0\"
version=\"1.7\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>LIBRARY REFERENCE: courier\</FONT\>

\<font class=\"query\"\>CATEGORY:\</font\> [Example](NIPCategoryExample)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:courier

\<font class=\"query\"\>DEPENDENCIES:\</font\>
[offers](NIPLibRefOffers), [presents](NIPLibRefPresents),
[DELIVERY](NIPHookRefDelivery)

\<font class=\"query\"\>COMPATIBILITY:\</font\> None specific.

\<font class=\"query\"\>INCOMPATIBILITY:\</font\>
[mounting](NIPLibRefMounting)

\<font class=\"query\"\>FEATURES\</font\>

Enqueuing and distributing enqueued items from the delivery database.

\<font class=\"query\"\>DESCRIPTION\</font\>

The courier library uses the delivery database to hand out / enqueue
objects from within the game.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

None.

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:act-post:enter\</font\> \<UL\> This script
is triggered when the courier has moved from a room into another. The
courier is added to the new room in the delivery database\'s nip:covered
mapping. \</UL\>

\<font class=\"lib\"\>merry:act-post:teleport\</font\> \<UL\> This
script is triggered when the courier has been teleported into a new
room. The courier is added to the room in question\'s nip:covered
mapping. \</UL\>

\<font class=\"lib\"\>merry:act:enter\</font\> \<UL\> This script is
triggered **before** the courier has entered a new room, while the
courier is still in the old room. The courier is removed from the old
room\'s nip:covered mapping. \</UL\>

\<font class=\"lib\"\>merry:act:teleport\</font\> \<UL\> This script is
triggered **before** the courier has been teleported out of a room into
another. The courier is removed from the left room in the nip:covered
mapping. \</UL\>

\<font class=\"lib\"\>merry:lib:handler:offers:addressed\</font\> \<UL\>
An [offers](NIPLibRefOffers) handler added to the offers script chain
when this library is loaded into an NPC. Anything offered to the NPC
which is addressed to someone is accepted and enqueued appropriately.
\</UL\>

\<font class=\"lib\"\>merry:lib:init\</font\> \<UL\> NIP Library
initialization script.\<BR\> This script adds the \<NPC:misc:scroll\> to
the present dist list, adds the \<font
class=\"lib\"\>offers:addressed\</font\> handler to the offers script
chain, and makes the NPC a scriptrunner if it isn\'t one already.
\</UL\>

\<font class=\"lib\"\>merry:witness:enter-from\</font\> \<UL\> This
script is triggered whenever someone enters the room. The target is
automatically checked for enqueued scrolls and if found, these are all
delivered instantly. \</UL\>

\-- Main.KalleAlm - 14 Jun 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)

We need for lovecraft country some type of inanimate object that acts
like a courier, i.e.:

    > enter mailroom
    You arrive in the mailroom.
    > check mailbox
    You get 5 envelopes from your mailbox.

\-- Main.ChristopherAllen - 17 Jun 2003

Definitely. A variety of different methods to collect the items
should/will be available soon.

I guess the big question is whether letters and such should be separated
from items and deliveries of that nature. Someone has a new T.V. sent to
them via mail. Would that be handed by a courier, be put in a mailbox,
or be available at some mail office with NPC clerks/desk assistants.

So yeah, the issue is \"broad\" to say the least. If you wish to do
something LC-specific, please do. I do have plans to do this some time
within the week/next week though.

\-- Main.KalleAlm - 18 Jun 2003

New feature implemented - alternative recipients (assistants).

There are two properties that affect this.

1 In every PC body, if the property \"nip:delivery:alternative\" is set
to another object, all scrolls to the PC will be redirected (but not
re-addressed) to the alternative body. Thus, assistants can take their
master\'s scrolls (CM). 2 In the actual letter/scroll/package, if the
property \"nip:delivery:direct\" is set (1), the item will **not** be
redirected. Thus, it is still possible to send things to the PC
directly.

\-- Main.KalleAlm - 24 Aug 2004

The courier example library now uses the CronDaemon to purge old
undelivered scrolls (purge = deliver). Make sure it is enabled.

\-- Main.KalleAlm - 29 Oct 2004
