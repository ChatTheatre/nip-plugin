%META:TOPICINFO{author=\"kallea\" date=\"1055635287\" format=\"1.0\"
version=\"1.1\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>SIGNAL/HOOK REFERENCE: DELIVERY\</FONT\>

\<QUERY\>WOE NAME:\</QUERY\> Lib:NIP:signals:DELIVERY

\<QUERY\>SIGNAL:\</QUERY\> DELIVERY

\<QUERY\>INITIAL PRIORITY:\</QUERY\> 60000

\<QUERY\>HOOK(S):\</QUERY\> delivery

\<QUERY\>DEPENDENCIES:\</QUERY\> None.

\<QUERY\>COMPATIBILITY:\</QUERY\> [courier](NIPLibRefCourier)

\<QUERY\>INCOMPATIBILITY:\</QUERY\> None.

\<QUERY\>MAIN PURPOSE\</QUERY\>

The DELIVERY signal is responsible for any delivery triggers, whereas
the main is in the delivery sig-hook, and is used to deliver items to
people in the room.

\<QUERY\>DESCRIPTION\</QUERY\>

The delivery feature is, to save resources, stepping through the room\'s
inventory for anything with volition, and grabs one at a time and checks
for new scrolls. A couple of scripts are in place to handle most of the
delivery, but this script is a back-up feature for if some or all of
these must be replaced.

It is my belief that most of the scripts are already sufficient to deal
with this, but things like disconnecting in a room, having a scroll put
in the queue for you, and then reconnecting, a courier wouldn\'t realize
you were there if it wasn\'t for this sig-hook.

\<QUERY\>NIP PROPERTIES\</QUERY\>

\<LIB\>nip:trait:delivery:database\</LIB\> \<UL\> This property points
to a propertycontainer, and relies on the property **\"nip:delivery\"**
which is in the format **(\[ \<recipient\> : ({ \<enqueued-object\>,
\... }) \])**. \</UL\>

\<QUERY\>SIGNAL/HOOK SCRIPT REFERENCE(S)\</QUERY\>

\<LIB\>merry:lib:handler:deliver\</LIB\> \<UL\> The deliver-script. Call
this with the argument \$recipient as object reference to whoever is to
be given their things. Note that this script doesn\'t check if the
recipient is in the same room. This check should be made before, unless
global deliveries across rooms is accepted behavior.

Syntax: **Call( this, \"handler:deliver\", \$recipient: object );**
\</UL\>

\<LIB\>merry:lib:delivery:delivery-exec\</LIB\> \<UL\> (Signal DELIVERY,
hook delivery, trigger exec)\<BR\> This sig-hook script steps through
the room\'s inventory and anything with volition is checked for queued
items (and those are delivered if found). It checks **one volitioned
object per heartbeat**, whereas a beat takes place approx. every 20th
second. \</UL\>

\-- Main.KalleAlm - 14 Jun 2003

\<QUERY\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</QUERY\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
