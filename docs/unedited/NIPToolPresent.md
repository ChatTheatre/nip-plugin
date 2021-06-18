%META:TOPICINFO{author=\"kallea\" date=\"1076977200\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPToolStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>+NIP TOOL: Present\</FONT\>

\<QUERY\>SYNTAX:\</QUERY\> +nip \<npc\> \"present add\|sub name/woe-name
newname1, 2, \...\"

\<QUERY\>AFFECTED / CONCERNED LIBS/ETC.:\</QUERY\>
[presents](NIPLibRefPresents)

\<QUERY\>GENERAL DESCRIPTION:\</QUERY\>

The \'presents\' function is used to deal with the management of items
an NPC may offer to a character in the game, such as scrolls for
couriers or food for cooks. For example, if you wish to add the object
NPC:misc:scroll to a summoned courier NPC, you would do:

    > +nip courier "present add NPC:misc:scroll"

This would automatically use the names provided in the scroll itself, so
that people could \"ask courier for scroll\" to receive a scroll, and
could also \"ask courier for parchment\" as that is a sname provided in
the object NPC:misc:scroll itself. However, if you wish to set the names
avaiable yourself, you may optionally do so as well:

    > +nip courier "present add NPC:misc:scroll scroll, paper"

\-- Main.KalleAlm - 09 Aug 2003

\<QUERY\>COMMENTS AND SUGGESTIONS, THOUGHTS ETC. ABOUT THIS
SUBJECT\</QUERY\>\<br\> (Please, don\'t forget to add your name to your
comment, preferably your TWiki-name.)
