%META:TOPICINFO{author=\"kallea\" date=\"1116292500\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<h1\>NIP Merry API\</h1\>

[]{.twiki-macro .TOC}

## Introduction

The NIP Merry API is the link between user Merry code and the NIP
system.

The API is there to make communication and manipulation of NPC behaviors
and features as simple as it can for the general, non-NPC coder.

The API is somewhat infantile and not many features exist at this point.
More will come, especially if you request it.

The API can be accessed through Merry by calling the script namespace
NPC::.

For example, if you wish to trigger the resource control (which would
start up any NPC\'s in the room that were disabled due to PC inactivity)
in the room \$here, you would simply do this:\<pre\>
NPC::trigger_rcontrol(\$room: \$here); \</pre\> This would enable any
NPC\'s using [resource-control](NIPLibRefResourceControl) in the room.
Simple, isn\'t it?

\-- Main.KalleAlm - 23 Mar 2004

## Reference

This is a complete list of the functions available as of May 17, 2005:

### area_trigger_rcontrol(object \$room, int \$radius)

The `NPC::area_trigger_rcontrol()` function is used to force NPC\'s in
an environment, which have been disabled using the resource-control
system, to start up as if a PC had entered the room.

Note: as of May 17, 2005, the \$radius is capped at 1. It must be
provided, still, and in future revisions, it will support adjacent rooms
(\>1).

Note \#2: this function is currently a copy of
`NPC::trigger_rcontrol()`. Consider it a feature yet-to-exist.

### heartbeat_thread_running(object \$npc)

`NPC::heartbeat_thread_running()` is used to detect whether or not an
NPC is enabled. Previously, this check has been done by checking the
`"core:delays"` property, but as sophisticated NPC\'s sometimes contain
external delays/daemons, this has had to change and evolve a bit.

This function is used in the `heartbeat` thread to control startup
synchronization.

### purge_deliveries(object \$database)

Used internally by the courier/delivery system, this function is used to
purge old deliveries. As characters sometimes disappear or are absent
for an extended period of time, this function handles forced deliveries.

Purging deliveries is necessary in order to maintain a manageable size
of the delivery database.

A delivery is marked for purging when it has been enqueued for 30 days.

### purge_trash()

Similar to `NPC::purge_deliveries()`, `NPC::purge_trash()` is used to
purge the NIP trashcan from old objects.

When an NPC cleans a room or accepts trash from a character, the trashed
objects are placed in the nil, and added to a virtual trashcan. This is
done in order to prevent the destruction of important objects.

Currently, there is no interface to recover lost objects. However,
`NPC::purge_deliveries()` is sensitive to a canned object\'s location.
Thus, summoning an object out of the nil is sufficient to save it from
destruction.

The trashcan database **should not be altered manually under any
circumstances** \-- recovered objects should be summoned only. The
trashcan database is available as `Data:NIP:servants:trashcan` on all
servers. It cannot be renamed.

An object in the trashcan is marked for purging when it has been
enqueued for at least 24 hours.

### resolve_meta_family_data(string \$meta_fam)

This function is used internally by the [comm tool](NIPToolComm) to
compile meta family data (e.g. `"hi/hello there"`) into \"true\" family
data (`({ ({ "hi", "hello" }), "there" })`). It could theoretically be
used in external server/game-specific applications to produce family
data. It should not be used in \"on-the-fly\" operations, as it is far
too resource-consuming.

### trigger_rcontrol(object \$room)

The `NPC::trigger_rcontrol()` function is used to force NPC\'s in an
environment, which have been disabled using the resource-control system,
to start up as if a PC had entered the room.

\-- Main.KalleAlm - 16 May 2005
