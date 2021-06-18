%META:TOPICINFO{author=\"kallea\" date=\"1055125353\" format=\"1.0\"
version=\"1.4\"}% %META:TOPICPARENT{name=\"NIPRefLibraries16\"}%
[NIPRefStyle]{.twiki-macro .INCLUDE}

[MerryColorStyles]{.twiki-macro .INCLUDE}

[NIPRefLibrariesTOC]{.twiki-macro .INCLUDE}

\<H2\>1.7: Creating the act:approach script.\</H2\>

    --- <B>act:approach</B> in <B>Marrach:Lib:NIP:lib:mountrider</B> ---
    <M_COM>/*

      D=Approach script, inherited whenever someone mounts an NPC, which deals with movement issues within rooms.

    */</M_COM>

    <M_COM>/* Instantly put the character in proximity to whatever he's attempting to approach, */</M_COM>
    <M_VARS>$actor</M_VARS><M_CCS>.</M_CCS><M_TXT>"base:proximity"</M_TXT> = <M_VARS>$what</M_VARS><M_CCS>;</M_CCS>

    <M_COM>/* Force the NPC (which is referred to through 'npc:mounting' in the actor) to perform the approach too. */</M_COM>
    Act<M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>.</M_CCS><M_TXT>"npc:mounting"</M_TXT><M_CCS>,</M_CCS> <M_TXT>"approach"</M_TXT><M_CCS>,</M_CCS> <M_VARS>$what</M_VARS>: <M_VARS>$what</M_VARS> <M_CCS>)</M_CCS>;

    <M_COM>/* Quick 100 ms delay, */</M_COM>
    <M_VARS>$delay</M_VARS><M_CCS>(</M_CCS> 0<M_CCS>.</M_CCS>1, FALSE <M_CCS>)</M_CCS>;

    <M_COM>/* And then put the rider back on the mount */</M_COM>
    <M_VARS>$actor</M_VARS><M_CCS>.</M_CCS><M_TXT>"base:proximity"</M_TXT> = <M_VARS>$actor</M_VARS><M_CCS>.</M_CCS><M_TXT>"npc:mounting"</M_TXT>;
    <M_VARS>$actor</M_VARS><M_CCS>.</M_CCS><M_TXT>"base:stance"</M_TXT> = <M_CON>STANCE_SIT</M_CON><M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS><M_CCS>.</M_CCS><M_TXT>"base:preposition"</M_TXT> = <M_CON>PREP_ON</M_CON><M_CCS>;</M_CCS>
    ---

Now that we have that script dealt with, let\'s go back and look at the
**react:jump-dob**-script in **mounting** again.

**Bold areas are new and/or modified segments of the code**

    --- <B>react:jump-dob</B> in <B>Marrach:Lib:NIP:lib:mounting</B> ---
    <M_COM>/*

        D=This script deals with mounting an NPC.

    */</M_COM>

    <M_RVD>if</M_RVD><M_CCS>(</M_CCS> this<M_CCS>.</M_CCS><M_TXT>"npc:mounted"</M_TXT> <M_CCS>)</M_CCS> <M_CCS>{</M_CCS> <M_COM>/* Someone is mounting the NPC already... */</M_COM>
      <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"You can't mount "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS>this<M_CCS>)</M_CCS>+<M_TXT>" as "</M_TXT>+this<M_CCS>.</M_CCS><M_TXT>"trait:nominative"</M_TXT>+<M_TXT>" is already being mounted."</M_TXT> <M_CCS>)</M_CCS>;
      <M_FUN>return</M_FUN> FALSE<M_CCS>;</M_CCS>
    <M_CCS>}</M_CCS>

    <B><M_COM>/* Let's also check if the actor is mounting something currently */</M_COM>
    <M_RVD>if</M_RVD><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>.</M_CCS><M_TXT>"npc:mounting"</M_TXT> <M_CCS>)</M_CCS> <M_COM>/* Actor is already mounting something. */</M_COM>
      <M_RVD>if</M_RVD><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>.</M_CCS><M_TXT>"npc:mounting"</M_TXT> == this <M_CCS>)</M_CCS> <M_CCS>{</M_CCS> <M_COM>/* Actor is mounting this NPC already! */</M_COM>
         <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"You are already mounting "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> this <M_CCS>)</M_CCS>+<M_TXT>"!"</M_TXT> <M_CCS>)</M_CCS>;
         <M_FUN>return</M_FUN> FALSE<M_CCS>;</M_CCS>
      <M_CCS>}</M_CCS> <M_RVD>else</M_RVD> <M_CCS>{</M_CCS> <M_COM>/* Actor is mounting something else. */</M_COM>
         <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"You are already mounting "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>.</M_CCS><M_TXT>"npc:mounting"</M_TXT> <M_CCS>)</M_CCS>+<M_TXT>"!"</M_TXT> <M_CCS>)</M_CCS>;
         <M_FUN>return</M_FUN> FALSE<M_CCS>;</M_CCS>
      <M_CCS>}</M_CCS></B>

    <M_COM>/* If we get here, the NPC isn't mounted. Let's print some pretty message describing what happens, */</M_COM>

    <M_FUN>EmitIn</M_FUN><M_CCS>(</M_CCS> this<M_CCS>.</M_CCS><M_TXT>"base:environment"</M_TXT><M_CCS>,</M_CCS> <M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS> <M_CCS>)</M_CCS>+<M_TXT>" mounts "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> this <M_CCS>)</M_CCS>+<M_TXT>"."</M_TXT><M_CCS>,</M_CCS> <M_VARS>$actor</M_VARS> <M_CCS>)</M_CCS>;
    <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"You mount "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> this <M_CCS>)</M_CCS>+<M_TXT>"."</M_TXT> <M_CCS>)</M_CCS>;

    <B><M_COM>/* ... and put the rider ON the NPC */</M_COM>

    <M_VARS>$actor</M_VARS><M_CCS>.</M_CCS><M_TXT>"base:proximity"</M_TXT> = this<M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS><M_CCS>.</M_CCS><M_TXT>"base:stance"</M_TXT> = <M_CON>STANCE_SIT</M_CON><M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS><M_CCS>.</M_CCS><M_TXT>"base:preposition"</M_TXT> = <M_CON>PREP_ON</M_CON><M_CCS>;</M_CCS>

    <M_COM>/* Let's inherit the approach-script we made earlier, in mountrider ... */</M_COM>

    <M_COM>/* First, we gotta figure out where the mountrider object is. */</M_COM>
    <M_VARS>$mountrider</M_VARS> = Call<M_CCS>(</M_CCS> this<M_CCS>,</M_CCS> <M_TXT>"find_nip_object"</M_TXT><M_CCS>,</M_CCS> <M_VARS>$what</M_VARS>: <M_TXT>"mountrider"</M_TXT> <M_CCS>)</M_CCS>;

    <M_COM>/* Then we inherit away! */</M_COM>
    <M_VARS>$actor</M_VARS><M_CCS>.</M_CCS><M_TXT>"merry:inherit:act:approach"</M_TXT> = <M_VARS>$mountrider</M_VARS><M_CCS>;</M_CCS>

    <M_COM>/* And we set the 'npc:mounted' property in the NPC to 1 to signal that we're mounted. */</M_COM>
    this<M_CCS>.</M_CCS><M_TXT>"npc:mounted"</M_TXT> = 1<M_CCS>;</M_CCS></B>

    <M_COM>/* And finally, let's set a "npc:mounting" property in the actor (the rider, not the horse) to the horse object reference (this) */</M_COM>
    <M_VARS>$actor</M_VARS><M_CCS>.</M_CCS><M_TXT>"npc:mounting"</M_TXT> = this<M_CCS>;</M_CCS>
    ---

We\'ve added in three major things now. Firstly, the check to see if the
actor is already riding something else. Secondly, the actual \"putting
the rider on the mount\". And thirdly, the actual inheritage of the
approach script. We\'re going to optimize that a little later on (the
call to \"find_nip_object\" is unnecessary **every** time someone mounts
the NPC), but we\'ll leave it as is for now.

This time, we haven\'t **added** any scripts. That means we can mount
again without having to re-add the library in the NPC.

    ---
    > jump horse
    You are already mounting a horse!

    > smile "Great, that works!"
    You smile, "Great, that works!"

    > +setp me "npc:mounting nil"
    Setting 'npc:mounting' in &lt;Marrach:players:K:kalle>;
    - from: &lt;Marrach:Coders:kalle:NPC:stallion>
    - to: nil

    > jump horse
    You mount a horse.

    > +stat horse "property:npc:*"
    -- Properties (npc:*)--
    Property: npc:mounted = 1

    > +stat me "property:npc:*"
    -- Properties (npc:*)--
    Property: npc:mounting = &lt;Marrach:Coders:kalle:NPC:stallion>

    > approach floor
    A horse approaches the floor.

    > look 
    [general description]

    StoryCoder Skylar is standing near here. You are sitting on a horse. A horse is standing near the floor.

    > step to skylar
    StoryCoder Skylar allows you to step her.

    A horse moves from the floor to StoryCoder Skylar.
    You step to StoryCoder Skylar.

    A horse steps to StoryCoder Skylar.
    <B>Hmm...</B>
    ---

Okay, we\'re finally getting somewhere! Still have some issues to deal
with though. Like the fact I and the horse approached Skylar. This is an
unpexpected occurance, but we will ignore it for now. Instead, we\'re
going to look into dismounting the NPC. The script, act:lower, in the
**mountrider** library, is going to deal with this.

[The act:lower script, a.k.a dismounting the mount.](NIPRefLibraries1.8)

\-- Main.KalleAlm - 05 Jun 2003
