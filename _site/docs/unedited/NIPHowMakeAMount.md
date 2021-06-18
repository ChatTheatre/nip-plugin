%META:TOPICINFO{author=\"kallea\" date=\"1054842792\" format=\"1.0\"
version=\"1.1\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>HOW TO make a mount (e.g. a horse)?\</FONT\>

**How:**

    ---
    > +setp NPC "add mounting"
    ---

**Tweaking functionality:**

There are a few values you can flip around to change how your NPC
behaves:

  ------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------- --------------------
  **Property:**                   **Description:**                                                                                                                            **Default value:**
  nip:trait:mounting:rider-gait   Whenever someone mounts the NPC, the rider\'s gait will change so that when the rider moves through rooms, it seems as if s/he is riding.   \"riding\"
  ------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------- --------------------

**Further comment(s):**

The creation of this library was documented as a technical reference on
how to make libraries, [found here](NIPRefLibraries).

\-- Main.KalleAlm - 05 Jun 2003
