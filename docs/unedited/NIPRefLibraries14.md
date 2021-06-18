%META:TOPICINFO{author=\"kallea\" date=\"1054920404\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPRefLibraries13\"}%
[NIPRefStyle]{.twiki-macro .INCLUDE}

[NIPRefLibrariesTOC]{.twiki-macro .INCLUDE}

\<H2\>1.4: Brief summary of the scripts we will eventually make.\</H2\>

Now that that\'s done, it\'s actually time to start doing something with
all of this. I\'m going to write a few specs for the individual scripts
and the individual libraries (there are, as you may have seen in the
todo, going to be two separate libs):

\-\-- **act:approach** in lib **mountrider** \-\--

This script will deal with the aspect of when the rider tries to move
around **inside a room**, e.g. approaching someone or walking to
someone, etc. This script will,

\* Force the NPC to perform the approach instead of the actor, \* Give
off a mini-delay (100 ms) in case the actor tried to perform a stance.
\* Abort the actor\'s approach.

\-\-- **act:leave** in lib **mountrider** \-\--

This script will deal with \'leaving\' as act:approach above deals with
\'approaching\'.

\* Force the NPC to perform the \'leave\' instead of the actor, \* Abort
the actor\'s leave (no risk for stances so we can skip the delay).

\-\-- **act:stance** in lib **mountrider** \-\--

This script will deal with the aspect of taking a new preposition in
relation to the environment, e.g. \"standing beside gunther\" or
\"standing in front of the gate\". This script will,

\* Extract the preposition and target from the arguments sent to
act:stance, \* Send these arguments to the NPC and force it to perform
its own act:stance based upon them, \* Abort the actor\'s stance-change.

\-\-- **act:lower** in lib **mountrider** \-\--

This script will dismount someone who types \"lower\" and is currently
mounting an NPC.

\-\-- **react:jump-dob** in lib **mounting** \-\--

This script will make a person mount the NPC in question and will set
the appropriate inherits.

\* Check if anyone\'s already on the NPC. Currently, we\'re not going to
address the issue of several people mounting the same NPC, but that is
something we\'ll get at later. Not now. \* If someone is mounting the
NPC, emit an error and abort the action. \* Otherwise, put the actor on
the NPC and set the merry inherits in the actor to the act:-scripts
mentioned above, in the **mountrider** lib. \* Also make sure the NPC
sets the \"mounted\" value to 1 (one mounting) to make the check at the
top work right.

------------------------------------------------------------------------

Time to go ahead and do this, then:

I start off by making a silly horse, as that\'s the most appropriate
example I can think of. After making the horse in woe, I summon it and
add in the basic NPC stuff,

    ---
    > +summon Marrach:Coders:kalle:NPC:stallion
    A horse arrives.

    > +nip 'set Marrach:Coders:kalle:NPC:stallion'
    WELCOME TO THE 'NIP' CNPC SYSTEM!

    Hold one moment while the core library is set up in &lt;Marrach:Coders:kalle:NPC:stallion> ...
    --> Implementing base.
    --> Adding base libraries.
    --> Inserting system signals.
    Done!
    ---

Okay, the horse is using the NPC system now.

[Time to create one of the libraries.](NIPRefLibraries1.5)

\-- Main.KalleAlm - 05 Jun 2003
