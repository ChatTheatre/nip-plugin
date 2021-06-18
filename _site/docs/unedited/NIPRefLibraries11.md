%META:TOPICINFO{author=\"kallea\" date=\"1054842360\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPRefLibraries\"}%
[NIPRefStyle]{.twiki-macro .INCLUDE}

[NIPRefLibrariesTOC]{.twiki-macro .INCLUDE}

\<H2\>1.1: So, you have the idea\...\</H2\>

\... but you\'re unsure where to start. Let\'s go through an example
mentioned earlier. The horse mounting feature. We\'re going to implement
it together now, step by step. Let\'s play Q&A with ourselves to see
where we\'re going with this:

        <B>Q: What are the basic few points that this system will provide?</B>
        <I>A: A way to mount an NPC, some way to keep the rider and NPC in 
                sync'd proximation, some way to deal with moving through 
                rooms.</I>

        <B>Q: What other, external/internal, features are we going to need 
                to pull this off?</B>
        <I>A: Unless we decide it's a good thing to separate the whole prox
                sync/approach features from the 'mounting' lib, none. But 
                that is something we can honestly cut out at a later point if
                we realize it is useful in other cases than this.</I>

        <B>Q: Who's going to use this system?</B>
        <I>A: At least two different theatres have expressed interest in it
                so far. I'm sure others could find it useful as well.</I>

Alright, we\'ve figured a few things out there. We don\'t need any
external libs for this to work. It\'s a \"standalone\" thing. We have a
hum at what we need to make, but at this point it\'s time we go ahead
and specify exactly what we\'re going to do.

**\-\-- What Would It Look Like, How Would It Work \-\--**

I\'ve decided to, initially, make the \"mounting\" part a
react:jump-script in the NPC so that whenever someone types \"jump
horse\", the script will be triggered (instead of making an entirely new
\"mount\" verb \-- for now).

I\'ve also gone over the [Merry Signal System](SignalSystem) chart and
found the following interesting entries:

  ---------- ----- ----- ------ -------- ------ ------------------------------------ ------ -------------------------------
  signal     pre   sig   post   arg      type   description                          role   description
  approach   X     X     X      target   NRef   which detail to approach             \*     which detail to approach
  leave      X     X     X                                                                  
  stance     X     X     X      target   NRef   prox target of stance (e.g. altar)   \*     prox target of stance
  enter      X     X     X      what     NRef   detail we\'re trying to enter        \*     detail we\'re trying to enter
                                                                                     from   detail we emerge from
                                                                                     into   detail we enter into
  ---------- ----- ----- ------ -------- ------ ------------------------------------ ------ -------------------------------

I\'m going to add a hook to the act:approach, act:leave and act:stance
signals. Whenever someone is mounting the NPC, these scripts will be put
in the rider, so that I can control all movement in the room. Thus, if
the rider types \"approach George\", the horse he\'s on will approach
George, and the rider will remain seated on the horse. Similarly, if the
rider types \"go east\" (or \"e\"), the horse will be teleported with
him and s/he will be plopped on the horse again.

[Continue.](NIPRefLibraries1.2)

\-- Main.KalleAlm - 05 Jun 2003
