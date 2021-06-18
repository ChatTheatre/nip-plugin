%META:TOPICINFO{author=\"kallea\" date=\"1076292425\" format=\"1.0\"
version=\"1.6\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPTodoStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>TODO: Merchants system\</FONT\>

\<font class=\"query\"\>PROJECT STATUS\</font\> COMPLETED.

\<font class=\"query\"\>STATUS NOTES\</font\>

This system is completed and is located on Skotos Seven and Castle
Marrach, with an example NPC \-- summon
Examples:complete:NIP:trading:burger-king-dude to see this.

\<font class=\"query\"\>ASSIGNED CODER(S)\</font\>

  --------------- ---------- ----------------------------
  **Who**         **From**   **Contact information**
  Main.KalleAlm   Skotos     <kalle@marrach.skotos.net>
  --------------- ---------- ----------------------------

\<font class=\"query\"\>WHAT?\</font\> A commerce system for NIP.

\<font class=\"query\"\>PRIORITY\</font\> VERY HIGH

\<font class=\"query\"\>ETA?\</font\> Completed february 8th, 2004.

\<font class=\"query\"\>HOW WILL IT WORK?\</font\>

1 A data object will be required. This object will contain
currency-specific data, and will support things like credit card
transactions, physical cash trade, etc. 2 A library called \"trading\"
will be made, which each NPC merchant will use and have set up to use
the data object spec. in \#1.

\<font class=\"query\"\>GENERAL DESCRIPTION\</font\>

    ---
    > ask cook for hamburger
    You do not have enough cash for a hamburger.

    > open my wallet
    You open your wallet.

    > take money from my wallet
    You take $4.22 from your wallet.

    > ask cook for hamburger
    This item will cost you $0.10.
    A cook offers a hamburger to you.
    Type 'accept from cook' to take this item.
    Type 'refuse cook' to refuse to take it.

    > accept hamburger
    You take a hamburger from a cook.
    You hand a dime to a cook.
    ---

Future (v 2) additions: haggling. Further information to be enclosed
when the time comes for such implementations.

\<font class=\"query\"\>LIBRARIES\</font\>

    [Library]         [Description]
    trading          The trading library, used in all NPC merchants.

\<font class=\"query\"\>TECHNICAL COMMENTS\</font\>

A temporary \"react:take\" script in the traded item would suffice,
which would ensure the user still had the money available etc. and
deducted it upon taking. (check if sig%name works)

\*Script requires (and replaces parts of)
[presents](NIPLibRefPresents)\*

merry:lib:handler:ask-for (replacing presents v.)

merry:lib:core_trading_query_assets \-- check if \$actor has a certain
amount of money

merry:lib:core_trading_deduct \-- deduct a certain amount of money from
\$actor

Act( \$actor, \"offer\", \$who: object, \$what: ({ object, \... }) );

Property in purchaseable objects which determines price:
\"nip:item:cost\"

\<font class=\"query\"\>LIST OF INTERESTED PARTIES\</font\>

If this subject interests you, please add yourself to the list below.
The more interest, the higher priority a subject will get. And also, by
doing so, we will be able to notify you specifically when this
subject\'s status has changed.

    [Your Name]      [Your Email]
    [insert a separate line above this one]

\-- Main.KalleAlm - 05 Feb 2004

\<font class=\"query\"\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT
THIS SUBJECT\</font\>\<br\> (Please, don\'t forget to add your name to
your comment, preferably your TWiki-name.)
