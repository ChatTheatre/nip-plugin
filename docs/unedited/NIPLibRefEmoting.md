%META:TOPICINFO{author=\"kallea\" date=\"1116192129\" format=\"1.0\"
version=\"1.7\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>LIBRARY REFERENCE: emoting\</FONT\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Appearance](NIPCategoryAppearance)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:emoting

\<font class=\"query\"\>DEPENDENCIES:\</font\> None.

\<font class=\"query\"\>COMPATIBILITY:\</font\> [MOOD](NIPHookRefMood)

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

Parser emoting functionality for CNPCs. The emoting library makes use of
a behavior database and randomly emotes via the parser.

If the NPC is using moods, the emoting library will look in the
specified database for mood-specific data. See [How To record a behavior
database](NIPHowRecord) for further details.

\<font class=\"query\"\>DESCRIPTION\</font\>

The emoting library uses a (group of) specified behavior database(s) to
randomly express how an NPC feels (if moods are available), or simply to
show it\'s alive.

The library uses behavior databases constructed using the NIP extension
Lib:NIP:EXT:record (to be documented) \-- again, see [How To record a
behavior database](NIPHowRecord) for details on this.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

\<font class=\"lib\"\>nip:trait:emoting:frequency\</font\> \<UL\> The
emoting frequency. The default value is 10, which means the NPC will
emote on average every 200th second (i.e. every 3m20s\'d).

The lower the value, the more frequent the NPC\'s emotes will be (every
(20 \* frequency)\'th second, on average). \</UL\>

\<font class=\"lib\"\>nip:trait:titles:default\</font\> \<UL\> Default
titles to use for men/women when they have none and the behavior uses
the \"(title)\" keyword. This defaults to \"sir/ma\'am\" if no property
is set whatsoever.

The system attempts to grab the property from <Data:NIP:system>
(titles:default) when the emoting library is added to an NPC. \</UL\>

\<font class=\"lib\"\>nip:behavior:db\</font\> \<UL\> This property
should point to the default behavior database which should be used when
no other more appropriate one is found. Initially, this value is not
set, so **you have to do it to make emoting work**. \</UL\>

\<font class=\"lib\"\>nip:behavior:\<mood\>\</font\> \<UL\> The
properties nip:behavior:\* are fetched by the emoting system based on
the NPC\'s current mood.

If, for instance, the NPC is currently \"**HAPPY**\", the emoting system
will first look for a **\"nip:behavior:happy\"** property, and if none
is found, it will go for the aforementioned **\"nip:behavior:db\"**.
\</UL\>

\<font class=\"lib\"\>nip:trait:hints:db\</font\> \<UL\> The standard
hints database, in which rumors are stored. This is optional but
internally supported. When recording behavior, if the emote \"(hint)\"
is used, the NPC will attempt to draw hints from the hints database
instead of using static emotes. Also see +nip command \"hints\". \</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:behave\</font\> \<UL\> Shorthand script
for the emoting parser. \<pre\> merry \-\-- ::behave(\$db: object,
\$mood: string); \-\-- \</pre\> \</UL\>

\<font class=\"lib\"\>merry:lib:emoting:decide\</font\> \<UL\> (Signal
DECIDE, hook emoting)\<br\> This sig-hook script will randomly force the
NPC to emote something specified in the appropriate behavior
database(s).\<br\> The script will not be executed if the NPC is
[sleeping](NIPLibRefSleeping). \</UL\>

\<font class=\"lib\"\>merry:lib:handler:emoting:parse\</font\> \<UL\>
The database parser. This is used by the emoting/DECIDE sig-hook script
to perform a random parser move from a specific db/mood. \</UL\>

\-- Main.KalleAlm - 07 Jun 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)

Fixed minor issue with property map that could cause a crash in
invalidly configured nippers.

\-- Main.KalleAlm - 12 May 2005

Added \"nip:trait:titles:default\" property.

\-- Main.KalleAlm - 15 May 2005
