%META:TOPICINFO{author=\"kallea\" date=\"1055164987\" format=\"1.0\"
version=\"1.4\"}% %META:TOPICPARENT{name=\"NIPRefLibraries112\"}%
[NIPRefStyle]{.twiki-macro .INCLUDE}

[MerryColorStyles]{.twiki-macro .INCLUDE}

[NIPRefLibrariesTOC]{.twiki-macro .INCLUDE}

\<H2\>1.13: Tweaking it a final time.\</H2\>

Well, our lib is done and useable. It may not be flawless, fantastic,
perfect, but it\'s definintely something. However, we\'re going to take
a few more steps into making it even more useful.

First off, we\'re going to turn the static gait (\"rides\") into a
customizable property. That will introduce a new library property:

\* **init:properties** - Which is used to set initial default values to
properties in NPC\'s that load the library in question.

So, we\'ll set this property in the **mounting** lib (which we\'ve at
this point renamed to **\<Lib:NIP:lib:mounting\>**) to:

\* (\[ \"nip:trait:mounting:rider-gait\" : \"rides\" \])

This means that whenever someone adds the **mounting** library to an
NPC, the property **\"nip:trait:mounting:rider-gait\"** in the NPC will
be set to **\"rides\"**, unless it\'s set to something already, in which
case the old value is saved.

Let\'s test this:

    ---
    > +setp "Lib:NIP:lib:mounting init:properties ([ "nip:trait:mounting:rider-gait" : "rides" ])"
    Setting 'init:properties' in &lt;Lib:NIP:lib:mounting>;
    - from: nil
    - to: ([ "nip:trait:mounting:rider-gait":"rides" ])

    > +setp horse "add mounting"
    Setting 'add' in &lt;Marrach:Coders:kalle:NPC:stallion>;
    - from: nil
    - to: "mounting"
    Attempting to add library ...
    &lt;Lib:NIP:lib:mounting> loaded successfully.

    > +stat horse "property:nip:trait:*"
    -- Properties (nip:trait:*)--
    Property: nip:trait:mounting:rider-gait = "rides"
    Property: nip:trait:mounting:riderlib = &lt;Lib:NIP:lib:mountrider>
    ---

Tada! There we have it! Now, let\'s implement it in the appropriate
script, **react:jump-dob**.

    --- <B>react:jump-dob</B> in <B>Lib:NIP:lib:mounting</B> ---
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

    <M_COM>/* Fetch the reference to the riderlib, */</M_COM>
    <M_VARS>$mountrider</M_VARS> = this<M_CCS>.</M_CCS><M_TXT>"nip:trait:mounting:riderlib"</M_TXT>;

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

    <B><M_VARS>$actor</M_VARS>.<M_TXT>"base:gait"</M_TXT> = this<M_CCS>.</M_CCS><M_TXT>"nip:trait:mounting:rider-gait"</M_TXT>; <M_COM>/* and set our own */</M_COM></B>

    <M_COM>/* And finally, let's set a "npc:mounting" property in the actor (the rider, not the horse) to the horse object reference (this) */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT> = this<M_CCS>;</M_CCS>
    ---

One line changed there, as you can see. Instead of setting
\$actor.\"base:gait\" to \"riding\", we\'re setting it to whatever
this.\"nip:trait:mounting:rider-gait\" is. Which can be nil, in which
case the regular \"Joe leaves through/arrives from the exit\" message
will be displayed.

Now, it\'s always a good idea to inform the user of this feature so that
s/he knows it can be tweaked with. Another library property is available
for this specific purpose:

\* **done:message** - Display a string of text when this library is
loaded.

Let\'s be informative and put in a brief note to the user,

    ---
    > +setp "Lib:NIP:lib:mounting done:message The NPC is now mountable! 
    The property 'nip:trait:mounting:rider-gait' can be customized to 
    something like "elegantly rides" or "heavily galops"."
    Setting 'done:message' in &lt;Lib:NIP:lib:mounting>;
    - from: nil
    - to: "The NPC is now mountable! The property 
    'nip:trait:mounting:rider-gait' can be customized to something like 
    \"elegantly rides\" or \"heavily galops\"."

    > +setp horse "add mounting"
    Setting 'add' in &lt;Marrach:Coders:kalle:NPC:stallion>;
    - from: nil
    - to: "mounting"
    Attempting to add library ...
    <FONT COLOR=#FF0000>The NPC is now mountable! The property 
    'nip:trait:mounting:rider-gait' can be customized to something like 
    "elegantly rides" or "heavily galops".</FONT>
    &lt;Lib:NIP:lib:mounting> loaded successfully.
    ---

There we go!

Now we should really replace those jump/lower re-/actions to use
something more appropriate \-- mount, and dismount.

First off, we create the two verbs, mount and dismount. We call them
**Neoct:IC:Verbs:mount** and **Neoct:IC:Verbs:dismount** (add a direct
object role named \'dob\' to each) and we also add an action to each
which we call **Neoct:IC:Actions:mount** and
**Neoct:IC:Actions:dismount**.

Both action objects get a tiny one-line **global:action** script, in
which we simply do **EmitTo( \$actor, \"You can\'t do that.\" );**.

After this is finished, we go ahead and simply rename the two scripts.

\* **react:jump-dob** in **mounting** we rename to **react:mount-dob**
\* **act:lower** in **mountrider** we rename to **act:dismount**

But now we need to update the system to inherit
**act:dismount**act:lower\</B\>,

    --- <B>react:mount-dob</B> in <B>Lib:NIP:lib:mounting</B> ---
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

    <M_COM>/* Fetch the reference to the riderlib, */</M_COM>
    <M_VARS>$mountrider</M_VARS> = this<M_CCS>.</M_CCS><M_TXT>"nip:trait:mounting:riderlib"</M_TXT>;

    <M_COM>/* Then we inherit away! */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:approach"</M_TXT> = <M_VARS>$mountrider</M_VARS>;

    <B><M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:dismount"</M_TXT> = <M_VARS>$mountrider</M_VARS>;</B>
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:leave"</M_TXT> = <M_VARS>$mountrider</M_VARS>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:stance"</M_TXT> = <M_VARS>$mountrider</M_VARS>;
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act-post:enter"</M_TXT> = <M_VARS>$mountrider</M_VARS>;

    <M_COM>/* And we set the 'npc:mounted' property in the NPC to 1 to signal that we're mounted. */</M_COM>
    this<M_CCS>.</M_CCS><M_TXT>"npc:mounted"</M_TXT> = 1<M_CCS>;</M_CCS>

    <M_COM>/* Let's replace the base:gait in the actor for when we move through rooms. */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:oldgait"</M_TXT> = <M_VARS>$actor</M_VARS>.<M_TXT>"base:gait"</M_TXT>; <M_COM>/* store old value, just in case */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:gait"</M_TXT> = this<M_CCS>.</M_CCS><M_TXT>"nip:trait:mounting:rider-gait"</M_TXT>; <M_COM>/* and set our own */</M_COM>

    <M_COM>/* And finally, let's set a "npc:mounting" property in the actor (the rider, not the horse) to the horse object reference (this) */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT> = this<M_CCS>;</M_CCS>
    ---

After this update, we also have to go into **act:dismount** and make it
unload itself rather than the, now non-existant, **act:lower** script.

    --- <B>act:dismount</B> in <B>Lib:NIP:lib:mountrider</B> ---
    <M_COM>/* 
     
      D=Script for unmounting NPC's. 
     
    */</M_COM>

    <B>[*** We've removed the check here, as it's no longer of any use ***]</B> 
    <M_COM>/* Let's emit something cute right away. */</M_COM> 
     
    <M_VARS>$mount</M_VARS> = <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT>; 
     
    <M_COM>/* Let's restore the gait to the old value. */</M_COM> 
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:gait"</M_TXT> = <M_VARS>$actor</M_VARS>.<M_TXT>"base:oldgait"</M_TXT>; 
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:oldgait"</M_TXT> = nil<M_CCS>;</M_CCS>  
     
    <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"You unmount "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$mount</M_VARS> <M_CCS>)</M_CCS>+<M_TXT>"."</M_TXT> <M_CCS>)</M_CCS>; 
    <M_FUN>EmitIn</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS>.<M_TXT>"base:environment"</M_TXT><M_CCS>,</M_CCS> <M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS> <M_CCS>)</M_CCS>+<M_TXT>" unmounts "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$mount</M_VARS> <M_CCS>)</M_CCS>+<M_TXT>"."</M_TXT><M_CCS>,</M_CCS> <M_VARS>$actor</M_VARS> <M_CCS>)</M_CCS>; 
     
    <M_COM>/* Now, let's reverse the things done in the mounting script. */</M_COM> 
     
    <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT> = nil<M_CCS>;</M_CCS> 
    <M_VARS>$mount</M_VARS>.<M_TXT>"npc:mounted"</M_TXT> = 0<M_CCS>;</M_CCS> 
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:approach"</M_TXT> = nil<M_CCS>;</M_CCS> 
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:leave"</M_TXT> = nil<M_CCS>;</M_CCS> 
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:stance"</M_TXT> = nil<M_CCS>;</M_CCS> 
    <M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act-post:enter"</M_TXT> = nil<M_CCS>;</M_CCS> 
    <B><M_VARS>$actor</M_VARS>.<M_TXT>"merry:inherit:act:dismount"</M_TXT> = nil<M_CCS>;</M_CCS></B>
     
    <M_COM>/* And finally, set the actor's stance to "standing", 
        and preposition to "beside". */</M_COM> 
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:stance"</M_TXT> = <M_CON>STANCE_STAND</M_CON><M_CCS>;</M_CCS> 
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:preposition"</M_TXT> = <M_CON>PREP_BESIDE</M_CON><M_CCS>;</M_CCS>
    ---

The final thing we need to do is to change the \"init:merry\" property,
which currently reads **({ \"react:jump-dob\" })**:

    ---
    > +setp "Lib:NIP:lib:mounting init:merry ({ "react:mount-dob" })"
    ---

Now, we need to reload the library into the NPC again, or it won\'t
work.

    ---
    > +setp horse "add mounting"
    Setting 'add' in &lt;Marrach:Coders:kalle:NPC:stallion>;
    - from: nil
    - to: "mounting"
    Attempting to add library ...
    <FONT COLOR=#FF0000>The NPC is now mountable! The property 
    'nip:trait:mounting:rider-gait' can be customized to something like 
    "elegantly rides" or "heavily galops".</FONT>
    &lt;Lib:NIP:lib:mounting> loaded successfully.

    > mount horse
    You mount a horse.

    > dismount
    You dismount a horse.
    ---

Now, you may have noticed a bug if you did this all from scratch, which
occurs with the error messages. This is because sometimes, the NPC
doesn\'t have a \"trait:nominative\" property (it, he or she). Now,
we\'re going to put one into the init:properties so that unless the NPC
has one already, it\'s going to default to \"it\".

    ---
    > +setp "Lib:NIP:lib:mounting init:properties ([ "nip:trait:mounting:rider-gait":"rides", "trait:nominative" : "it" ])
    Setting 'init:properties' in &lt;Lib:NIP:lib:mounting>;
    - from: ([ "nip:trait:mounting:rider-gait":"rides" ])
    - to: ([ "nip:trait:mounting:rider-gait":"rides", "trait:nominative":"it" ])

    > +setp horse "add mounting"
    Setting 'add' in &lt;Marrach:Coders:kalle:NPC:stallion>;
    - from: nil
    - to: "mounting"
    Attempting to add library ...
    <FONT COLOR=#FF0000>The NPC is now mountable! The property 
    'nip:trait:mounting:rider-gait' can be customized to something like 
    "elegantly rides" or "heavily galops".</FONT>
    &lt;Lib:NIP:lib:mounting> loaded successfully.

    > +stat horse "property:trait:*"
    -- Properties (trait:*)--
    Property: trait:his = "his"
    <B>Property: trait:nominative = "it"</B>
    Property: trait:possessive = "his"
    ---

That should deal with that issue.

After a recent discussion, [further changes were
made](NIPRefLibraries1.14)!

\-- Main.KalleAlm - 05 Jun 2003
