%META:TOPICINFO{author=\"toddn\" date=\"1139507887\" format=\"1.0\"
version=\"1.9\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>LIBRARY REFERENCE: eating\</FONT\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Behavior](NIPCategoryBehavior)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:eating

\<font class=\"query\"\>DEPENDENCIES:\</font\> [offers](NIPLibRefOffers)

\<font class=\"query\"\>COMPATIBILITY:\</font\> [MOOD](NIPHookRefMood)

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

The eating library provides, if the MOOD signal is available, the
\'HUNGRY\' mood automatically. It uses the [offers](NIPLibRefOffers)
library to accept food offered to it (something that can be disabled
and/or restricted at the whim of the user).

It eats food in its hands if it\'s hungry enough.

It also takes food in its environment, if it\'s very hungry.

The hunger is determined by looking at the **\"npc:energy\"** property.

\<font class=\"query\"\>DESCRIPTION\</font\>

The eating library is pretty much described above. It adds the aspect of
hunger to the NPC and the mood (if appl.) \'HUNGRY\' as well.

Internally, the NPC keeps track of the **\"npc:energy\"** value which
determines how hungry it is (the lower energy, the hungrier). The hunger
is also affected by the **\"nip:trait:eating:grammes\"**, which
specifies (in grammes) how much food the NPC has to eat to be \"full\".
The property **\"nip:trait:eating:accepts\"** represents a list of
properties that the NPC will regard as \'food\'.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

\<font class=\"lib\"\>nip:trait:eating:accepts\</font\> \<UL\> Mapping,
like (\[ \"property name\" : \"property value\" \]) specifying a list of
properties and values. These values are then used in the \<font
class=\"lib\"\>merry:lib:handler:offer:eating\</font\> script, whereas
if either is found in an offered item, the NPC will accept it as food
(if it\'s hungry enough). \</UL\>

\<font class=\"lib\"\>nip:trait:eating:burn\</font\> \<UL\> Float, the
number of grammes of food (energy) burnt per hour.

Default value is 300 grammes per hour, which will let the default NPC (2
kg energy stock) hungry once every \~6-7th hour.

The burn rate is how many grammes the NPC burns. The **lower** that
value, the **less** hungry it will be, or rather, the longer it will go
full. \</UL\>

\<font class=\"lib\"\>nip:trait:eating:grammes\</font\> \<UL\> Integer,
describes how many grammes of food an NPC must eat to be full. \* If the
relative hunger (energy / grammes) is less than 0.5, the NPC will eat if
it has food in its inventory. \* If the relative hunger is less than 0.3
(w/ some random modifiers), the NPC will get anything it regards as
food, which lies in its direct environment.

\</UL\>

\<font class=\"lib\"\>npc:energy\</font\> \<UL\> Integer. The npc:energy
value determines the NPC\'s current fat reserves: the lower the value,
the hungrier the NPC. The higher the energy value, the more food it can
eat before it is full. Energy is decreased based on the burn rate, so a
very high energy with a low burn rate will result in an NPC that eats
**less** often. To figure out the relational hunger of the NPC, do
(this.**\"npc:energy\"** / this.**\"nip:trait:eating:grammes\"**).
(Multiply that by 100 to get a percentage value.)

\</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:act:eat\</font\> \<UL\> This script is
triggered whenever the NPC eats something. The script is responsible for
increasing the NPC\'s energy a bit (**\"npc:energy\"**) whenever it
takes a bit of something. \</UL\>

\<font class=\"lib\"\>merry:lib:done-post\</font\> \<UL\> NIP Library
de-initialization script. \</UL\>

\<font class=\"lib\"\>merry:lib:eating:decide\</font\> \<UL\> (Signal
DECIDE, hook eating)\<br\> This script scans the energy values and
decides if the NPC should do something about its hunger, and if so,
what. \</UL\>

\<font class=\"lib\"\>merry:lib:eating:internal\</font\> \<UL\> (Signal
INTERNAL, hook eating)\<br\> This script simply makes the NPC gradually
hungrier. \</UL\>

\<font class=\"lib\"\>merry:lib:eating:mood\</font\> \<UL\> (Signal
MOOD, hook eating)\<br\> This script is only loaded if the MOOD signal
is present. It will modify the \"HUNGRY\" mood according to the hunger.
\</UL\>

\<font class=\"lib\"\>merry:lib:handler:offer:eating\</font\> \<UL\>
This handler script is called from the **react-post:offer-to** script,
as specified in [the offers library](NIPLibRefOffers). \</UL\>

\<font class=\"lib\"\>merry:lib:hook:init-post\</font\> \<UL\> This
script is attached to a special hook called \"hook\" which is triggered
whenever a hook is loaded, where **\$HID** is the hook ID. \</UL\>

\<font class=\"lib\"\>merry:lib:init\</font\> \<UL\> (NIP Library init
script.)\<br\> This script adds the handler \"offer:eating\" (\<font
class=\"lib\"\>merry:lib:handler:offer:eating\</font\>) to the offer
chain. \</UL\> \</font\>

\-- Main.KalleAlm - 05 Jun 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
