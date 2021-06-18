%META:TOPICINFO{author=\"kallea\" date=\"1062193920\" format=\"1.0\"
version=\"1.1\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>HOW TO make them give out things?\</FONT\>

The more practical CNPC\'s, such as couriers, cooks, tailors, and such,
must be able to distribute things. That\'s where the
[presents](NIPLibRefPresents) library comes into the picture.

**How:**

Add the library \'presents\'. You will need to add \'asking\' first,
though, if your NPC doesn\'t have it already.\<pre\>\> +setp \<npc\>
\"add presents\" \<font color=\"\#ff0000\"\>The \'presents\' handler has
been added to this CNPC. This means you can now attach things that the
NPC will \'hand out\' to people. For instance, \'scrolls\' for courier
CNPC\'s and such.\</font\>\</pre\>

Now, use the +NIP \"present\" tool to add items to the NPC. If it is a
cook, for instance, you might want to add
\<Generic:food:meat:beef-roll\>:\<pre\>\> +nip \<npc\> \"**present add
Generic:food:meat:beef-roll**\" The object Generic:food:meat:beef-roll
added.\</pre\>

The system automatically grabs all the snames from the object\'s prime
detail and tacks them to the list of choices. If we wish to decide the
names to use, we simply write the names ourselves instead.\<pre\>\> +nip
\<npc\> \"present add Generic:food:meat:beef-roll **beef meat food**\"

**Tweaking functionality:**

None.

**Further comment(s):**

None.

\-- Main.KalleAlm - 29 Aug 2003
