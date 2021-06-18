%META:TOPICINFO{author=\"kallea\" date=\"1085145459\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: spawn-equipment\</font\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Internal](NIPCategoryInternal)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:spawn-equipment

\<font class=\"query\"\>DEPENDENCIES:\</font\> None.

\<font class=\"query\"\>COMPATIBILITY:\</font\> None specific.

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None known.

\<font class=\"query\"\>KNOWN ISSUES:\</font\>

Confirmed () issues with this library. (Unconfirmed issues should be
reported in the feedback section at the bottom of this document.)

\<font class=\"query\"\>FEATURES\</font\>

Spawning of objects, setting properties in new-spawned objects, placing
new-spawned object(s) in specific other new-spawned object(s),
wield/wear objects, automatically at nipper spawn-time.

\<font class=\"query\"\>DESCRIPTION\</font\>

The spawn-equipment library is a sibling of the
[spawn-traits](NIPLibRefSpawnTraits) lib, but works on objects rather
than properties.

Spawn-equipment is defined using four properties, described in detail
below. Whenever a nipper using spawn-equipment is **spawned**, that
nipper\'s spawn-equipment settings will immediately be kicked in place
and the nipper will spawn and customize the objects in its list, in
order of appearance.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

`object *<font class="lib">nip:trait:equipment:list</font>` \<UL\>
(Required.)\<br/\> Array listing each object that should be spawned into
the nipper\'s inventory. \</UL\>

`mapping <font class="lib">nip:trait:equipment:specify</font>` \<UL\>
(Optional.)\<br/\> Mapping used to specify some/all object\'s spawn
behavior. Available behavior is:\<pre\> 1 (TRUE) - Wear/wield, if
possible. 0 (FALSE) - Place object in inventory, even if wear/wieldable.
\<object\> - Move into \<object\>\'s inventory. Good for e.g. swords
into scabbards.\</pre\> \</UL\>

`mapping <font class="lib">nip:trait:equipment:set</font>` \<UL\>
(Optional.)\<br/\> Two-dimensional mapping object-to-property-to-value
in the following manner:\<pre\>(\[ \<object\> : (\[ \"\<property\>\" :
\<value\> \]) \])\</pre\>

E.g.:\<pre\> \"nip:trait:equipment:set\" = (\[
\<MGMarrach:clothing:scabbard-short\> : (\[ \"alteration:color\" :
\"brown\", \"alteration:color:desc\" : \"brown\", \"alteration:fit\" :
\"practical\", \"alteration:fit:desc\" : \"practically fitted\",
\"alteration:symbol\" : \"castle\", \"alteration:symbol:desc\" :
\"castle\" \]) \])\</pre\> \</UL\>

`mapping <font class="lib">nip:trait:equipment:prop</font>` \<UL\>
(Optional.)\<br/\> Map of property-name in nipper to set to reference of
new spawns of objects. Example:\<pre\> \"nip:trait:equipment:prop\" =
(\[ \<MGMarrach:clothing:scabbard-short\> : \"npc:fighting:weapon\",
\<MGMarrach:weapons:dagger\> : \"npc:fighting:scabbard\" \])\</pre\>
\</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:handler:start:equip\</font\> \<UL\>
Spawn-start trigger, which spawns and sets the object(s) and nipper as
specified in the properties above. \</UL\>

\-- Main.KalleAlm - 09 May 2004

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
