%META:TOPICINFO{author=\"kallea\" date=\"1055168752\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>HOW TO make an NPC move through rooms
randomly?\</FONT\>

**How:**

    > +setp NPC "add movement"

**Tweaking functionality:**

There are a few values you can tweak to change how often your NPC moves
around:

  ------------------------------ -------------------------------------------------------------------------------------------------- --------------------
  **Property:**                  **Description:**                                                                                   **Default value:**
  nip:trait:movement:frequency   Movement frequency. 0 = don\'t ever move; the higher the value the more seldom the NPC will move   10
  ------------------------------ -------------------------------------------------------------------------------------------------- --------------------

**Further comment(s):**

A [more advanced movement library](NIPTodoAdvancedMovement) is to be
developed further on. This library will simply scan for exits, pick one
at random, and attempt to walk through it. I will add in code for
opening doors that are closed and unlocking doors the NPC has access too
eventually (to this lib).

\-- Main.KalleAlm - 08 Jun 2003
