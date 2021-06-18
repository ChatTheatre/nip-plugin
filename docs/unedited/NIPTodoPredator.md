%META:TOPICINFO{author=\"kallea\" date=\"1069315012\" format=\"1.0\"
version=\"1.7\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPTodoStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>TODO: Predator\</FONT\>

\<font class=\"query\"\>PROJECT STATUS\</font\> COMPLETED

\<font class=\"query\"\>STATUS NOTES\</font\>

The system works. Report any bugs you find.

\<font class=\"query\"\>ASSIGNED CODER(S)\</font\>

  --------------- ---------- ----------------------------
  **Who**         **From**   **Contact information**
  Main.KalleAlm   Skotos     <kalle@marrach.skotos.net>
  --------------- ---------- ----------------------------

\<font class=\"query\"\>WHAT?\</font\> Predator library, for the hunting
wildlife.

\<font class=\"query\"\>PRIORITY\</font\> MEDIUM

\<font class=\"query\"\>ETA?\</font\> Finished 19 Nov 2003.

\<font class=\"query\"\>HOW WILL IT WORK?\</font\>

The system will include a number of features and settings for NPC\'s
that hunt other NPC\'s for prey; predators. The NPC predator will have a
number of prerequisites for \"valid targets\" and will, based on these,
act and attack nearby prey.

\<font class=\"query\"\>GENERAL DESCRIPTION\</font\>

An NPC cat could use the predator system to hunt for small animals, such
as mice or rats, etc. The rats would, in turn, contain some properties
which identified them as valid prey, and also contained the
functionality for the actual attack/killing of the target itself.

\<font class=\"query\"\>LIBRARIES\</font\>

    [Library]         [Description]
    predator            Used by the hunting NPC, the predator lib supports the predator aspects.
    prey                 Used by the hunted NPC, the prey lib deals with prey issues.

\<font class=\"query\"\>HOOKS\</font\>

    [Hook]            [Using signals]             [Description]
    predator            DECIDE                        The predator hook.

\<font class=\"query\"\>TECHNICAL COMMENTS\</font\>

(The predator hook and the predator library are both the same object,
located in Lib:NIP:lib.)

The predator library includes the functionality to make the predator
hunt for prey in various ways (of course extendable by means of creating
your own add-on libraries to the system).

The prey library, however, will include such things as \"what will I
turn into when I die? What will happen to me when I die?\" and \"how
will I try to avoid being killed?\"

**Predator** \<ul\> The predator has a number of merry regular- and
sig-hook scripts which are used to simulate an NPC hunting for prey, as
well as a number of properties which define how the predator functions.

**Predator properties** \<ul\> *nip:behavior:predator*\<pre\> - Property
type: object pointer - Syntax: \<Object:name\> - Default value: nil -
Description: The predator behavior DB points to the data object which
contains the recorded actions for when the NPC performs various
predator-related actions. \</pre\>

*nip:trait:predator:scavenger*\<pre\> - Property type: boolean - Syntax:
*1*\|*0* - Default value: 0 - Description: Is this predator a scavenger?
If 1 (yes), it will eat encountered dead carcass, but if 0 (no), it will
only eat prey it killed itself. \</pre\>

*nip:trait:predator:prey*\<pre\> - Property type: array - Syntax: ({
\"\<prey-type\>\", \"\<pret-type\>\", \... }) - Default value: ({
\"prey\" }) - Description: The prey array contains a list of which NPC
prey types the NPC would consider as \'prey\'. (see prey properties)
\</pre\>

*nip:stats:offense*\<pre\> - Property type: integer - Syntax: \<number\>
- Default value: 10 - Description: The offensive strength of the NPC.
\</pre\>

*nip:stats:agility*\<pre\> - Property type: integer - Syntax: \<number\>
- Default value: 10 - Description: The swiftness/agility of the NPC.
\</pre\> \</ul\>

**Predator merry scripts** \<ul\> *merry:lib:act:predator:attack* \<ul\>
The \'predator:attack\' script will issue an assault on the target prey.
The prey will be called on whether or not it escapes, by comparing the
randomize result of two numbers (predator offense versus prey defense),
and will return the appropriate response to the attacker. The
\'predator:attack\' script will fetch the stats for strength and
agility, and send these (unmodified by default) on to the \'defend\'
script in the prey for evaluation. The script will presume that the
property \"npc:prey\" is set to an object pointer of the prey target.
\</ul\> *merry:lib:handler:offer:eating* \<u\>(Replacement.)\</u\>
\<ul\> The eating offer handler will replace the eating library\'s
internail eating handler, as some internal checks are required (e.g. for
non-scavenger predators, for instance). \</ul\> \</ul\>

**Predator sig-hook scripts** \<ul\> *merry:lib:predator:DECIDE* \<ul\>
The predator decide sig-hook will continuously scan for prey in the area
in which the NPC is currently located, and will set in motion the hunt
for the target if various checks made think such is a good idea. It will
set the \'npc:prey\' object pointer to the selected prey. \</ul\>
\</ul\>

\</ul\>

**Prey** \<ul\> The prey has, like the predator, a number of merry
regular- and sig-hook scripts as well as a number of properties to
define the prey feature.

**Prey properties** \<ul\> *nip:behavior:prey*\<pre\> - Property type:
object pointer - Syntax: \<Object:name\> - Default value: nil -
Description: The prey behavior DB points to the data object which
contains the recorded actions for when the NPC performs various
prey-related actions. \</pre\>

*nip:trait:prey:type*\<pre\> - Property type: array - Syntax: ({
\"\<prey-type\>\", \"\<pret-type\>\", \... }) - Default value: ({
\"prey\" }) - Description: The prey:type array contains a list of which
NPC prey types the NPC belongs to. The matching of each individual prey
type must be found in the predator:prey property for a predator to
regard a specific NPC as valid prey. \</pre\>

*nip:stats:defense*\<pre\> - Property type: integer - Syntax: \<number\>
- Default value: 10 - Description: The defensive strength of the NPC.
\</pre\>

*nip:stats:agility*\<pre\> - Property type: integer - Syntax: \<number\>
- Default value: 10 - Description: The swiftness/agility of the NPC.
\</pre\> \</ul\>

**Prey merry scripts** \<ul\> *merry:lib:handler:prey:defend* \<ul\> The
\'prey:defend\' script will respond to an assault from a hunting
predator. The prey will determine whether or not it escapes, by
comparing the randomize result of two numbers (predator offense versus
prey defense), and will return the appropriate response. The prey:defend
script will presume that the properties \$predator, \$offense and
\$agility are sent as arguments for comparison. The prey:defend script
returns a boolean result value of the fight. \</ul\>
*merry:lib:handler:prey:die* \<ul\> The prey:die script will turn the
NPC prey from living prey into dead corpse. The NPC predator will also
keep track of whether or not it killed a target. The script will presume
the argument \$killer is set to the object reference of the predator
which slays it. \</ul\> \</ul\>

\</ul\>

\<font class=\"query\"\>LIST OF INTERESTED PARTIES\</font\>

If this subject interests you, please add yourself to the list below.
The more interest, the higher priority a subject will get. And also, by
doing so, we will be able to notify you specifically when this
subject\'s status has changed.

    [Your Name]      [Your Email]

    Todd Nilson (Lovecraft Country), storyplotterwells@yahoo.com
    [insert a separate line above this one]

\-- Main.KalleAlm - 17 Nov 2003

\<font class=\"query\"\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT
THIS SUBJECT\</font\>\<br\> (Please, don\'t forget to add your name to
your comment, preferably your TWiki-name.)
