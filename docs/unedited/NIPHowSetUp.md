%META:TOPICINFO{author=\"kallea\" date=\"1062192653\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>HOW TO turn an object into an NPC?\</FONT\>

**How:**

Make sure your object is backed up (in case something would go wrong).

Summon it into your environment if you wish. It\'s not needed, though.

Type: **+nip \"set Woename:for:your:object\"**

You will receive a brief welcome message, and then you\'re done!

**Tweaking functionality:**

The NPC will at this point contain a number of properties. These
properties are nip:**, nip-core:** and npc:**.\<br\>The most important
ones to remember are the nip:** ones.\<br\>nip-core:\* should usually be
left as is.\<br\>npc:\* is a property representation of the NPC\'s
current state, and should not contain any system configuration
properties.

**Further comment(s):**

[Check out the tutorials and/or howto\'s](NIPSystemReference) on what to
do next.

\-- Main.KalleAlm - 03 Jun 2003
