%META:TOPICINFO{author=\"kallea\" date=\"1062195240\" format=\"1.0\"
version=\"1.1\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>HOW TO make them accept things?\</FONT\>

Some NPC\'s should be able to accept and take things from people, such
as trash-taking servants, credit-card clerks in hotels, scroll-snatching
couriers and such. The [offers](NIPLibRefOffers) library is used to do
this. However, the offers library keeps a list of **scripts** that will
be executed. These scripts will then return TRUE or FALSE, depending on
whether they wish to accept the offered object or not. Check out the
library reference for [eating](NIPLibRefEating), specifically the
**merry:lib:handler:offer-eating** script.

**How:**

Add the offers library to your NPC. If your NPC does not have the asking
library yet, you must add this as well.\<pre\>\> +setp \<npc\> \"add
offers\" \<font color=\"\#ff0000\"\>The core \'offer\' handler has been
added to this CNPC. This library is for example required by the
\'eating\' library.\</font\>\</pre\>

After successfully adding the offers library, you may now proceed to add
your script to the offer script chain by, whilst possessing the NPC,
doing:\<verbatim\>\> +tool merry exec Call( this, \"core:add_offer\",
\$script: \"**script-name**\" );\</verbatim\>

**Tweaking functionality:**

None.

**Further comment(s):**

This is currently somewhat tricky. I will toss together a simple offer
container library sometime soon, so you won\'t have to bother with
scripts. The reason for the script thing is because at times it\'s not
just a matter of checking whether a property exists in the offered
object; a lot of the times checks need to be made to see if the NPC
would have use for the thing, or whether the NPC would refuse to take
it.

\-- Main.KalleAlm - 29 Aug 2003
