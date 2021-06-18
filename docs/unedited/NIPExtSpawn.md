%META:TOPICINFO{author=\"kallea\" date=\"1142281601\" format=\"1.0\"
version=\"1.1\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>Spawn System (external)\</font\>

The spawn system is used by nippers to re-spawn based on \"areas\". Each
area may have its own settings on matters such as \"how fast should a
nipper \'reincarnate\'\", \"how many nippers should there be\", and so
on.

The spawn area is a simple property container containing the various
specifics for the area it targets. An area is simply defined by the
physical and practical boundaries of the various available spawn points.
For instance, if a spawn area had the outer bailey courtyard as its
spawn point, then the nippers would basically be able to wander around
the entire outer bailey (but not the inner, unless they had precedence,
and not the gaol, period).

Each nipper master object tells the system which one spawn area it
belongs to. This is set in the property `nip:trait:spawn:area` in the
nipper itself. The nipper must also have the
[spawn-control](NIPLibRefSpawnControl) library loaded for this to take
effect.

\<font color=red\>*Note: whenever a nipper with spawn-control is slain,
it is \"enqueued\" in the respawning process. Thus, unless you set a cap
on the \# of nippers there may be, any new-spawned nippers will be
**added** to the circle of life, thus increasing the overall
population.*\</font\>

Setting a cap on an NPC is a matter of setting the integer property
`nip:trait:spawn:maxpop` in the master nipper itself. The area which
that particular nipper is associated with will only respawn an NPC of
that type if the number of available spawns is lower than the maxpop
value.

In the spawn area (the property container), the following properties are
supported:

  Property          Description                                                              Example / Recommended value
  ----------------- ------------------------------------------------------------------------ -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  nip:delay:min     The minimum time (in seconds) before the NPC is respawned                600
  nip:delay:max     The maximum time (in seconds) before the NPC is respawned                86400
  nip:disabled      1 or 0; if 1, the spawn area will NOT respawn any NPC\'s.                0
  nip:spawn-point   Mapping of rooms-to-emits where the spawn area may respawn, at random.   (\[ \<Kalle:rooms:area1:room1\>:\"From a corner, (npc) crawls into the light.\", \<Kalle:rooms:area1:room2\>:\"(npc) startles you, rushing out into sight from a tiny berry bush.\" \])

To avoid a spawn being entered into the circle of life, without using
the maxpop feature, you can set \"norespawn\" in the spawn before
slaying it. The spawn system will ignore any NPC that is slain with this
property set in its body.

\-- Main.KalleAlm - 13 Mar 2006
