%META:TOPICINFO{author=\"kallea\" date=\"1092188965\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<font color=red\>This document underwent modifications in accordance to
the modifications made to the NIP trading system. The main modification
was converting all float properties into integer 2-decimal hack-floats
(`123 = 1.23`)\</font\>

\<FONT CLASS=\"title\"\>HOW TO set up a nipper to use
[trading](NIPLibRefTrading)?\</FONT\>

**How:**

[Trading](NIPLibRefTrading) is a nipper library used to enable
\"transactions,\" or \"purchases,\" NPC-to-PC. It allows the usage of
\"hard\" cash (bills and coins) and/or \"credit\" type cash (like an
actual credit card, or some form of credit system or another), depending
on how the CDO is set up (in this case, CDO is abbr. \"Cash Data
Object\"). [\[more information on CDO\'s](NIPHowCashDataObjects)\]

In this how-to, I am going to presume that you have a CDO set up (for
you, or by you), and that you simply wish to enable this CDO setup in
your NPC. If this is not the case, either [go
here](NIPHowCashDataObjects) (to find out how to make CDO\'s), or stop
reading now and poke someone worldly into doing it.

\<hr/\>

(From here on, I\'m going to refer to your CDO\'s woe object as
\<CDO\>.)

Any objects the NPC will sell need to have a \"cost\" property set;
namely the property **\"export:nip:item:cost\"**. This property **must
be an integer value**, e.g. 100. If your currency is in dollars and
cents, and one dollar equals 100 cents, then all money values should be
written in **cents**.

In order to fully test the set up, you need at least one item with the
**\"export:nip:item:cost\"** property set. Grab whatever, a beef roll or
something, and set this property to, for example, **500** (\$5.00)

This, of course, presuming you do not already have a set of items
already set up for sale, in which case you can use one or several of
them.

1 Summon your NPC.\<pre\>\> +summon *Woe:name:for:my:npc*\</pre\> 2 You
need these three NIP libs, in this order: [asking](NIPLibRefAsking),
[presents](NIPLibRefPresents), [trading](NIPLibRefTrading)\<pre\>\>
+setp *npc* \'add asking\'\<br/\>\> +setp *npc* \'add
presents\'\<br/\>\> +setp *npc* \'add trading\'\</pre\>(Now, obviously,
if you already use one or both of the aforementioned libraries, you
needn\'t add them a second time.) 3 Set the property
**\"nip:trait:trading:object\"** to \<CDO\> (where \<CDO\> is, as stated
earlier, the woename of your CDO within \< and \>\'s.)\<pre\>\> +setp
*npc* \'nip:trait:trading:object \<Woename:for:my:CDO\>\'\</pre\> 4 Add
your item-for-sale to the nipper\'s list of \"presents\" by using the
+nip-command\'s [present](NIPToolPresent) command.\<pre\>\> +nip *npc*
\'present add *Woename:for:my:item*\'\</pre\>

And now, things should work. Start out by trying to ask the NPC (just
\'ask npc\') to see if the item is listed.

    ---
    > ask <i>npc</i>
    <i>An NPC</i> can give you a beef roll.
    ---

Good. Now, presuming you have some cash at hand, you should be able to
complete a purchase.

    ---
    > ask <i>npc</i> for beef roll
    <i>An NPC</i> offers his beef roll to you.
    Type 'accept from an NPC' to take this item.
    Type 'refuse an NPC' to refuse to take it.
    This will cost you $23.45.

    > accept beef roll
    You hand your three half dollars, your two bucks and your twenty dollar bill to an NPC, paying him $23.50.
    An NPC gives you back $.05 in change.
    You take a beef roll from an NPC.
    ---

\<font color=\"\#ff0000\"\>Note: currently, the \'ask\' verb is still
hooked with the old NPC system; a temporary \'+ask\' verb exists in its
stead.\<br/\>Further note: this goes for the CM server only. The other
servers are using the NPC \'ask\' verb.\</font\>

\-- Main.KalleAlm - 16 Feb 2004
