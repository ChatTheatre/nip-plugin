%META:TOPICINFO{author=\"kallea\" date=\"1151685240\" format=\"1.0\"
version=\"1.4\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>LIBRARY REFERENCE: relations\</font\>

\<font class=\"query\"\>CATEGORY:\</font\>
[Behavior](NIPCategoryBehavior)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:relations

\<font class=\"query\"\>DEPENDENCIES:\</font\> None.

\<font class=\"query\"\>COMPATIBILITY:\</font\> All.

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

Relations reaction and recall. Using the complex relation-rules builder,
define how a nipper reacts to various (physical) actions directed
towards it, such as when someone grins at the nipper, or kicks the
nipper, and so on.

Additionally keep track of any number of relations categories, which can
be modified (improved or impaired) using triggers in a rule.

\<font class=\"query\"\>DESCRIPTION\</font\>

The relations system allows you to define a set of rules which an NPC
uses to determine how a character is behaving towards them. For
instance, a barmaid might wink at you when she delivers you beer if
you\'ve been acting friendly enough towards her for an extended period
of time, or she might flat out refuse to serve you if you\'ve been
pinching her butt once too many (you dirty, dirty old man).

The relations system lets the nipper do one or both of two things: 1 It
reacts to actions directed at it 2 It remembers the action by altering a
relationship for the actor

This can be extended infinitely. You could theoretically use the
`query_relationship` function in whatever code (say, the \"actor wants
to buy beer\" code) and determine if the actor\'s friendship is too low
to serve him. This might look something like this: \<ul\>

    int rel;

    rel = ::query_relationship($category: "friendship");
    if (rel < -30) {
         /* Nope, they suck. Act out refusal. */
         ::behave($db: this."nip:behavior:relations", $mood: "REFUSE", $subject: $actor);
         return FALSE;
    } else if (rel > 30) {
         /* Let's give'm a wink, cause they've been nice. */
         ::behave($db: this."nip:behavior:relations", $mood: "FLIRT", $subject: $actor);
    } else {
         /* Be professional. */
         ::behave($db: this."nip:behavior:relations", $mood: "PROFESSIONAL", $subject: $actor);
    }
    /* give-actor-their-beer code goes here */

\</ul\>

The above code would first fetch the \"friendship\" relationship and
dump it in the rel integer. THen it\'d check first if the actor\'s been
TOO MEAN to be served. If they have, it behaves using the internal
behavior system and then exits. If they haven\'t been too mean, it
checks if they\'ve been GOOD ENOUGH to deserve special treatment in the
form of flirting. If they haven\'t, the NPC simply behaves as it will
any normal, new customer. It is only in the \'too mean\' instance where
the code refuses to give the actor beer (by returning before it reaches
the \"give-actor-their-beer\" code).

This can be applied and used in any number of ways with a bit of Merry
skills.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

\<font class=\"lib\"\>nip:trait:relations:db\</font\> \<UL\> The data
object in which the relations structure is set up. \</UL\>

\<font class=\"lib\"\>nip:behavior:relations\</font\> \<UL\> The BDO
containing relations behavior. \</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:handler:relations\</font\> \<UL\>
\<pre\>\"This script is used by the relations NIP library to determine
the type of action performed.

The script requires that the property \'nip:trait:relations:db\' exists,
and points to a valid property-container with relations data.\"\</pre\>
\</UL\>

\<font class=\"lib\"\>merry:lib:query_relationship\</font\> \<UL\>
query_relationship(\$actor: object, \$category: string) \[figure out
\"my\" relationship with \$actor for the category \$category\]

Return value: (int) Numeric relationship. \</UL\>

\<font class=\"lib\"\>merry:react:command-iob/dob%nip-relations\</font\>
\<UL\> \<pre\>These scripts \"pipe\" commands to
lib:handler:relations.\</pre\> \</UL\>

\-- Main.KalleAlm - 08 Dec 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)

Note that this library reference was modified June 30th, 2006, to adhere
to the new relations system. - Main.KalleAlm.
