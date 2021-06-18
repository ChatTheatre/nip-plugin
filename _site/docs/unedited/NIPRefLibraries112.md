%META:TOPICINFO{author=\"kallea\" date=\"1055164360\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPRefLibraries111\"}%
[NIPRefStyle]{.twiki-macro .INCLUDE}

[MerryColorStyles]{.twiki-macro .INCLUDE}

[NIPRefLibrariesTOC]{.twiki-macro .INCLUDE}

\<H2\>1.12: The revised code.\</H2\>

    --- <B>act-post:enter</B> in <B>Marrach:Lib:NIP:lib:mountrider</B>
    <M_COM>/*

      D=The act-post:enter script for the mounting system (NIP), which handles movement through rooms.

    */</M_COM>

    <M_COM>/* The rider has left through the exit. NPC still "on the other side" though. Let's move the NPC as well, but manually. */</M_COM>

    <M_VARS>$mount</M_VARS> = <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT>;
    <M_VARS>$mount</M_VARS>.<M_TXT>"base:environment"</M_TXT> = <M_VARS>$actor</M_VARS>.<M_TXT>"base:environment"</M_TXT>;
    <M_VARS>$mount</M_VARS>.<M_TXT>"base:proximity"</M_TXT> = <M_VARS>$actor</M_VARS>.<M_TXT>"base:proximity"</M_TXT>;

    <M_COM>/* And put the rider back on the mount. */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:proximity"</M_TXT> = <M_VARS>$mount</M_VARS>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:stance"</M_TXT> = <M_CON>STANCE_SIT</M_CON><M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:preposition"</M_TXT> = <M_CON>PREP_ON</M_CON><M_CCS>;</M_CCS>
    ---

Let\'s see how that works.

    ---
    > n
    You begin to enter the gate to the living room.

    A living room.

    You are sitting on a horse. A horse is standing near the gate to the laboratory.

    > n
    A horse moves from the gate to the laboratory to the doors leading to the pool.
    The doors leading to the pool is closed.

    > s
    A horse moves from the doors leading to the pool to the gate to the laboratory.
    You begin to enter the gate to the laboratory.

    Kalle's Laboratory: a windy turret, currently littered with 'Workers, slow down!'-signs and bright red traffic cones.

    StoryCoder Skylar is standing near here. You are sitting on a horse. A horse is standing near the gate to the laboratory. 

    > smile
    You smile.
    ---

That works good! Now, before we call this a version 1.0, let\'s put in a
cute little thing in the mount/unmount scripts, react:jump-dob
(**mounting**) and act:lower (**mountrider**):

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

    <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"You mount "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> this <M_CCS>)</M_CCS>+<M_TXT>"."</M_TXT> <M_CCS>)</M_CCS>;

    <M_COM>/* ... and put the rider ON the NPC */</M_COM>

    <M_VARS>$actor</M_VARS>.<M_TXT>"base:proximity"</M_TXT> = this<M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:stance"</M_TXT> = <M_CON>STANCE_SIT</M_CON><M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:preposition"</M_TXT> = <M_CON>PREP_ON</M_CON><M_CCS>;</M_CCS>

    <M_COM>/* Let's inherit the approach-script we made earlier, in mountrider ... */</M_COM>

    <M_COM>/* First, we gotta figure out where the mountrider object is. */</M_COM>
    <M_VARS>$mountrider</M_VARS> = Call<M_CCS>(</M_CCS> this<M_CCS>,</M_CCS> <M_TXT>"find_nip_object"</M_TXT><M_CCS>,</M_CCS> <M_VARS>$what</M_VARS>: <M_TXT>"mountrider"</M_TXT> <M_CCS>)</M_CCS>;

    <M_COM>/* Then we inherit away! */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:approach"</M_TXT> = <M_VARS>$mountrider</M_VARS>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:lower"</M_TXT> = <M_VARS>$mountrider</M_VARS>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:leave"</M_TXT> = <M_VARS>$mountrider</M_VARS>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:stance"</M_TXT> = <M_VARS>$mountrider</M_VARS>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act-post:enter"</M_TXT> = <M_VARS>$mountrider</M_VARS>;

    <M_COM>/* And we set the 'npc:mounted' property in the NPC to 1 to signal that we're mounted. */</M_COM>

    this<M_CCS>.</M_CCS><M_TXT>"npc:mounted"</M_TXT> = 1<M_CCS>;</M_CCS>

    <B><M_COM>/* Let's replace the base:gait in the actor for when we move through rooms. */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:oldgait"</M_TXT> = <M_VARS>$actor</M_VARS>.<M_TXT>"base:gait"</M_TXT>; <M_COM>/* store old value, just in case */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:gait"</M_TXT> = <M_TXT>"rides"</M_TXT>; <M_COM>/* and set our own */</M_COM></B>

    <M_COM>/* And finally, let's set a "npc:mounting" property in the actor (the rider, not the horse) to the horse object reference (this) */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT> = this<M_CCS>;</M_CCS>
    ---

And act:lower,

    --- <B>act:lower</B> in <B>Marrach:Lib:NIP:lib:mountrider</B> ---
    <M_COM>/*

      D=Script for unmounting NPC's.

    */</M_COM>

    <M_COM>/* Firstly, make sure the rider typed just "lower". We're going to let everything else pass. */</M_COM>

    <M_RVD>if</M_RVD><M_CCS>(</M_CCS> <M_VARS>$dob</M_VARS> <M_CCS>||</M_CCS> <M_VARS>$iob</M_VARS> <M_CCS>)</M_CCS> <M_FUN>return</M_FUN> TRUE<M_CCS>;</M_CCS> <M_COM>/* Roles found, we abort. */</M_COM>

    <M_COM>/* Let's emit something cute right away. */</M_COM>

    <M_VARS>$mount</M_VARS> = <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT>;

    <B><M_COM>/* Let's restore the gait to the old value. */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:gait"</M_TXT> = <M_VARS>$actor</M_VARS>.<M_TXT>"base:oldgait"</M_TXT>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:oldgait"</M_TXT> = nil<M_CCS>;</M_CCS></B>

    <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"You unmount "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$mount</M_VARS> <M_CCS>)</M_CCS>+<M_TXT>"."</M_TXT> <M_CCS>)</M_CCS>;
    <M_FUN>EmitIn</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS>.<M_TXT>"base:environment"</M_TXT><M_CCS>,</M_CCS> <M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS> <M_CCS>)</M_CCS>+<M_TXT>" unmounts "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$mount</M_VARS> <M_CCS>)</M_CCS>+<M_TXT>"."</M_TXT><M_CCS>,</M_CCS> <M_VARS>$actor</M_VARS> <M_CCS>)</M_CCS>;

    <M_COM>/* Now, let's reverse the things done in the mounting script. */</M_COM>

    <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT> = nil<M_CCS>;</M_CCS>
    <M_VARS>$mount</M_VARS>.<M_TXT>"npc:mounted"</M_TXT> = 0<M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:approach"</M_TXT> = nil<M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:leave"</M_TXT> = nil<M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:stance"</M_TXT> = nil<M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act-post:enter"</M_TXT> = nil<M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:lower"</M_TXT> = nil<M_CCS>;</M_CCS>

    <M_COM>/* And finally, set the actor's stance to "standing",
        and preposition to "beside". */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:stance"</M_TXT> = <M_CON>STANCE_STAND</M_CON><M_CCS>;</M_CCS>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:preposition"</M_TXT> = <M_CON>PREP_BESIDE</M_CON><M_CCS>;</M_CCS>

    ---

And our library is working fine. But there are some things that we can
make better right away. For instance, the call to **find_nip_object** in
**react:jump-dob** should be a one-timer only. This introduces a new
aspect of the system, the **merry:lib:init**-script:

This script is going to be placed in the **mounting** lib, as that\'s
the one the NPC actually loads.

    --- <B>lib:init</B> in <B>Marrach:Lib:NIP:lib:mounting</B>
    <M_COM>/*

      D=This script is executed once, when an NPC loads the 'mounting' library.

    */</M_COM>

    this<M_CCS>.</M_CCS><M_TXT>"nip:trait:mounting:riderlib"</M_TXT> = Call<M_CCS>(</M_CCS> this<M_CCS>,</M_CCS> <M_TXT>"find_nip_object"</M_TXT><M_CCS>,</M_CCS> <M_VARS>$what</M_VARS>: <M_TXT>"mountrider"</M_TXT><M_CCS>,</M_CCS> <M_VARS>$options</M_VARS>: nil <M_CCS>)</M_CCS>;
    ---

To see this in action, all we have to do is, yet again, add the library
(mounting) to the NPC. As you can see, it\'s okay to add the same
library multiple times.

    ---
    > +setp horse "add mounting"
    Setting 'add' in &lt;Marrach:Coders:kalle:NPC:stallion>;
    - from: nil
    - to: "mounting"
    Attempting to add library ...
    &lt;Marrach:Lib:NIP:lib:mounting> loaded successfully.

    > +stat horse "property:nip:*
    -- Properties (nip:*)--
    Property: nip:trait:mounting:riderlib = &lt;Marrach:Lib:NIP:lib:mountrider>
    ---

Great! Now all we have to do is open up that pesky **react:jump-dob**
script again and use the \'nip:trait:mounting:riderlib\' property
instead of calling find_nip_object every time.

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
    <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"You mount "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> this <M_CCS>)</M_CCS>+<M_TXT>"."</M_TXT> 

    <B><M_COM>/* Fetch the reference to the riderlib, */</M_COM>
    <M_VARS>$mountrider</M_VARS> = this<M_CCS>.</M_CCS><M_TXT>"nip:trait:mounting:riderlib"</M_TXT>;</B>
    <M_COM>/* Then we inherit away! */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:approach"</M_TXT> = <M_VARS>$mountrider</M_VARS>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:lower"</M_TXT> = <M_VARS>$mountrider</M_VARS>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:leave"</M_TXT> = <M_VARS>$mountrider</M_VARS>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:stance"</M_TXT> = <M_VARS>$mountrider</M_VARS>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act-post:enter"</M_TXT> = <M_VARS>$mountrider</M_VARS>;

    <M_COM>/* And we set the 'npc:mounted' property in the NPC to 1 to signal that we're mounted. */</M_COM>
    this<M_CCS>.</M_CCS><M_TXT>"npc:mounted"</M_TXT> = 1<M_CCS>;</M_CCS>

    <M_COM>/* Let's replace the base:gait in the actor for when we move through rooms. */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:oldgait"</M_TXT> = <M_VARS>$actor</M_VARS>.<M_TXT>"base:gait"</M_TXT>; <M_COM>/* store old value, just in case */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:gait"</M_TXT> = <M_TXT>"rides"</M_TXT>; <M_COM>/* and set our own */</M_COM>

    <M_COM>/* And finally, let's set a "npc:mounting" property in the actor (the rider, not the horse) to the horse object reference (this) */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT> = this<M_CCS>;</M_CCS>
    ---

Now we\'re done. Of course, some improvement can be made. For instance,
we can turn some of the functionality into customizable properties so
the user can tweak the settings and make his NPC more \"unique\". For
instance the \"gait\" we added previously could be turned into something
like \"nip:trait:mounting:rider-gait\". But, as we\'ve come this far,
it\'s time to make this library **public**. Since it\'s actually useful
at this point, we move it from Marrach:Lib:NIP:\... to Lib:NIP:\...

A note to the dear Skotos-Seveners, though. If you put something in
Lib:, it may be lost when Zell decides to make one of his Marrach -\> S7
upgrades. I would hate to see this happen, but if you have created a
functional library and wish to make it available to not only your own
theatre, feel free to email me and I will ensure it\'s distributed and
not destroyed! \-- <kalle@marrach.skotos.net>

[Tweaking it a final time.](NIPRefLibraries1.13)

\-- Main.KalleAlm - 05 Jun 2003
