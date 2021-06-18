%META:TOPICINFO{author=\"kallea\" date=\"1069181559\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
\<style\> b { font-size: 12pt; color: \#000000; font-weight: bold; } A {
text-decoration: none; font-size: 11pt; color: \#0000ff; } .title {
font-size: 20pt; font-weight: bold; color: \#000000; } \</style\>

\<FONT CLASS=\"title\"\>Property naming rules and meaning\</FONT\>

As you will realize soon enough, a lot of properties are handled when
dealing with the NPC system. Customization properties, condition
properties, system properties, etc. all reside in the NPC itself
(wherelse would they be, as each NPC has its own custom design?).

To make it easier to read these values, they have been separated into
groups and sub-groups. This is also because it should be apparent which
of these can be altered away, and which should be left to be handled by
the system.

There are three main property groups: \* **nip-core**:\* \* **nip**:\*
\* **npc**:\*

**nip-core** is the most difficult to read property, but thankfully,
noone should ever have to modify it on their own. It contains a list of
libraries and hooks, the cached signal hook path, etc.

**nip** contains all the customizable settings, and is further divided
into (currently) four sub-groups: \* nip:**behavior**:\* \*
nip:**mood**:\* \* nip:**offer**:\* \* nip:**stats**:\* \*
nip:**trait**:\*

**nip:behavior** contains behavior database information,\<br\>
**nip:mood** contains the mood settings,\<br\> **nip:offer** contains
offer settings,\<br\> **nip:stats** contains numeric stats for the NPC,
such as strength, agility, etc,\<br\> **nip:trait** contains a set of
sub-sub-groups, usually named after the hook/library/signal which uses
them (e.g. \'eating\', \'emoting\' and \'sleeping\').

**npc** contains all condition properties, basically it\'s a listing of
how the NPC feels at this very moment.\<br\>

    +stat gruffle "property:npc:*"
    -- Properties (npc:*)--
    Property: npc:energy = 722
    Property: npc:mood = "HUNGRY"
    Property: npc:state = "awake"
    Property: npc:weariness = 10590

\-- Main.KalleAlm - 01 Jun 2003 (18 Nov 2003)
