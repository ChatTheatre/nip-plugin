%META:TOPICINFO{author=\"kallea\" date=\"1054842360\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPRefLibraries11\"}%
[NIPRefStyle]{.twiki-macro .INCLUDE}

[NIPRefLibrariesTOC]{.twiki-macro .INCLUDE}

\<H2\>1.2: Imagining up a few scenarios.\</H2\>

    <B>--- Mounting "in action", aka the way we want it to work when it's done ---</B>
    > look
    A test place.
    You're standing here. A heroic-looking horse is standing near here.

    > immediately jump heroic-looking horse
    <I>[my own react script in the horse kicks in here]</I>
    You mount the heroic-looking horse.

    > look
    A test place.

    A heroic-looking horse is standing near here. You are sitting on a 
    heroic-looking horse.

    Gunther arrives from the north exit.

    Gunther smiles.

    > walk to Gunther "Hi, Gunther!"
    <I>[my own act:approach script is triggered here]</I>
    A heroic-looking horse approaches Gunther.

    A heroic-looking horse walks to Gunther, "Hi, Gunther!"
    <B>OOPS!</B>
    ---

Okay, in my little imagined scene above, we immediately realize one
concrete thing about the stance script \-- **the emote (in the stance)
must be by the rider, not by the horse**. Perhaps this would work, as
something of a hack:

Approaches are hooked, but the approach is done internally (using
\$what).

That issue settled, let\'s go back to our scene and see what happens:

    ---
    Gunther arrives from the north exit.

    Gunther smiles.

    > walk to Gunther "Hi, Gunther!"
    <I>[the act:approach script kicks in, forces the horse to approach as 
     well, and makes the rider's approach internal and silent. A very 
     short delay (100 ms) ...]</I>
    A heroic-looking horse approaches Gunther.
    <I>[... and drop the rider on the horse again. The act:stance check 
     (to see if he's got in prox) has already been executed at this point 
     (so we won't have any spammy, endless failed attempts to 
     approach]</I>
    You walk to Gunther, "Hi, Gunther!"
    ---

That looks sorta good so far. The last part (walking to Gunther although
mounting a horse) is something we\'ll have to deal with eventually, but
for now it\'ll do as is.

    ---
    > look
    A test place.
    Gunther is standing near the north exit. A heroic-looking horse is 
    standing near Gunther. You are sitting on a heroic-looking horse.
    ---

That also works.

    ---
    > stand beside gunther 
    [act:approach; horse is already near Gunther, so nothing really 
     happens here]
    You stand beside Gunther.

    > look
    A test place.
    Gunther is standing near the north exit. A heroic-looking horse is 
    standing near Gunther. You are sitting on a heroic-looking horse.
    ---

Okay. Any way we can implement a solution to make the horsie reflect not
only proximity but also preposition (stance would be a little odd and
could be abused way too much, \"A heroic-looking horse is kneeling
before Gunther.\")?

Course there is! act:stance, mentioned earlier, is called whenever the
actor tries to change his stance. Let\'s be repetitive and look at that
table again,

  -------- ----- ----- ------ -------- ------ ------------------------------------ ------ -----------------------
  signal   pre   sig   post   arg      type   description                          role   description
  stance   X     X     X      target   NRef   prox target of stance (e.g. altar)   \*     prox target of stance
  -------- ----- ----- ------ -------- ------ ------------------------------------ ------ -----------------------

We have \$target right off. There are also two others (undocumented)
arguments that are interesting. So we quickly test this in the client of
the game,

    ---
    > +setp me "merry:act:stance X[M] EmitTo( $actor, dump_value( args ));
    > stand on floor
    ([ "actor":<Marrach:players:K:kalle>, "current-action":"stance", 
        <B>"prep":8, "stance":5, "target":(43)O(/base/data/nref#-1, 
        <Marrach:Coders:kalle:rooms:home>, "floor")</B>, 
        "targets":(43)O(/base/data/nref#-1, 
        &lt;Marrach:Coders:kalle:rooms:home>, "floor"), 
        "this":&lt;Marrach:players:K:kalle>, "witnesses":({ 
        &lt;Marrach:Coders:kalle:rooms:home>, ({ }) }) ])
    ---

Lovely, we have \$prep which is the preposition. We have \$stance (which
we won\'t use) which is the stance, and we have \$target which is the
proximity target. For entertainment value, there is a set of constants
readily available in Merry for these values,

\* PREP\_\<PREPOSITION\>

E.g. PREP_ON is 8, PREP_UNDER is 4, etc. A heck, here\'s a complete
list:

  --------------- --------------------- -------------------
  **constant**    **preposition**       **integer value**
  PREP_AGAINST    against               2
  PREP_BEFORE     before, in front of   2048
  PREP_BEHIND     behind                1024
  PREP_BESIDE     beside                4096
  PREP_CLOSE_TO   close to              1
  PREP_INSIDE     inside                16
  PREP_NEAR       near                  256
  PREP_ON         on                    8
  PREP_OVER       over                  512
  PREP_UNDER      under                 4
  --------------- --------------------- -------------------

Though, we won\'t need those. :)

What we need to do, though is to based on these three values, **prep**,
**stance** and **target** found in the rider\'s act:stance, and force
the mount (i.e. the horse, in this case) to perform them instead of the
actor. That\'s easy, though. Let\'s see what would/should happen then:

[Continue.](NIPRefLibraries1.3)

\-- Main.KalleAlm - 05 Jun 2003
