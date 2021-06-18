%META:TOPICINFO{author=\"kallea\" date=\"1066674321\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>HOW TO make NPC\'s interact with each
other?\</FONT\>

**How:**

\<a name=\"quick\"\> \</a\> \<font color=\"\#0000ff\"\>QUICK
HOW-TO:\</font\>\<br\> *(if you feel comfident with the system, you
might want to read this quicker description; otherwise you might want to
\<a href=\"\#long\"\>hop down to the more explanative version\</a\>)*

This is a check-list for what you will need to do in order to make two
NPC\'s interact with each other: \* You, naturally, need two NPC\'s set
up with the [emoting](NIPLibRefEmoting) library added. \* You must then
add the [interaction](NIPLibRefInteraction) library to both NPC\'s. \*
At least one behavior data object must be set up (in case they\'re \"of
the same type\", you only need one, otherwise you need two). \*
*Optionally, you can set the \'nip:group\' property in the NPC, to
define more specifically what kind of NPC it is. If you do this,
however, you must record for the group-name in the next step, instead of
\'nip\'.* \* You need to record **specifically** for the interaction, by
using the +nip tool \"scene\" to name the other \"npc\" ([see
tutorial](NIPTutorialScenery)), in all behavior data objects, for the
mood \'nip\'. \* Both NPC\'s must be set up to use these, by setting the
**\'nip:trait:interaction:db\'** property in them to point at their
respective behavior data objects.

*For testing purposes, you might want to set the property
\'nip:trait:interaction:chance\' to 1. This property determines how big
of a chance it is that an NPC should \"broadcast request\" or \"accept
requests\". Its default is 10 (which is 10%; 1 is 100%, 100 is 1%, etc.)
which means the you will see some interaction approximately once every
6th minute, which is a long wait if you just want to see if it works.
Just don\'t forget to set it back up to \~10 when you\'re finished, or
your NPC\'s will be spam-beasts.*

\<hr noshade\>

\<a name=\"long\"\> \</a\> \<font color=\"\#0000ff\"\>EXPLANATIVE
HOW-TO:\</font\>\<br\> *(if you feel comfident with the system, you
might want to \<a href=\"\#quick\"\>hop up to the quicker
description\</a\>; otherwise you probably want to read this more
explanative version)*

This description shows an example on how to set two NPC\'s up to
interact with each other:

*I have two NPC\'s; George and Lucy. I want George to occasionally wave
to Lucy, and I want Lucy to occasionally wink at George. Simple enough,
eh? This is what I do, initially.*

------------------------------------------------------------------------

    > +setp george "add emoting"
    Setting 'add' in &lt;Examples:George> to "emoting"
    Attempting to add library ...
    The 'emoting' library/hook has been loaded. Before your NPC will react, however, you must use (and 
    make, if you haven't already) a behavior database.
    &lt;Lib:NIP:lib:emoting> loaded successfully.

    > +setp lucy "add emoting"
    [...]

    <strong>[Now that I have the emoting libs loaded (note: if you already have emoting, there's no point adding
     it again), I'm going to add the actual 'interaction' library as well.]</strong>

    > +setp george "add nip"
    Setting 'add' in &lt;Examples:George> to "nip"
    Attempting to add library ...
    - dependencies found. Checking prerequisites ...
    - OK.
    The NIP (NPC Interaction Protocol) has been loaded into the NPC. You can now create NPC-NPC 
    interaction behavior, using the 'record' +nip-tool. See troll TWiki for further information.
    &lt;Lib:NIP:lib:interaction> loaded successfully.

    > +setp lucy "add nip"
    [...]

    <strong>[Next, I have to create two propertycontainers for their behavior.]</strong>
    <ul>
    > +cobj propcontainer "Data:NIP:behavior:kalle:george"
    OK.
    > +cobj propcontainer "Data:NIP:behavior:kalle:lucy"
    OK.
    </ul>
    <strong>[Thirdly, I need to record for each of them.]</strong>

    > +nip "record start Data:NIP:behavior:kalle:george nip"

    > +nip lucy "scene npc"
    Scene role (npc) set to Lucy.

    > wave to lucy "!Hi Lucy!"
    You wave to Lucy, "!Hi Lucy!"
    [STO:1]

    > +nip "scene --"
    Scene deleted.

    <strong>[And for Lucy too.]</strong>

    > +nip "record start Data:NIP:behavior:kalle:lucy nip"

    > +nip george "scene npc"
    Scene role (npc) set to George.

    > wink at george "!Hey George!"
    You wink at George, "!Hey George!"
    [STO:1]

    > +nip "scene --"
    Scene deleted.

    > +nip "record stop"

    <strong>[There we go! Now we only need to set a few values and see if Lucy and George will work 
    together.]</strong>

    > +setp george "nip:trait:interaction:db &lt;Data:NIP:behavior:kalle:george>"

    > +setp lucy "nip:trait:interaction:db &lt;Data:NIP:behavior:kalle:lucy>"

    <strong>[And we're done. But let's temporarily set the chance of interaction to 100% (1) to make 
    sure things work as they should. And, unless already enabled, let's turn the NPC's on.]</strong>

    > +setp george and lucy "nip:trait:interaction:chance 1"

    > +nip george "live"

    > +nip lucy "live"

    <strong>[And now, simply wait for them to act. Once they've done so (should take about a minute) 
    return the chance value to 10 (10%)]</strong>

    > +setp george and lucy "nip:trait:interaction:chance 10"

\-- Main.KalleAlm - 07 Sep 2003
