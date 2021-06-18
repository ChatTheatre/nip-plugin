%META:TOPICINFO{author=\"kallea\" date=\"1054834140\" format=\"1.0\"
version=\"1.1\"}% %META:TOPICPARENT{name=\"NIPRefLibraries14\"}%
[NIPRefStyle]{.twiki-macro .INCLUDE}

[NIPRefLibrariesTOC]{.twiki-macro .INCLUDE}

\<H2\>1.5: Time to create one of the libraries.\</H2\>

Let\'s create one of the libraries, by

\* Cloning **Core:PropertyContainer** in woe. \* Renaming it to
**Marrach:Lib:NIP:lib:mountrider**.

Now, you ask, how on earth did I know what to call it? There are a few
rules in the NPC system, as defined in
\<<Data:NIP:system>\>.**lib_path**. Specifically, this is the route the
system will take to find an object I am requesting, and this is also
dependant on what theatre I belong to.

Thus, when I want to do something to a library through the NPC system,
the system will look for that library in the following order:

    ---
        Lib:NIP:base:lib:<B>&lt;library></B>
        Lib:NIP:base:hooks:<B>&lt;library></B>
        Lib:NIP:base:signals:<B>&lt;library></B>
        (game):Lib:NIP:lib:<B>&lt;library></B>
        (game):Lib:NIP:hooks:<B>&lt;library></B>
        (game):Lib:NIP:signals:<B>&lt;library></B>
        (game):Lib:NIP:<B>&lt;library></B>
        (game):NIP:lib:<B>&lt;library></B>
        (game):NIP:hooks:<B>&lt;library></B>
        (game):NIP:signals:<B>&lt;library></B>
        (game):NIP:<B>&lt;library></B>
        Lib:NIP:lib:<B>&lt;library></B>
        Lib:NIP:hooks:<B>&lt;library></B>
        Lib:NIP:signals:<B>&lt;library></B>
        Lib:NIP:<B>&lt;library></B>
    ---

Thus, if you belong to the Devil\'s Cay theatre,

    ---
    > +stat me "property:theatre:id"
    -- Properties (theatre:id)--
    Property: theatre:id = "DevilsCay"
    >
    ---

\- the system scan would be:

    ---
        Lib:NIP:base:lib:<B>&lt;library></B>
        Lib:NIP:base:hooks:<B>&lt;library></B>
        Lib:NIP:base:signals:<B>&lt;library></B>
        DevilsCay:Lib:NIP:lib:<B>&lt;library></B>
        DevilsCay:Lib:NIP:hooks:<B>&lt;library></B>
        DevilsCay:Lib:NIP:signals:<B>&lt;library></B>
        DevilsCay:Lib:NIP:<B>&lt;library></B>
        DevilsCay:NIP:lib:<B>&lt;library></B>
        DevilsCay:NIP:hooks:<B>&lt;library></B>
        DevilsCay:NIP:signals:<B>&lt;library></B>
        DevilsCay:NIP:<B>&lt;library></B>
        Lib:NIP:lib:<B>&lt;library></B>
        Lib:NIP:hooks:<B>&lt;library></B>
        Lib:NIP:signals:<B>&lt;library></B>
        Lib:NIP:<B>&lt;library></B>
    ---

Now that we have our library in place, let\'s create the other right
away (\'mounting\').

\* Clone **Core:PropertyContainer** in woe. \* Rename it to
**Marrach:Lib:NIP:lib:mounting**.

(Of course, in your case, that would be
**Whatever-theatre-you\'re-on**:Lib:NIP:\...)

Now, the **mounting** library will actually be loaded into the NPC. The
**mountrider** won\'t. It will contain the scripts that the rider will
inherit when he mounts the NPC. But let\'s try to add the \'mounting\'
lib to the NPC now (and introduce one of the other +nip-functions while
we\'re at it! :).

    ---
    > +setp horse "add mounting"
    Setting 'add' in &lt;Marrach:Coders:kalle:NPC:stallion>;
    - from: nil
    - to: "mounting"
    Attempting to add library ...
    &lt;Marrach:Lib:NIP:lib:mounting> loaded successfully.

    > +nip horse "list"
    NIP in &lt;Marrach:Coders:kalle:NPC:stallion>:
    ---------------------------------------------------------------
    Libraries:
    - &lt;Lib:NIP:base:lib:signals>
    - &lt;Lib:NIP:base:lib:hooks>
    - &lt;Lib:NIP:base:lib:stream>
    - &lt;Lib:NIP:core>
    - &lt;Lib:NIP:base:signals:DELAY>
    - &lt;Lib:NIP:base:signals:DECIDE>
    - &lt;Lib:NIP:base:signals:INTERNAL>
    <B>- &lt;Marrach:Lib:NIP:lib:mounting></B>

    Signals:
    - "DELAY" [PRIORITY 10]
    - "INTERNAL" [PRIORITY 500]
    - "DECIDE" [PRIORITY 1000]

    Hooks:
    - decide: &lt;Lib:NIP:base:hooks:decide>
    - delay: &lt;Lib:NIP:base:hooks:delay>
    - internal: &lt;Lib:NIP:base:hooks:internal>

    End.
    ---

As you see at the bold line above, the library was loaded fine. Nothing
happened though, and it\'s only there \"in the papers\". It makes no
difference whatsoever. Not yet.

[Time to start writing code.](NIPRefLibraries1.6)

\-- Main.KalleAlm - 05 Jun 2003
