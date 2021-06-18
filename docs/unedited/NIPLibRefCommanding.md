%META:TOPICINFO{author=\"kallea\" date=\"1150029360\" format=\"1.0\"
version=\"1.5\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPSpecStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>LIBRARY REFERENCE: commanding\</FONT\>

\<font class=\"query\"\>CATEGORY:\</font\> [Service](NIPCategoryService)

\<font class=\"query\"\>WOE NAME:\</font\> Lib:NIP:lib:commanding

\<font class=\"query\"\>DEPENDENCIES:\</font\> None.

\<font class=\"query\"\>COMPATIBILITY:\</font\> None/All.

\<font class=\"query\"\>INCOMPATIBILITY:\</font\> None.

\<font class=\"query\"\>FEATURES\</font\>

The commanding lib is used to handle evoked commands to NPC\'s, and may
come in handy when making guards whom obey orders or animals who do
tricks, or anything similar.

The library provides two functions, **lib:core:add_command** and
**lib:core:sub_command** inherited in the NPC when the lib has been
loaded. These functions can be used to add/remove scripts to the command
chain, **\"nip:trait:commands\"**.

Example lib:init script for a library using the command lib, which adds
a command *\"jump\"* which is triggered when someone says *\"jump\"*,
*\"bounce\"* or *\"skip\"* to the NPC.

    --- <B>merry:lib:init</B> in <B>Example:Library:Using:Commanding</B> ---
      Call( this, "core:add_command", $trigger: ({ "jump", "bounce", "skip" }), $script: "jump" );
    ---

The script in the above example **must** be named
merry:lib:command:*jump*. Read [the naming rules for
scripts](NIPScriptGroups) for further information on this.

\<font class=\"query\"\>DESCRIPTION\</font\>

The commanding library hooks the
**react-post:evoke-dob**/**react-post:evoke-iob**-scripts in the NPC on
load, which in turn call the **lib:commanding** script. The commanding
script checks the command chain (**\"nip:trait:commands\"**) for any
matches in the evoke. The first match (if any) triggers the appropriate
lib:command:\*-script. This means that you must call any script called
in this way [lib:command:something](NIPScriptGroups), or it won\'t be
found.

\<font class=\"query\"\>NIP PROPERTIES\</font\>

\<font class=\"lib\"\>nip:trait:commands\</font\> \<UL\> Mapping of
trigger-\>script references. \</UL\>

\<font class=\"query\"\>LIBRARY SCRIPT REFERENCE(S)\</font\>

\<font class=\"lib\"\>merry:lib:commanding\</font\> \<UL\> This script
is called from the **react:evoke-dob**/**react:evoke-iob**-scripts
whenever something is spoken to the NPC.\<br\> It scans the
**\"nip:trait:commands\"** property in the NPC for possible
interpretations and, if found, executes the appropriate script (again,
if found). \</UL\>

\<font class=\"lib\"\>merry:lib:core:add_command\</font\> \<UL\> The
add_command script is a function for use by libraries using the
commanding library, and is used to add trigger-to-script references to
the command chain.\<br\> The script takes two arguments, **\$trigger**
and **\$script**, both required.\<BR\> The \$trigger argument may be **a
string** or **array of strings**.\<BR\> The \$script argument must refer
to a merry:lib:command:**(\$script)**-merry script which must reside,
inheritantly or natively, in **this** (the NPC). \</UL\>

\<font class=\"lib\"\>merry:lib:core:sub_command\</font\> \<UL\> The
sub_command script removes references from the command chain.\<BR\> It
requires one argument, **\$trigger**, which may be **a string** or
**array of strings**. \</UL\>

\<font class=\"lib\"\>merry:react-post:evoke-dob\</font\>,\<font
class=\"lib\"\> merry:react-post:evoke-iob\</font\> \<UL\> These scripts
are shells for direct-object and indirect-object evoke signals, and call
the \<font class=\"lib\"\>merry:lib:commanding\</font\> script. \</UL\>

\-- Main.KalleAlm - 05 Jun 2003

\<font class=\"query\"\>COMMENTS, BUGS, SUGGESTIONS, ETC. ABOUT THIS
LIBRARY\</font\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)

Kalle is it possible to get an actual Tutorial on using this particular
library? I\'ve ready over the information here several times, and really
cant make heads or tails of it. I\'m attempting, well was attempting to
use in for our new Pets on Lazarus, but because of my inability to
properly read and use this I\'ve been forced to create a library of
commands through merry. I just wonder if, using the command library, it
would have been an easier. \-- Main.StoryBuilderLilith - 07 Jun 2006

It\'s already there: NIPHowCommanding :) -Kalle.
