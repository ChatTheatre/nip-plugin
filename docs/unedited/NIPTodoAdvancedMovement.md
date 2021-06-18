%META:TOPICINFO{author=\"soledadb\" date=\"1154310891\" format=\"1.0\"
version=\"1.11\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPTodoStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>TODO: Advanced movement\</FONT\>

\<font class=\"query\"\>PROJECT STATUS\</font\> INITIATED

\<font class=\"query\"\>STATUS NOTES\</font\>

External coder is working on this project.

\<font class=\"query\"\>ASSIGNED CODER(S)\</font\>

  ---------- ---------- -------------------------
  **Who**    **From**   **Contact information**
  External   Skotos     n/a
  ---------- ---------- -------------------------

\<font class=\"query\"\>WHAT?\</font\> Advanced movement, e.g \"figure
out the quickest path to move from room A to room B, and walk it.\"

\<font class=\"query\"\>PRIORITY\</font\> TOP

\<font class=\"query\"\>ETA?\</font\> n/a

\<font class=\"query\"\>HOW WILL IT WORK?\</font\> Whenever the NPC
decides it\'s time to move from one room to another, the advanced
movement feature will be used to calculate the path to take.

\<font class=\"query\"\>GENERAL DESCRIPTION\</font\>

The NPC will use a shared map over the setting from which it will
calculate the quickest path (taking into account any closed/locked doors
on the way, and whether or not the NPC itself has the proper key to the
locked once) from X1, Y1 to X2, Y2.

This path will then be sent to the NPC as a
[script](Trash.NIPTodoScriptSystem) and (optionally) the NPC will walk
the path.

\<font class=\"query\"\>LIBRARIES\</font\>

    [Library]         [Description]
    advmovement     Advanced movement library.

\<font class=\"query\"\>TECHNICAL COMMENTS\</font\>

There will be a commonly shared map of the system, gradually created
when NPC\'s use the advanced movement feature, which will cache paths
and solutions to paths in a centralized object. This object will be used
to calculate possible routes to take, excluding paths that include doors
that are locked (possibly, doors that are always locked \-- perhaps the
NPC should have some form of \"general idea\" on how often a door is
locked and from there decide to try or not) to which the NPC currently
do not possess a proper key.

The system will presume the \"path is clear,\" i.e. the NPC can walk
straight from point A to B, but if the NPC encounters a closed/locked
door (fails to leave through one of the set of exits), the NPC will
check if the door is closed. If it is, the NPC will try to open it. If
the door is locked, the NPC will check if it has a key to it. If the NPC
doesn\'t have a key, it will re-calculate the path and remember the
failure for future path calculations.

The door/locked etc. feature will probably be transferred to a separate
library and be optional.

\<font class=\"query\"\>LIST OF INTERESTED PARTIES\</font\>

If this subject interests you, please add yourself to the list below.
The more interest, the higher priority a subject will get. And also, by
doing so, we will be able to notify you specifically when this
subject\'s status has changed.

    [Your Name]      [Your Email]
    Tony Demetriou   ademet@ics.mq.edu.au
    Todd Nilson      wells@lovecraftcountry.com
    Soledad Bourdo   reveur@marrach.skotos.net
    [insert a separate line above this one]

\-- Main.KalleAlm - 03 Jun 2003

\<font class=\"query\"\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT
THIS SUBJECT\</font\>\<br\> (Please, don\'t forget to add your name to
your comment, preferably your TWiki-name.)

For an initial version, you do not really have to construct a map
datastructure in a database object. You can simply query the room
directly for its exit data when you\'re doing the path-finding
algorithm. For games that have many hundreds of rooms, this can
admittedly cause prohibitively much swapping, but building the map DB is
not trivial either. Once you start approaching map sizes of hundreds of
thousands of rooms you have to take measures to prevent the quadratic
cost of calculating the path. One traditional approach is to divide the
full-size maps into areas, and then only map room for room at the area
level. For example, Marrach could easily be split into one area for each
floor. Then, path-finding executes like this: if I want to go from A to
B, figure out which area A is, and which area B is. Figure out an AREA
level path from A-area to B-area, e.g. \"first floor, then second floor,
then third floor\". Then do path finds from A to \"the exit in first
floor that leads to second floor\" (which is precomputed/cached). Then
\"how do I get from there to the exit on the second floor that leads to
third floor\" (precomputed/cached). Etc, etc. This increases the size of
the map you can handle without explosive quadratic growth to tens of
thousands of rooms. There are many other approaches to large-scale path
finding too, but it\'s always a somewhat tricky problem since the
trivial solution to the problem can be so costly.

\-- Main.ParWinzell - 09 Jun 2003

I like the idea of having areas but that means the user (builder) needs
to do the work of specifying them each, unless a good way of calculating
these sensibly/accurately/automagically is implemented. Perhaps some way
of marking the borders between areas would be enough (like the green
arch between OB/IB) and then presume all \"levels\" are areas of
themselves. Of course, two exits leading up to level 2 doesn\'t
necessarily connect with each other, so these two areas would have to be
separate \"areas.\"

Should be interesting.

\-- Main.KalleAlm - 09 Jun 2003

A good start point is WOE structure itself. **In general**, any rooms in
the same WOE path are accessible from one another. So, you find the WOE
path of your current room and the WOE path of your destination, and then
walk the tree.

\-- Main.SpZiph - 10 Jun 2003

Couldn\'t the areas be built up like we do in 3D polygon mapping? Start
with a room, check all exits from it, and extend outwards until we find
a list of rooms that have no other entrances from this \"area\". We then
mark them as borders between areas. (and yes, this will mean many areas
are only one room large). Once you\'ve done this, you can combine nearby
small areas together to make one larger area, until you have a map that
suits the size of your world.

A better solution would be to watch which are these smaller one-room
areas are used most often, and use that as the border between areas.
That should naturally force stairwells, drawbridges etc. to form the
edges of the areas.

\-- Main.TonyDemetriou - 20 July 2005
