%META:TOPICINFO{author=\"kallea\" date=\"1054842018\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>HOW TO make them sleep?\</FONT\>

**How:**

\> +setp NPC \"add sleeping\"

Done!

**Tweaking functionality:**

There are a few values you can flip around to change how your NPC
behaves sleeping-wise:

  ----------------------------- -------------------------------------------------------------------------- ----------------------------------
  **Property:**                 **Description:**                                                           **Default value:**
  nip:trait:sleeping:effect     How fast does it recover while sleeping?                                   2
  nip:trait:sleeping:interval   Approximately, how many seconds before we\'re tired.                       57600
  nip:trait:sleeping:states     The states in which the NPC might reside. Don\'t change unless you must.   (\[ \"awake\":1, \"sleep\":1 \])
  ----------------------------- -------------------------------------------------------------------------- ----------------------------------

**Further comment(s):**

The sleeping effect value determines how much one second is worth while
sleeping, compared to one whilst awake. Effect 1 would be 100%, e.g. NPC
is awake for 12 hours, gets tired, sleeps for 12, gets up, etc. Effect 2
would be 200%. NPC is awake for 12 hours, sleeps for 6, awake 12, sleep
6, etc. Effect 3 = awake 12, sleep 4. And so on.

A number of scripts rely on this script\'s states, being \"awake\" or
\"sleep\", but it\'s not a dead set thing and can be changed if scripts
that were necessary were given a new name and modified accordingly.

\-- Main.KalleAlm - 01 Jun 2003
