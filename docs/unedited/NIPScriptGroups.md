%META:TOPICINFO{author=\"kallea\" date=\"1054851821\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
\<style\> b { color: \#000000; font-weight: bold; } A { text-decoration:
none; font-size: 11pt; color: \#0000ff; } .title { font-size: 20pt;
font-weight: bold; color: \#000000; } \</style\>

\<FONT CLASS=\"title\"\>Script naming rules and meaning\</FONT\>

Quickly, the NPC will begin to hoard up scripts.

    > +tool merry list %Marrach:players:G:gruffle
    Merry code found in Marrach:players:G:gruffle:
         <B>Inherited from Lib:NIP:base:hooks:delay:</B>
              lib:delay:delay-exec
              lib:delay:delay-init
         <B>Inherited from Lib:NIP:base:hooks:decide:</B>
              lib:decide:decide-exec
              lib:decide:decide-init
              lib:decide:decide-post
         <B>Inherited from Lib:NIP:base:lib:signals:</B>
              lib:calc_sighookpath
              lib:modify:signals
              setprop-post:signal
         <B>Inherited from Lib:NIP:lib:offers:</B>
              lib:core:add_offer
              lib:core:sub_offer
              react-post:offer-to
         <B>Inherited from Lib:NIP:signals:MOOD:</B>
              lib:core:add_mood
              lib:core:sub_mood
         <B>Inherited from Lib:NIP:lib:emoting:</B>
              lib:emoting:decide
         <B>Inherited from Lib:NIP:hooks:mood:</B>
              lib:mood:delay
              lib:mood:mood-exec
              lib:mood:mood-init
         <B>Inherited from Lib:NIP:base:signals:DECIDE:</B>
              setprop-post:decide
         <B>Inherited from Lib:NIP:lib:happiness:</B>
              lib:happiness:mood
         <B>Inherited from Lib:NIP:lib:eating:</B>
              act:eat
              lib:eating:decide
              lib:eating:internal
              lib:eating:mood
              lib:handler:offer:eating
         <B>Inherited from Lib:NIP:base:lib:hooks:</B>
              lib:core:find-hook
              lib:core:register-hook
              lib:core:unregister-hook
              lib:modify:hooks
              setprop-post:hook
         <B>Inherited from Lib:NIP:core:</B>
              lib:core:merry_add
              lib:core:merry_delete
              lib:find_nip_object
              lib:heartbeat
              lib:modify:libraries
              setprop-post:add
              setprop-post:del
              setprop-post:delete
              setprop-post:sub
         <B>Inherited from Lib:NIP:lib:anger:</B>
              lib:anger:mood
         <B>Inherited from Lib:NIP:lib:sleeping:</B>
              lib:act:sleep:state
              lib:handler:state:awake
              lib:handler:state:sleep
              lib:sleeping:decide
              lib:sleeping:delay
              lib:sleeping:internal
              lib:sleeping:mood
         <B>Inherited from Lib:NIP:base:lib:stream:</B>
              setprop-post:sigexecptr
         <B>Inherited from Lib:NIP:base:hooks:internal:</B>
              lib:internal:internal-exec

Which is, admittedly, a lot of scripts. Thankfully, we don\'t need to
care about the majority of those, and thankfully, most of them are very
small.

Now, since there are so many scripts, we can\'t just go in and make a
script called lib:kalles:script without thinking. What if someone else
made a lib:kalles:script for his NPC. What if he then happily adds the
lib I put lib:kalles:script in to his own NPC?

Some form of control was necessary, and thus the following set of groups
and rules have been decided upon:

**Groups:**

There are four set groups:

\* **lib:core:\***\<UL\>Core add-ons for libraries, hooks and signals.
Such as add_offer/sub_offer (from library \'offers\') or
add_mood/sub_mood (from signal \'MOOD\'). These are usually related to
the management or configuration of the system, rather than having a real
impact on the NPC \"in-game\".\</UL\> \*
**lib:handler:\***\<UL\>Internal scripts, less core, named
\"feature:action\". Such as handler:offer:eating (from \'offers\') or
handler:state:awake/sleep (from \'sleeping\'). These scripts are usually
related to in-game actions or issues, such as waking up/falling asleep
or acting on a react-post:offer-to trigger.\</UL\> \*
**lib:command:\***\<UL\>The lib:command:\*-scripts are called from the
[commanding](NIPLibRefCommanding) library as a part of the command chain
solution.\</UL\> \* **lib:\***\<UL\>Reserved for system functions and
*hook:signal* functions.\</UL\>

\-- Main.KalleAlm - 01 Jun 2003
