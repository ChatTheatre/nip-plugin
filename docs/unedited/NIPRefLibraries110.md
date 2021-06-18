%META:TOPICINFO{author=\"kallea\" date=\"1055126039\" format=\"1.0\"
version=\"1.4\"}% %META:TOPICPARENT{name=\"NIPRefLibraries19\"}%
[NIPRefStyle]{.twiki-macro .INCLUDE}

[MerryColorStyles]{.twiki-macro .INCLUDE}

[NIPRefLibrariesTOC]{.twiki-macro .INCLUDE}

\<H2\>1.10: The three remaining scripts.\</H2\>

    --- <B>act:leave</B> in <B>Marrach:Lib:NIP:lib:mountrider</B> ---
    <M_COM>/*

      D=Leave script, inherited whenever someone mounts an NPC, which deals with movement issues within rooms.

    */</M_COM>

    <M_COM>/* Force the NPC (which is referred to through 'npc:mounting' in the actor) to perform the leave. */</M_COM>
    Act<M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT><M_CCS>,</M_CCS> <M_TXT>"leave"</M_TXT> <M_CCS>)</M_CCS>;

    <M_COM>/* And then put the rider back on the mount */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:proximity"</M_TXT> = <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:stance"</M_TXT> = <M_CON>STANCE_SIT</M_CON><M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:preposition"</M_TXT> = <M_CON>PREP_ON</M_CON><M_CCS>;</M_CCS>
    ---

Once again, we need to go into the jump-script, but this time we\'re
going to have some forethought and inherit all scripts, even those we
haven\'t created yet.

    --- <B>react:jump-dob</B> in <B>Marrach:Lib:NIP:lib:mounting</B> ---
    <M_COM>/*

        D=This script deals with mounting an NPC.

    */</M_COM>

    <M_RVD>if</M_RVD><M_CCS>(</M_CCS> this<M_CCS>.</M_CCS><M_TXT>"npc:mounted"</M_TXT> <M_CCS>)</M_CCS> <M_CCS>{</M_CCS> <M_COM>/* Someone is mounting the NPC already... */</M_COM>
      <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"You can't mount "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS>this<M_CCS>)</M_CCS>+<M_TXT>" as "</M_TXT>+this<M_CCS>.</M_CCS><M_TXT>"trait:nominative"</M_TXT>+<M_TXT>" is already being mounted."</M_TXT> <M_CCS>)</M_CCS>;
      <M_FUN>return</M_FUN> FALSE<M_CCS>;</M_CCS>
    <M_CCS>}</M_CCS>

    <M_COM>/* Let's also check if the actor is mounting something currently */</M_COM>
    <M_RVD>if</M_RVD><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT> <M_CCS>)</M_CCS> <M_COM>/* Actor is already mounting something. */</M_COM>
      <M_RVD>if</M_RVD><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT> == this <M_CCS>)</M_CCS> <M_CCS>{</M_CCS> <M_COM>/* Actor is mounting this NPC already! */</M_COM>
         <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"You are already mounting "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> this <M_CCS>)</M_CCS>+<M_TXT>"!"</M_TXT> <M_CCS>)</M_CCS>;
         <M_FUN>return</M_FUN> FALSE<M_CCS>;</M_CCS>
      <M_CCS>}</M_CCS> <M_RVD>else</M_RVD> <M_CCS>{</M_CCS> <M_COM>/* Actor is mounting something else. */</M_COM>
         <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"You are already mounting "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT> <M_CCS>)</M_CCS>+<M_TXT>"!"</M_TXT> <M_CCS>)</M_CCS>;
         <M_FUN>return</M_FUN> FALSE<M_CCS>;</M_CCS>
      <M_CCS>}</M_CCS>

    <M_COM>/* If we get here, the NPC isn't mounted. Let's print some pretty message describing what happens, */</M_COM>

    <M_FUN>EmitIn</M_FUN><M_CCS>(</M_CCS> this<M_CCS>.</M_CCS><M_TXT>"base:environment"</M_TXT><M_CCS>,</M_CCS> <M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS> <M_CCS>)</M_CCS>+<M_TXT>" mounts "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> this <M_CCS>)</M_CCS>+<M_TXT>"."</M_TXT><M_CCS>,</M_CCS> <M_VARS>$actor</M_VARS> <M_CCS>)</M_CCS>;
    <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"You mount "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> this <M_CCS>)</M_CCS>+<M_TXT>"."</M_TXT> <B><M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:leave"</M_TXT> = <M_VARS>$mountrider</M_VARS>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:stance"</M_TXT> = <M_VARS>$mountrider</M_VARS>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act-post:enter"</M_TXT> = <M_VARS>$mountrider</M_VARS>;</B>

    <M_COM>/* And we set the 'npc:mounted' property in the NPC to 1 to signal that we're mounted. */</M_COM>
    this<M_CCS>.</M_CCS><M_TXT>"npc:mounted"</M_TXT> = 1<M_CCS>;</M_CCS>

    <M_COM>/* And finally, let's set a "npc:mounting" property in the actor (the rider, not the horse) to the horse object reference (this) */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT> = this<M_CCS>;</M_CCS>
    ---

\- and let\'s do the same with the dismounting script, act:lower in
**mountrider**

    --- <B>act:lower</B> in <B>Marrach:Lib:NIP:lib:mountrider</B> ---
    <M_COM>/*

      D=Script for dismounting NPC's.

    */</M_COM>

    <M_COM>/* Firstly, make sure the rider typed just "lower". We're going to let everything else pass. */</M_COM>

    <M_RVD>if</M_RVD><M_CCS>(</M_CCS> <M_VARS>$dob</M_VARS> <M_CCS>||</M_CCS> <M_VARS>$iob</M_VARS> <M_CCS>)</M_CCS> <M_FUN>return</M_FUN> TRUE<M_CCS>;</M_CCS> <M_COM>/* Roles found, we abort. */</M_COM>

    <M_COM>/* Let's emit something cute right away. */</M_COM>

    <M_VARS>$mount</M_VARS> = <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT>;


    <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"You dismount "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$mount</M_VARS> <M_CCS>)</M_CCS>+<M_TXT>"."</M_TXT> <M_CCS>)</M_CCS>;
    <M_FUN>EmitIn</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS>.<M_TXT>"base:environment"</M_TXT><M_CCS>,</M_CCS> <M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS> <M_CCS>)</M_CCS>+<M_TXT>" dismounts "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$mount</M_VARS> <M_CCS>)</M_CCS>+<M_TXT>"."</M_TXT><M_CCS>,</M_CCS> <M_VARS>$actor</M_VARS> <M_CCS>)</M_CCS>;

    <M_COM>/* Now, let's reverse the things done in the mounting script. */</M_COM>

    <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT> = nil<M_CCS>;</M_CCS>
    <M_VARS>$mount</M_VARS>.<M_TXT>"npc:mounted"</M_TXT> = 0<M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:approach"</M_TXT> = nil<M_CCS>;</M_CCS>
    <B><M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:leave"</M_TXT> = nil<M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:stance"</M_TXT> = nil<M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act-post:enter"</M_TXT> = nil<M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:lower"</M_TXT> = nil<M_CCS>;</M_CCS></B>
    <M_COM>/* And finally, set the actor's stance to "standing",
        and preposition to "beside". */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:stance"</M_TXT> = <M_CON>STANCE_STAND</M_CON><M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:preposition"</M_TXT> = <M_CON>PREP_BESIDE</M_CON><M_CCS>;</M_CCS>
    ---

To make use of the new code we\'ve made, we just have to jump the horse
again, since the **react:jump-dob**-script will put us \"up-to-date\",

    ---
    > jump horse
    You mount a horse.

    > +stat me "property:merry:inherit:act:*
    -- Properties (merry:inherit:act:*)--
    Property: merry:inherit:act:approach = &lt;Marrach:Lib:NIP:lib:mountrider>
    Property: merry:inherit:act-post:enter = &lt;Marrach:Lib:NIP:lib:mountrider>
    Property: merry:inherit:act:leave = &lt;Marrach:Lib:NIP:lib:mountrider>
    Property: merry:inherit:act:lower = &lt;Marrach:Lib:NIP:lib:mountrider>
    Property: merry:inherit:act:stance = &lt;Marrach:Lib:NIP:lib:mountrider>

    > look
    [general description]

    StoryCoder Skylar is standing near here. You are sitting on a horse. A horse is standing near the floor.

    > approach skylar
    A horse moves away from the floor.

    > look
    [general description]

    A horse and StoryCoder Skylar are standing near here. You are sitting on a horse.

    > approach skylar

    <B>Hmm.</B>
    ---

After some tests, I came to the conclusion that the system decided it
was smart if I, instead of approaching someone (as I asked for), left
the horse first. Which I can\'t. This is either a bug that someone else
will address, or it\'s a feature we can\'t really do much about. Let\'s
test some more.

    ---
    > step to skylar

    StoryCoder Skylar allows you to step her.
    A horse approaches StoryCoder Skylar.
    You step to StoryCoder Skylar.

    A horse steps to StoryCoder Skylar.

    > look
    [general description]

    StoryCoder Skylar is standing near here. You are sitting on a horse. A horse is standing near StoryCoder Skylar.

    > leave
    A horse moves away from StoryCoder Skylar.

    > look
    [general description]

    A horse and StoryCoder Skylar are standing near here. You are sitting on a horse.
    ---

Everything but a few minor issues seems to work so far! Great! Let\'s go
ahead and tackle the stance-issue (where the horse and I both approach).
Temporarily, we\'re adding a little point to the act:approach-script,
which seems to be where this problem occurs.

    --- <B>act:approach</B> in <B>Marrach:Lib:NIP:lib:mountrider</B> ---
    <M_COM>/*

      D=Approach script, inherited whenever someone mounts an NPC, which deals with movement issues within rooms.

    */</M_COM>

    <M_COM>/* Instantly put the character in proximity to whatever he's attempting to approach, */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:proximity"</M_TXT> = <M_VARS>$what</M_VARS>;

    <M_COM>/* Force the NPC (which is referred to through 'npc:mounting' in the actor) to perform the approach too. */</M_COM>

    <B>
    <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> dump_value<M_CCS>(</M_CCS> args <M_CCS>)</M_CCS>)<M_CCS>;</M_CCS>
    </B>
    <M_FUN>Act</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT><M_CCS>,</M_CCS> <M_TXT>"approach"</M_TXT><M_CCS>,</M_CCS> <M_VARS>$what</M_VARS>: <M_VARS>$what</M_VARS> <M_CCS>)</M_CCS>;

    <M_COM>/* Quick 100 ms delay, */</M_COM>
    <M_VARS>$delay</M_VARS><M_CCS>(</M_CCS>0<M_CCS>.</M_CCS>1, FALSE<M_CCS>,</M_CCS> <M_TXT>"0c9f"</M_TXT><M_CCS>)</M_CCS>;

    <M_COM>/* And then put the rider back on the mount */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:proximity"</M_TXT> = <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:stance"</M_TXT> = <M_CON>STANCE_SIT</M_CON><M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:preposition"</M_TXT> = <M_CON>PREP_ON</M_CON><M_CCS>;</M_CCS>
    ---

Test it.

    ---
    > stand by skylar
    StoryCoder Skylar allows you to stand by her.
    ([ "actor":<Marrach:players:K:kalle>, "consent_mapping":([ "action":"stance", "args":([ "prep":256, "stance":5, "target":(43)O(/base/data/nref#-1, <Marrach:players:S:skylar>, "default") ]), "message":"stand by" ]), "consented":1, "current-action":"approach", "target":(43)O(/base/data/nref#-1, <Marrach:players:S:skylar>, "default"), "targets":(43)O(/base/data/nref#-1, <Marrach:players:S:skylar>, "default"), "this":<Marrach:players:K:kalle>, "what":(43)O(/base/data/nref#-1, <Marrach:players:S:skylar>, "default"), "witnesses":({ <Marrach:Coders:kalle:rooms:home>, ({ <Marrach:Coders:kalle:NPC:stallion> }) }) ])

    A horse approaches StoryCoder Skylar.

    A horse stands up near StoryCoder Skylar.
    ---

Woah! Okay. If we squint and peer very carefully, it seems the big
variable **consent_mapping** is causing trouble. It\'s actually sending
what to do next, on to the horse! No wonder the horse did the stance as
well.

[Let\'s go in and tweak just a bit\...](NIPRefLibraries1.11)

\-- Main.KalleAlm - 05 Jun 2003
