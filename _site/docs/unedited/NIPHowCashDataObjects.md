%META:TOPICINFO{author=\"tonyd\" date=\"1121829503\" format=\"1.0\"
version=\"1.4\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<font color=red\>This document underwent modifications in accordance to
the modifications made to the NIP trading system. The main modification
was converting all float properties into integer 2-decimal hack-floats
(`123 = 1.23`)\</font\>

\<FONT CLASS=\"title\"\>HOW TO create cash data objects?\</FONT\>

**How:**

The CDO\'s are a vital part of the [trading](NIPLibRefTrading) system in
NIP. Additionally, the CDO\'s are the most complicated objects in the
process of introducing trade to your NPC\'s. As such, we\'re going to
step-by-step create a CDO here with support for both hard cash and
credit.

\* Firstly, I create a bunch of \"cash\" objects, a dollar-bill, five
dollar-bill, ten-, twenty-, fifty-, and one hundred-dollar bills, plus
various coins. I put all these in the woe folder \"Game:Props:cash\",
and name them after their value (the 100-dollar bill is
\"Game:Props:cash:100\", the quarter is \"Game:Props:cash:.25\", etc).
Additionally, I create a \"VISA\" card and call it
\"Game:Props:cash:visa\".

The VISA card is the only object I need to set a special property in,
and this only for testing purposes. I set the property \"cash:balance\"
to an integer value, **20000**, which in USD would equal to \$200.00.

If you\'re only going to deal with \"credit\" type cash, then you can
skip everything but the \'VISA\' part.

\* Secondly, I create the CDO itself, which is a property container. I
give this the name \"Game:<Data:NIP:cash:CDO>\" and set three properties
in it.

I set **\"cash:announce-change\"** to \<pre\>\"\$(npc) gives you back
\$(prefix)\$(change)\$(suffix) in change.\"\</pre\> 1 \$(npc) will
resolve as Describe( \<npc\> ), i.e. the brief description (\"a burger
king dude\"). 2 \$(prefix) will resolve the prefix of the cash. More
about this later. 3 \$(suffix) -\"- 4 \$(change) will resolve the amount
of money given back in change.

Then I set **\"cash:announce-cost\"** to \<pre\>\"This will cost you
\$(prefix)\$(cost)\$(suffix).\"\</pre\> 1 \$(cost) will resolve the
amount of money the item costs.

Then I set **\"cash:announce-shortage\"** to \<pre\>\"You do not have
enough \$(name) for \$(item).\"\</pre\> 1 \$(name) will resolve the name
of the cash type (more later). 2 \$(item) will resolve the name of the
item being requested (\"a beef roll\").

\<font color=\"\#0000ff\"\>Hint: use **+cobj** to create the object(s),
and **+setp** with the @-feature to point to the object, like:\<pre\>\>
+setp \'\@Game:<Data:NIP:cash:CDO>\"\<br/\>\<br/\> \[pointer\] \--\>
\<Game:<Data:NIP:cash:CDO>\>\<br/\>\<br/\>\> +setp
\'cash:announce-change \$(npc) gives you back
\$(prefix)\$(change)\$(suffix) in change.\'\<br/\>Setting
\'cash:announce-change\' in \<Game:<Data:NIP:cash:CDO>\>;\<br/\> - from:
nil\<br/\> - to: \"\$(npc) gives you back \$(prefix)\$(change)\$(suffix)
in change.\"\</pre\>\</font\>

\* Now we need to create the \"options\" available to us. These are
\"physical payment\" and \"non-physical payment\", purchase in cash, or
purchase on credit. Each option is, in fact, its own property container
with its own settings.

\* First, we create the credit card option. I name this
\"Game:<Data:NIP:cash:credit>\".

In the new credit card object \"Game:<Data:NIP:cash:credit>\" we set
**\"cash:announce-pay\"** to \<pre\>\"You pay \$(npc)
\$(prefix)\$(paid)\$(suffix) with \$(using).\"\</pre\> 1 \$(npc) is a
Describe() of the NPC (\"a dusky looking merchant\") 2 \$(prefix) and
\$(suffix) are the prefix/suffix of the currency (more in a bit). 3
\$(paid) will resolve the amount of money paid. 4 \$(using) will
describe the item used to make the purchase (\"your VISA-card\").

Set **\"cash:name\"** to \<pre\>\"credit\"\</pre\> This will be the
\$(name) used in the \"announce-shortage\" message.

Set **\"cash:object\"** to \<pre\>\<Game:Props:cash:visa\>\</pre\> (This
is the visa card object we created earlier)

Set **\"cash:physical\"** to \<pre\>0\</pre\>

Set **\"cash:pname\"** to \<pre\>\"dollars\"\</pre\> (This is the word
used to describe the money values)

Set **\"cash:sname\"** to \<pre\>\"dollar\"\</pre\> (This is also used
to describe the money values)

Set **\"cash:suffix\"** to \<pre\>\" dollars\"\</pre\> (This is whatever
you want added to the end of the money values. E.g. 5 dollars, or 3
pence)

Set **\"cash:prefix\"** to \<pre\>\"\$\"\</pre\> (This is whatever you
want added BEFORE the money values. E.g. \$5 dollars)

And the credit is set up.

We now return to the CDO, \"Game:<Data:NIP:cash:CDO>\" Set
**\"cash:options\"** to \<pre\>({ \<Game:<Data:NIP:cash:credit>)
})\</pre\>

The CDO now knows that we can pay for objects using credit. It should
now allow you to buy items, assuming you have a visa card, and a large
enough balance stored in the card.

Since we\'ve set up non-physical payments, we can now set up physical
payments.

\* We create the hard cash option. I name this
\"Game:<Data:NIP:cash:cash-hard>\".

In the new hard cash object \"Game:<Data:NIP:cash:cash-hard>\" we set
**\"cash:announce-pay\"** to \<pre\>\"You hand
\$(prefix)\$(paid)\$(suffix) to \$(npc).\"\</pre\> 1 \$(npc) is a
Describe() of the NPC (\"a dusky looking merchant\") 2 \$(prefix) and
\$(suffix) are the prefix/suffix of the currency (more in a bit). 3
\$(paid) will resolve the amount of money paid.

Set **\"cash:name\"** to \<pre\>\"money\"\</pre\> This will be used in
the error message, \"You do not have enough \<cash:name\> to buy this
item.\"

Set **\"cash:object\"** to \<pre\>(\[ \<Game:Props:cash:1\>:100,
\<Game:Props:cash:2\>:200, \<Game:Props:cash:10\>:1000,
\<Game:Props:cash:20\>:2000, \<Game:Props:cash:50\>:5000,
\<Game:Props:cash:100\>:10000 \])\</pre\> This is a list of cash items,
and their value. List all the notes and coins that we created earlier.
List their values after it. Remember that \$1 has a value of 100. So
\$20 has a value of 2000, and so on.

Set **\"cash:physical\"** to \<pre\>1\</pre\>

Set **\"cash:pname\"** to \<pre\>\"dollars\"\</pre\> The plural name of
the currency.

Set **\"cash:sname\"** to \<pre\>\"dollar\"\</pre\> The singular name of
the currency.

Set **\"cash:prefix\"** to \<pre\>\"\$\"\</pre\> The prefix used when
describing the currency. E.g. \$5.

Set **\"cash:suffix\"** to \<pre\>\" dollars\"\</pre\> The suffix used
when describing the currency. E.g. 5 dollars.

Set **\"cash:range\"** to \<pre\>({ 10000, 1 })\</pre\> The range of
valid cash, used when calculating change/taken cash from the actor in
acts of purchase.

Set **\"cash:slang\"** to \<pre\>(\[ 1 : \"cent\", 25 : \"quarter\", 100
: \"dollar\" \])\</pre\> An optional mapping containing a list of the
\"coins\" or bills which have a slang name, in singular form.

Set **\"cash:plang\"** to \<pre\>(\[ 1 : \"cents\", 25 : \"quarters\",
100 : \"dollars\" \])\</pre\> An optional mapping containing a list of
the \"coins\" or bills which have a slang name, in plural form.

Set **\"cash:type\"** to \<pre\>(\[ 1:\"coin\", 100:\"bill\" \])\</pre\>
The type, exclusively cosmetic, for describing transactions.

Finally, we return to the CDO, \"Game:<Data:NIP:cash:CDO>\" Set
**\"cash:options\"** to include \<pre\>({
\<Game:<Data:NIP:cash:cash-hard>) })\</pre\> (So if you\'d already added
the credit option, it should now look like this \<pre\>({
\<Game:<Data:NIP:cash:cash-hard>), \<Game:<Data:NIP:cash:credit>)
})\</pre\>) (The order in which you add the options is important.
Because the cash-hard is listed first, the character will pay with any
cash they are holding before they pay using their visa card. If we
reversed the order, the character would pay using their visa card
first.)

We\'re now done, and our merchants can accept either hard cash in the
form of notes and coins, or a visa card.

\-- Main.KalleAlm - 16 Feb 2004 Updated \-- Main.TonyDemetriou - 19 Jul
2005
