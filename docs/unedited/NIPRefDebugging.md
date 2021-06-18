%META:TOPICINFO{author=\"kallea\" date=\"1069935269\" format=\"1.0\"
version=\"1.1\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>NIP Debugging reference\</font\>

At this point, the NIP system has grown so much that more than I are
using it, and more than I are coding for it. This grants some reference
for knowledge on the various options an NPC-designer or NIP library
builder has available in regards to debugging.

[]{.twiki-macro .TOC}

------------------------------------------------------------------------

# Reading debug data.

There is already a bunch of debug information in the system. Most of it
is invisible unless you specifically take a look at it, though. A few
options are available;

## Possessing the npc.

Possessing the NPC is one way of debugging it. A lot of information is
sent to the NPC in form of emits that are never seen by anyone else.
These emits are useful to give a glance if for instance your NPC keeps
crashing, or if the NPC refuses to do something that it\'s expected to
do.

------------------------------------------------------------------------

## Using the lfc.

The LFC (Log Feed Channel) is a chat channel used specifically by
systems on the server to transmit debug information and notifications on
various things. This channel at times has a high volume of traffic, but
thankfully, it has some filtering rules that you may use to receive only
the information you are interested in.

To enable and use the LFC, and only receive NIP specific data, do the
following:

    > +lfc 'on'
    You start listening to LFC.
    > +lfc '+NIP'
    Hook "nip" added to hook list, displaying all messages of priority COMMENT and up.

------------------------------------------------------------------------

# Writing debug data.

As for the coding audience, there are a few tricks that are commonly
used when coding NPC libs or features. There are in general two ways
that are preferred for debugging data, both of which are mentioned
above.

## Emitting to the npc body, \'this\'.

Sending an emit to \'this\' will ensure that noone unexpected gets your
message (unless non-staffers are going to possess NPC\'s, which is a bad
idea in general).

    EmitTo( this, "Some debug data." );

Coders will then be expected to possess the NPC to receive your
notification. This is sometimes good, but in some cases, coders are not
as well versed with this as one would like, which leads to the
secondary, and in some cases better, alternative.

------------------------------------------------------------------------

## Using the lfc.

The NIP system has a built-in extended logging feature, which can be
used to easily emit debug entries to the LFC.

The syntax for this feature is as follows:

    ::log( $subject:  (object) in which the error occured (usually this)
             $error:     (string) description of the error that occured
             $ecode:     (int)   error-code (if any).
             $expected: (string) what did expect, that we didn't get?
             $got:      (string) what did we instead get, that we didn't expect?
          );

\* \$subject is optional, and should usually be ignored. Most often,
\"this\" is the object in which the error occured. \* \$error should be
short and brief. Something like \"Unexpected value.\"

An example in which this is used is in the eating:decide script;

    if( !grammes ) {
      ::log( $error: "Invalid value for property \"nip:trait:eating:grammes\"",
                $expected: "float",
                $got: "nil" );
      return nil;
    }

This is a live example of how a debug logging might appear using the
LFC.

Of course, this has its pro\'s and its con\'s. If a user does not hae
the LFC enabled, they won\'t get our debug messages. Similarly, if we
send too many debug messages, people will not want to keep it enabled,
as it\'s spamming their eyes out.

For important notifications, using the LFC is preferred, though.

------------------------------------------------------------------------

\-- Main.KalleAlm - 27 Nov 2003
