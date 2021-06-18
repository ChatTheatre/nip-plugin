%META:TOPICINFO{author=\"kallea\" date=\"1202983341\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPRefLibraries15\"}%
[NIPRefStyle]{.twiki-macro .INCLUDE}

[MerryColorStyles]{.twiki-macro .INCLUDE}

[NIPRefLibrariesTOC]{.twiki-macro .INCLUDE}

\<H2\>1.6: Time to start writing code.\</H2\>

Let\'s go in and create the script we gave a brief spec above,
react:jump-dob in the \'mounting\' lib,

    <B>--- Marrach:Lib:NIP:lib:mounting/react:jump-dob ---</B>
    <M_COM>/*

        D=This script deals with mounting an NPC.

    */</M_COM>

    <M_RVD>if</M_RVD><M_CCS>(</M_CCS> this<M_CCS>.</M_CCS><M_TXT>"npc:mounted"</M_TXT> <M_CCS>)</M_CCS> <M_CCS>{</M_CCS> <M_COM>/* Someone is mounting the NPC already... */</M_COM>
      <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"You can't mount "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS>this<M_CCS>)</M_CCS>+<M_TXT>" as "</M_TXT>+this<M_CCS>.</M_CCS><M_TXT>"trait:nominative"</M_TXT>+<M_TXT>" is already being mounted."</M_TXT> <M_CCS>)</M_CCS>;
      <M_FUN>return</M_FUN> FALSE<M_CCS>;</M_CCS>
    <M_CCS>}</M_CCS>

    <M_COM>/* If we get here, the NPC isn't mounted. Let's print some pretty message describing what happens, */</M_COM>

    <M_FUN>EmitIn</M_FUN><M_CCS>(</M_CCS> this<M_CCS>.</M_CCS><M_TXT>"base:environment"</M_TXT><M_CCS>,</M_CCS> <M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS> <M_CCS>)</M_CCS>+<M_TXT>" mounts "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> this <M_CCS>)</M_CCS>+<M_TXT>"."</M_TXT><M_CCS>,</M_CCS> <M_VARS>$actor</M_VARS> <M_CCS>)</M_CCS>;
    <M_FUN>EmitTo</M_FUN><M_CCS>(</M_CCS> <M_VARS>$actor</M_VARS><M_CCS>,</M_CCS> <M_TXT>"You mount "</M_TXT>+<M_FUN>Describe</M_FUN><M_CCS>(</M_CCS> this <M_CCS>)</M_CCS>+<M_TXT>"."</M_TXT> <M_CCS>)</M_CCS>;

    <M_COM>/* And finally, let's set a "npc:mounting" property in the actor (the rider, not the horse) to the horse object reference (this) */</M_COM>
    <M_VARS>$actor</M_VARS><M_CCS>.</M_CCS><M_TXT>"npc:mounting"</M_TXT> = this<M_CCS>;</M_CCS>
    ---

Okay, goody. Before we can try this, however, we need to set the
property **init:merry** in **Marrach:Lib:NIP:lib:mounting**. This
property controls which scripts should be inherited when the library is
loaded. We can do this from the parser (using setp) or through woe. I do
it from woe, it\'s faster, but unless you know what you\'re doing, you
may break something that way.

    ---
    > +setp "Marrach:Lib:NIP:lib:mounting init:merry ({ "react:jump-dob" })"
    Setting 'init:merry' in &lt;Marrach:Lib:NIP:lib:mounting>;
    - from: nil
    - to: ({ "react:jump-dob" })
    ---
    >

Now that we\'re all set, we need to load the library in the horse again,

    ---
    > +setp horse "add mounting"
    Setting 'add' in &lt;Marrach:Coders:kalle:NPC:stallion>;
    - from: nil
    - to: "mounting"
    Attempting to add library ...
    &lt;Marrach:Lib:NIP:lib:mounting> loaded successfully.

    > +stat horse "property:merry:inherit:react:*
    -- Properties (merry:inherit:react:*)--
    Property: merry:inherit:react:jump-dob = &lt;Marrach:Lib:NIP:lib:mounting>
    ---

Splendid! Let\'s try it out.

    ---
    > jump horse
    You mount a horse.

    > +stat me "property:npc:*
    -- Properties (npc:*)--
    Property: npc:mounting = &lt;Marrach:Coders:kalle:NPC:stallion>
    ---

Nice! As you see, we got that \'npc:mounting\' property as the script
said we should. Before we continue working on that script, though,
we\'re going to need to put some of those **mountrider** act-scripts
into reality.

[Creating the act:approach script](NIPRefLibraries1.7)

\-- Main.KalleAlm - 05 Jun 2003
