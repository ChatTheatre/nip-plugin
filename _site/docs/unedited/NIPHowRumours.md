%META:TOPICINFO{author=\"kallea\" date=\"1077576129\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>HOW TO add in the \'ask NPC about TOPIC\' stuff
into my NPC (aka. \'rumours\')?\</FONT\>

**How:**

Add the [rumours](NIPLibRefRumours) library:

    > +setp &lt;npc> "add <b>rumours</b>"
    <font color="#ff0000">The rumours library was loaded. You will need to set the rumour data object to use in the property 'nip:trait:rumour:database'.</font>

Set up a propertycontainer and name it something appropriate, e.g.
*<Data:NIP:rumours:courier>*.

Add the topics and rumours to it;

\<li\> **Topics**: \<ul\> To make the NPC reply to \"ask NPC about
VIVIENNE\", with either \"Long May She Reign\" or \"Queen Vivienne is
our gracious ruler\", you would use, \<li\> the property
**\'topic:vivienne\'**\<br\> and set it to \<li\> **({ \"Long May She
Reign\", \"Queen Vivienne is our gracious ruler\" })** \</ul\> \<li\>
**Aliases**: \<ul\> To make the same NPC also reply with the above, to
\"ask NPC about QUEEN\", you would use, \<li\> the property
**\'alias:queen\'**\<br\> and set it to \<li\> **\"vivienne\"** \</ul\>

When you\'re done making your rumour data object, you would set the
property **\'nip:trait:rumour:database\'** in the NPC to
\<*woename:for:the:rumour:<data:object>*\>.

And you\'re all set. Now you should be able to ask NPC about VIVIENNE
and s/he should reply according to your object.

Note: currently, the ask command is +ask, until the old ask command is
ripped out.

\-- Main.KalleAlm - 06 Sep 2003
