%META:TOPICINFO{author=\"kallea\" date=\"1055126160\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPRefLibraries110\"}%
[NIPRefStyle]{.twiki-macro .INCLUDE}

[MerryColorStyles]{.twiki-macro .INCLUDE}

[NIPRefLibrariesTOC]{.twiki-macro .INCLUDE}

\<H2\>1.11: Tweaking a bit.\</H2\>

    --- <B>act:approach</B> in <B>Marrach:Lib:NIP:lib:mountrider</B> ---
    <M_COM>/*

      D=Approach script, inherited whenever someone mounts an NPC, which deals with movement issues within rooms.

    */</M_COM>

    <M_COM>/* Instantly put the character in proximity to whatever he's attempting to approach, */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:proximity"</M_TXT> = <M_VARS>$what</M_VARS>;

    <M_COM>/* Force the NPC (which is referred to through 'npc:mounting' in the actor) to perform the approach too. */</M_COM>
    <M_FUN>Act</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT><M_CCS>,</M_CCS> <M_TXT>"approach"</M_TXT><M_CCS>,</M_CCS> <M_VARS>$what</M_VARS>: <M_VARS>$what</M_VARS><B>, <M_VARS>$consent_mapping</M_VARS>: nil</B> <M_CCS>)</M_CCS>;

    <M_COM>/* Quick 100 ms delay, */</M_COM>
    <M_VARS>$delay</M_VARS><M_CCS>(</M_CCS>0<M_CCS>.</M_CCS>1, FALSE<M_CCS>,</M_CCS> <M_TXT>"0c9f"</M_TXT><M_CCS>)</M_CCS>;

    <M_COM>/* And then put the rider back on the mount */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:proximity"</M_TXT> = <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:stance"</M_TXT> = <M_CON>STANCE_SIT</M_CON><M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:preposition"</M_TXT> = <M_CON>PREP_ON</M_CON><M_CCS>;</M_CCS>
    ---

And now, let\'s try again:

    ---
    > leave
    A horse moves away from StoryCoder Skylar.

    > stand by skylar
    StoryCoder Skylar allows you to stand by her.

    A horse approaches StoryCoder Skylar.
    You stand up near StoryCoder Skylar.
    ---

Well\... I\'d say that works. At least for the time being. We have
another issue to address\...

    ---
    > look
    [general description]

    StoryCoder Skylar is standing near here. You are sitting on a horse. A horse is standing near StoryCoder Skylar.

    > stand before skylar
    StoryCoder Skylar allows you to stand before her.

    You stand up in front of StoryCoder Skylar.

    > look
    [general description]

    StoryCoder Skylar is standing near here. You are sitting on a horse. A horse is standing near StoryCoder Skylar.
    ---

As you see, the horse isn\'t standing in front of Skylar, as it should.
We address that issue in the following script,

    --- <B>act:stance</B> in <B>Marrach:Lib:NIP:lib:mountrider</B> ---
    <M_COM>/*

      D=Stance handler for mounted NPC's. This script ensures stances are displayed correctly.

    */</M_COM>

    <M_COM>/* Here, we simply forward the action to the horse, but we put the 
        stance to "standing". Don't want any kneeling horses here... */</M_COM>

    <M_FUN>Act</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT><M_CCS>,</M_CCS> <M_TXT>"stance"</M_TXT><M_CCS>,</M_CCS> <M_VARS>$stance</M_VARS>: <M_CON>STANCE_STAND</M_CON> <M_CCS>)</M_CCS>;
    ---

Well, that was simple enough. And the simple explanation is that we
trust the actions will be \"forwarded\" as we\'ve seen them be before
(in act:approach). Let\'s try this out.

    ---
    > step to skylar briskly "Hey there pa dig there!"
    StoryCoder Skylar allows you to step her.

    You step to StoryCoder Skylar briskly, "Hey there pa dig there!"

    > look
    [...]

    StoryCoder Skylar is standing near here. You are sitting on a horse. A horse is standing in front of StoryCoder Skylar.

    > leave
    A horse moves away from StoryCoder Skylar.

    > step to skylar consideringly
    StoryCoder Skylar allows you to step her.
    A horse approaches StoryCoder Skylar.

    You step to StoryCoder Skylar consideringly.

    > step to floor
    A horse moves from StoryCoder Skylar to the floor.
    You step to the floor.

    > stand on floor
    A horse stands up on the floor.

    > step to skylar
    StoryCoder Skylar allows you to step her.

    A horse moves from the floor to StoryCoder Skylar.
    You step to StoryCoder Skylar.

    > sit behind skylar
    StoryCoder Skylar allows you to sit behind her.

    A horse stands up behind StoryCoder Skylar.

    > kneel before skylar
    StoryCoder Skylar allows you to kneel before her.

    A horse stands up in front of StoryCoder Skylar.

    > nod satisfied
    You nod satisfiedly.
    ---

It seems we\'re getting close to finished here. All we really have left
to do is **act:enter**, which is probably not going to be too difficult
to do. If we look at the signal table again,

  -------- ----- ----- ------ ------ ------ ------------------------------- ------ -------------------------------
  signal   pre   sig   post   arg    type   description                     role   description
  enter    X     X     X      what   NRef   detail we\'re trying to enter   \*     detail we\'re trying to enter
                                                                            from   detail we emerge from
                                                                            into   detail we enter into
  -------- ----- ----- ------ ------ ------ ------------------------------- ------ -------------------------------

We see clearly what it is we need to do. What we\'re going to do, to
make it clear who\'s actually doing what, is to make sure the message
goes \"StoryCoder Kalle leaves through \...\", not \"A horse leaves
through.\"\<br\> If there are several horses in the same environment and
they move in and out, it\'s going to confuse the living snot out of
anyone trying to keep track of who\'s where. The simple solution,
codewise, is to let the actor\'s enter go through, catch the post-phase
and manually teleport NPC and put rider on NPC manually, once safely on
the other side.

[The revised code.](NIPRefLibraries1.12)

\-- Main.KalleAlm - 05 Jun 2003
