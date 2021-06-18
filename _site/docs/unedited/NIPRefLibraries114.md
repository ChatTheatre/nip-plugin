%META:TOPICINFO{author=\"kallea\" date=\"1055165389\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPRefLibraries113\"}%
[NIPRefStyle]{.twiki-macro .INCLUDE}

[MerryColorStyles]{.twiki-macro .INCLUDE}

[NIPRefLibrariesTOC]{.twiki-macro .INCLUDE}

\<H2\>1.14: Modifications to the code.\</H2\>

In a discussion with one of the team members of Devils Cay, thoughts on
a solution where the mounting library would be integrated into a
somewhat different other type of system were put forth.

Initially, I said \"Of course it works,\" but then I realized the code
was a bit too static for the time being, for that. So I updated it.

As you may recall, in the mount/dismount-scripts, a couple of inherits
were made. These were clumsily written, and it was always in my mind to
replace these in the \"Tweaking the code\"-part, but I never got around
to do it.

The system integration mentioned above required another script to be
inherited in the rider, though.

To make this possible, I added another property to the nip:trait\'s,
namely **\"nip:trait:mounting:rider-inherits\"**.

This property should by default look like this: **(\[
\"act-post:enter\":\"nip:trait:mounting:riderlib\",
\"act:approach\":\"nip:trait:mounting:riderlib\",
\"act:dismount\":\"nip:trait:mounting:riderlib\",
\"act:leave\":\"nip:trait:mounting:riderlib\",
\"act:stance\":\"nip:trait:mounting:riderlib\" \])**

Why not just an array, though? Because if we added a simple array, the
system wouldn\'t know where to grab it!

So, as the **init:properties**-property in the mounting-lib already
exists, and looks like this: **(\[
\"nip:trait:mounting:rider-gait\":\"rides\", \"trait:nominative\":\"it\"
\])**

\- we\'re going to just add the aforementioned to it.

    ---
    > +setp "Lib:NIP:lib:mounting init:properties ([ "nip:trait:mounting:rider-gait":"rides", "trait:nominative":"it", "nip:trait:mounting:rider-inherits":([ "act-post:enter":"nip:trait:mounting:riderlib", "act:approach":"nip:trait:mounting:riderlib", "act:dismount":"nip:trait:mounting:riderlib", "act:leave":"nip:trait:mounting:riderlib", "act:stance":"nip:trait:mounting:riderlib" ]) ])
    ---

As you probably know already, this means any NPC that loads the mounting
library, will get the aforementioned properties set, unless the
properties already exist in the NPC body.

Let\'s see what we need to do with the react:mount-dob-script in the
mounting library though:

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

    <B><M_COM>/* We inherit, as specified in the inherits mapping */</M_COM>
    <M_VARS>$inherits</M_VARS> = this<M_CCS>.</M_CCS><M_TXT>"nip:trait:mounting:rider-inherits"</M_TXT>;
    <M_VARS>$scripts</M_VARS> = <M_FUN>map_indices</M_FUN><M_CCS>(</M_CCS> <M_VARS>$inherits</M_VARS> <M_CCS>)</M_CCS>;
    <M_RVD>for</M_RVD><M_CCS>(</M_CCS> <M_VARS>$i</M_VARS> = 0<M_CCS>;</M_CCS> <M_VARS>$i</M_VARS> < <M_FUN>sizeof</M_FUN><M_CCS>(</M_CCS> <M_VARS>$scripts</M_VARS> <M_CCS>)</M_CCS>; <M_VARS>$i</M_VARS>++ <M_CCS>)</M_CCS>
      <M_FUN>Set</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"merry:inherit:"</M_TXT>+<M_VARS>$scripts</M_VARS>[$i], <M_FUN>Get</M_FUN><M_CCS>(</M_CCS> this<M_CCS>,</M_CCS> <M_VARS>$inherits</M_VARS>[$scripts[$i]] <M_CCS>)</M_CCS>)<M_CCS>;</M_CCS></B>

    <M_COM>/* And we set the 'npc:mounted' property in the NPC to 1 to signal that we're mounted. */</M_COM>
    this<M_CCS>.</M_CCS><M_TXT>"npc:mounted"</M_TXT> = 1<M_CCS>;</M_CCS>

    <M_COM>/* Let's replace the base:gait in the actor for when we move through rooms. */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:oldgait"</M_TXT> = <M_VARS>$actor</M_VARS>.<M_TXT>"base:gait"</M_TXT>; <M_COM>/* store old value, just in case */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:gait"</M_TXT> = this<M_CCS>.</M_CCS><M_TXT>"nip:trait:mounting:rider-gait"</M_TXT>; <M_COM>/* and set our own */</M_COM>

    <M_COM>/* And finally, let's set a "npc:mounting" property in the actor (the rider, not the horse) to the horse object reference (this) */</M_COM>
    <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT> = this<M_CCS>;</M_CCS>
    ---

What does that modification do, anyway?

Firstly, let\'s look at the properties in our NPC: (if you haven\'t
reloaded the mounting lib yet, you need to do so)

    ---
    > +stat horse "property:nip:*"
    -- Properties (nip:*)--
    Property: nip:trait:mounting:rider-gait = "rides"
    Property: nip:trait:mounting:rider-inherits = ([ 
    "act-post:enter":"nip:trait:mounting:riderlib", 
    "act:approach":"nip:trait:mounting:riderlib", 
    "act:dismount":"nip:trait:mounting:riderlib", 
    "act:leave":"nip:trait:mounting:riderlib", 
    "act:stance":"nip:trait:mounting:riderlib" ])
    Property: nip:trait:mounting:riderlib = &lt;Lib:NIP:lib:mountrider>
    ---

Specifically, the last property is interesting,
**\"nip:trait:mounting:riderlib\"**. It points to
\<Lib:NIP:lib:mountrider\>. So in our code, what we do here:
\<PRE\>\$inherits =
this.\"nip:trait:mounting:rider-inherits\";\</PRE\>is to grab the
inherits mapping as is, and here: \<PRE\>\$scripts = map_indices(
\$inherits );\</PRE\>we extract the indices (keys) as an array; which we
then use here: \<PRE\>for( \$i = 0; \$i \< sizeof( \$scripts ); \$i++
)\</PRE\> to step through each individual indice. Now comes the tricky
part,

    Set( $actor, <B>"merry:inherit:"+$scripts[$i]</B>,

which in the first indice would be \"merry:inherit:act-post:enter\";

    Set( $actor, "merry:inherit:"+$scripts[$i], <B>Get( this, $inherits[$scripts[$i]] ));</B>

and we **set it** to the value, of the value, of the mapping with the
indice in question, which in the first case means we set it to the
horse\'s \"nip:trait:mounting:riderlib\"\'s value, which is
\<Lib:NIP:lib:mountrider\>.

Let me repeat that one: We set the property \[\<FONT
COLOR=\#FF0000\>merry:inherit:\<indice\>\</FONT\>\] to the value of the
value \[\<FONT
COLOR=\#FF0000\>\"nip:trait:mounting:riderlib\"\</FONT\>\] in the NPC,
which is \<FONT COLOR=\#FF0000\>\<Lib:NIP:lib:mountrider\>\</FONT\>.

Alright. Now that we\'ve (hopefully) covered that part, we need to go in
and tweak the act:dismount-script in the mountrider-lib.

    --- <B>act:dismount</B> in <B>Lib:NIP:lib:mountrider</B> ---
    <M_COM>/*  
      
      D=Script for dismounting NPC's.  
      
    */</M_COM>  
      
    <M_COM>/* Let's emit something cute right away. */</M_COM>  
      
    <M_VARS>$mount</M_VARS> = <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT>;  
      
    <M_COM>/* Let's restore the gait to the old value. */</M_COM>  
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:gait"</M_TXT> = <M_VARS>$actor</M_VARS>.<M_TXT>"base:oldgait"</M_TXT>;  
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:oldgait"</M_TXT> = nil<M_CCS>;</M_CCS> 
      
    <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"You dismount "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$mount</M_VARS> <M_CCS>)</M_CCS>+<M_TXT>"."</M_TXT> <M_CCS>)</M_CCS>;  
    <M_FUN>EmitIn</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS>.<M_TXT>"base:environment"</M_TXT><M_CCS>,</M_CCS> <M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS> <M_CCS>)</M_CCS>+<M_TXT>" unmounts "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$mount</M_VARS> <M_CCS>)</M_CCS>+<M_TXT>"."</M_TXT><M_CCS>,</M_CCS> <M_VARS>$actor</M_VARS> <M_CCS>)</M_CCS>;  
      
    <M_COM>/* Now, let's reverse the things done in the mounting script. */</M_COM>  
      
    <M_VARS>$actor</M_VARS>.<M_TXT>"npc:mounting"</M_TXT> = nil<M_CCS>;</M_CCS>  
    <M_VARS>$mount</M_VARS>.<M_TXT>"npc:mounted"</M_TXT> = 0<M_CCS>;</M_CCS>  

    <B><M_VARS>$inherits</M_VARS> = <M_FUN>map_indices</M_FUN><M_CCS>(</M_CCS> <M_VARS>$mount</M_VARS>.<M_TXT>"nip:trait:mounting:rider-inherits"</M_TXT> <M_CCS>)</M_CCS>;
    <M_RVD>for</M_RVD><M_CCS>(</M_CCS> <M_VARS>$i</M_VARS> = 0<M_CCS>;</M_CCS> <M_VARS>$i</M_VARS> < <M_FUN>sizeof</M_FUN><M_CCS>(</M_CCS> <M_VARS>$inherits</M_VARS> <M_CCS>)</M_CCS>; <M_VARS>$i</M_VARS>++ <M_CCS>)</M_CCS>
      <M_FUN>Set</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"merry:inherit:"</M_TXT>+<M_VARS>$inherits</M_VARS>[$i], nil <M_CCS>)</M_CCS>;</B>
      
    <M_COM>/* And finally, set the actor's stance to "standing",  
        and preposition to "beside". */</M_COM>  
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:stance"</M_TXT> = <M_CON>STANCE_STAND</M_CON><M_CCS>;</M_CCS>  
    <M_VARS>$actor</M_VARS>.<M_TXT>"base:preposition"</M_TXT> = <M_CON>PREP_BESIDE</M_CON><M_CCS>;</M_CCS>
    ---

Okay, that one\'s not as difficult as the previous.

We fetch the mapping\'s indices straight away, \<PRE\>\$inherits =
map_indices( \$mount.\"nip:trait:mounting:rider-inherits\" );\</PRE\>-
and we step through each and every one of the entries and set the
inherit to nil,\<PRE\>for( \$i = 0; \$i \< sizeof( \$inherits ); \$i++ )
Set( \$actor, \"merry:inherit:\"+\$inherits\[\$i\], nil );\</PRE\>

That\'s it. It is now possible to add/remove rider-inherits from the
customized NPC without having to grok code. We will possibly get back
with more chapters on more expansions and customizations in time for
this one. Keep on the lookout. :)

\-- Main.KalleAlm - 08 Jun 2003
