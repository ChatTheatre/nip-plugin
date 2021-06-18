%META:TOPICINFO{author=\"kallea\" date=\"1054920225\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPRefLibraries12\"}%
[NIPRefStyle]{.twiki-macro .INCLUDE}

[NIPRefLibrariesTOC]{.twiki-macro .INCLUDE}

\<H2\>1.3: Fine-tuning the aforementioned imagined scenarios.\</H2\>

    ---
    > stand beside gunther 
    [act:approach; horse is already near Gunther, so nothing really 
     happens here]
    [act:stance; (in rider), blow the action off and instead tell the horse to perform the stance action]
    A heroic-looking horse stands beside Gunther.

    > look
    A test place.
    Gunther is standing near the north exit. A heroic-looking horse is 
    standing beside Gunther. You are sitting on a heroic-looking horse.
    ---

Okay, that\'s settled. How about the traveling through environments (aka
leaving a room) part?

    --- unmodified, this is what I presume will happen as things are now ---
    > look
    A test place.
    Gunther is standing near the north exit. A heroic-looking horse is 
    standing beside Gunther. You are sitting on a heroic-looking horse.

    > go north
    [my approach script]
    A heroic-looking horse approaches the north exit.
    You leave through the north exit.

    Another place which exists only in Kalle's mind.
    You are standing near the south exit.
    ---

Ah. Kay. So the horse is still standing south of here with Gunther.
That\'s no good.

So, we tweak act:stance in the rider. We add in,

\* A quick delay (100 ms) \* And then we teleport the NPC to the rider,
stand the NPC where the rider\'s standing, and drop the rider on the NPC
again.

Fair enough,

    ---
    > look
    A test place.
    Gunther is standing near the north exit. A heroic-looking horse is 
    standing beside Gunther. You are sitting on a heroic-looking horse.

    > go north
    [my approach script]
    A heroic-looking horse approaches the north exit.
    [my act:stance script, delay (100 ms)...]
    You leave through the north exit.
    [... delay done, teleport the horse to the rider, put the horse where the rider is standing, put the rider on the horse again]
    Another place which exists only in Kalle's mind.
    A heroic-looking horse is standing near the south exit. You are sitting on a heroic-looking horse.
    ---

Now before we start making any code, let\'s look at one more thing:

    ---
    > look
    A test place.
    Gunther is standing near the north exit. A heroic-looking horse is 
    standing beside Gunther. You are sitting on a heroic-looking horse.

    > leave
    You move away from a heroic-looking horse.

    > look
    A test place.
    Gunther is standing near the north exit. A heroic-looking horse is 
    standing beside Gunther. You are standing near here.
    ---

Ah. Hm. Now we have two ways of dealing with this\...

\* We can either decide that \'leave\' means dismounting. But I don\'t
like that idea, because it should be possible to \"control\" the mount
without having to skip off it all the time. \* Or, we simply do as we
did with approach. The horse performs a \"leave\" and the rider is put
back on the horse immediately.

I\'m going for \#2 \-- the approach clone.

    ---
    > look
    A test place.
    Gunther is standing near the north exit. A heroic-looking horse is 
    standing beside Gunther. You are sitting on a heroic-looking horse.

    > leave
    A heroic-looking horse moves away from Gunther.

    > look
    A test place.
    Gunther is standing near the north exit. A heroic-looking horse is 
    standing near here. You are sitting on a heroic-looking horse.
    ---

Okay, I deem this idea ready to be created, so I go ahead and write up
the [NIPTodoMounting](NIPTodoMounting) TWiki-page, for good measure. :)

[Continue.](NIPRefLibraries1.4)

\-- Main.KalleAlm - 05 Jun 2003
