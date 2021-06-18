%META:TOPICINFO{author=\"kallea\" date=\"1068891300\" format=\"1.0\"
version=\"1.10\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
\<style\> b { font-size: 10pt; font-weight: bold; } A { text-decoration:
none; font-size: 11pt; color: \#0000ff; } .title { font-size: 20pt;
font-weight: bold; color: \#000000; } ROOT { color: \#ff0000;
font-weight: bold; font-size: 12pt; } REQ { color: \#ff0000;
font-weight: bold; } SUPP { color: \#00dd00; font-weight: bold; }
\</style\>

\<FONT CLASS=\"title\"\>System map\</FONT\>

    <TABLE BORDER=0 CELLSPACING=0 CELLPADDING=3>
    <TR><TD><B>OBJECT</B></TD> <TD><B>DESCRIPTION</B></TD> <TD><REQ>REQ</REQ></TD> <TD><SUPP>SUPPORTS</SUPP></TD> </TR>

    <TR><TD><ROOT>Data:NIP</ROOT></TD><TD>- <ROOT>System and user data</ROOT></TD></TR>
    <TR><TD>    NCS</TD><TD>- NIP Communications System data</TD></TR>
    <TR><TD>    functions</TD><TD>- Function link for the +nip command</TD></TR>
    <TR><TD>    system</TD><TD>- System configuration</TD></TR>
    <TR><TD>    <B>behavior</B></TD><TD>- Behavior databases</TD></TR>
    <TR><TD>        bert</TD><TD>- example DB</TD></TR>
    <TR><TD>        gruffle</TD><TD>- example DB</TD></TR>
    <TR><TD>        livestatue</TD><TD>- example DB</TD></TR>
    <TR><TD>        phoenix</TD><TD>- example DB</TD></TR>
    <TR><TD>        snuggles</TD><TD>- example DB</TD></TR>
    <TR><TD>        <B>musicians</B></TD><TD>- Marrach musicians example folder</TD></TR>
    <TR><TD>&nbsp;</TD></TR>
    <TR><TD><ROOT>Lib:NIP</ROOT></TD><TD>- <ROOT>Core system plus libs, signals and hooks</ROOT></TD></TR>
    <TR><TD>    NCS</TD><TD>- NCS (NIP Communications System).</TD></TR>
    <TR><TD>    basefuns</TD><TD>- Base functions used by +NIP</TD></TR>
    <TR><TD>    core</TD><TD>- The core system object</TD></TR>
    <TR><TD>    updates</TD><TD>- The update revisions code.</TD></TR>
    <TR><TD>    <B>EXT</B></TD><TD>- External libraries</TD></TR>
    <TR><TD>        bedit</TD><TD>- Behavior editor data</TD></TR>
    <TR><TD>        record</TD><TD>- The behavior record system</TD></TR>
    <TR><TD>    <B>base</B></TD><TD>- Base system libraries</TD></TR>
    <TR><TD>        <B>hooks</B></TD><TD>- System hooks</TD></TR>
    <TR><TD>            decide</TD><TD>- The internal DECIDE signal hook</TD></TR>
    <TR><TD>            delay</TD><TD>- The internal DELAY signal hook</TD></TR>
    <TR><TD>            internal</TD><TD>- The internal INTERNAL signal hook</TD></TR>
    <TR><TD>        <B>lib</B></TD><TD>- System libs</TD></TR>
    <TR><TD>            hooks</TD><TD>- The 'hooks' system</TD></TR>
    <TR><TD>            signals</TD><TD>- The 'signals' system</TD></TR>
    <TR><TD>            stream</TD><TD>- Signal stream system</TD></TR>
    <TR><TD>        <B>signals</B></TD><TD>- System signals</TD></TR>
    <TR><TD>            DECIDE</TD><TD>- The DECIDE signal  [P:1000]</TD></TR>
    <TR><TD>            DELAY</TD><TD>- The DELAY signal     [P:10]</TD></TR>
    <TR><TD>            INTERNAL</TD><TD>- The INTERNAL signal [P:500]</TD></TR>
    <TR><TD>&nbsp;</TD></TR>
    <TR><TD>    <B>hooks</B></TD><TD>- User hooks</TD></TR>
    <TR><TD>        delivery</TD><TD>- The delivery hooks.</TD></TR>
    <TR><TD>        mood</TD><TD>- The mood hooks (happy, sad, etc.)</TD></TR>
    <TR><TD>        nip</TD><TD>- NPC Interaction Protocol hook (interaction)</TD></TR>
    <TR><TD>        room-cleaning</TD><TD>- Room-cleaning hook.</TD></TR>
    <TR><TD>    <B>lib</B></TD><TD>- User libraries</TD></TR>
    <TR><TD>        anger</TD><TD>- NPC anger.</TD><TD><REQ>sig. MOOD</REQ></TD></TR>
    <TR><TD>        asking</TD><TD>- Ask NPC for/about ...</TD><TD></TD></TR>
    <TR><TD>        commanding</TD><TD>- Enable NPC heed orders</TD></TR>
    <TR><TD>        courier</TD><TD>- NPC courier system</TD><TD><REQ>sig. DELIVERY; libs. offers, presents</REQ></TR>
    <TR><TD>        delivery-area</TD><TD>- Delivery area.</TD><TD><REQ>sig. DELIVERY</REQ></TR>
    <TR><TD>        delivery-object</TD><TD>- Delivery object.</TD><TD><REQ>sig. DELIVERY</REQ></TR>
    <TR><TD>        eating</TD><TD>- NPC hunger/eating</TD><TD><REQ>lib. offers</REQ></TD><TD><SUPP>sig. MOOD</SUPP></TD></TR>
    <TR><TD>        emoting</TD><TD>- NPC parser usage</TD></TR>
    <TR><TD>        freemoting</TD><TD>- NPC free-emoting usage</TD></TR>
    <TR><TD>        guarding</TD><TD>- NPC guarding</TD></TR>
    <TR><TD>        happiness</TD><TD>- NPC happiness</TD><TD><REQ>sig. MOOD</REQ></TD></TR>
    <TR><TD>        interaction</TD><TD>- Interaction</TD><TD><REQ>lib. emoting</REQ></TD></TR>
    <TR><TD>        mounting</TD><TD>- (horse)backriding</TD></TR>
    <TR><TD>        mountrider</TD><TD>- inherit-base for riders</TD></TR>
    <TR><TD>        movement</TD><TD>- random room-movement</TD><TD></TD><TD><SUPP>lib. sleeping</SUPP></TD></TR>
    <TR><TD>        musician</TD><TD>- Musicians lib. Example, live on Marrach soon</TD></TR>
    <TR><TD>        offers</TD><TD>- NPC trading (receiving)</TD></TR>
    <TR><TD>        presents</TD><TD>- NPC trading (giving)</TD></TR>
    <TR><TD>        relations</TD><TD>- Relationship control</TD></TR>
    <TR><TD>        rumours</TD><TD>- Rumour system library</TD><TD><REQ>lib. asking</TD></TR>
    <TR><TD>        sadness</TD><TD>- NPC sadness</TD><TD><REQ>sig. MOOD</REQ></TD></TR>
    <TR><TD>        sleeping</TD><TD>- NPC sleepy/sleeping.</TD><TD></TD><TD><SUPP>sig. MOOD</SUPP></TD></TR>
    <TR><TD>        trash-taker</TD><TD>- Accepting trash feature</TD><TD></TD><TD><SUPP>hook room-cleaning</SUPP></TD></TR>
    <TR><TD>        <B>circus</B></TD><TD>- "Circus" example libs</TD></TR>
    <TR><TD>            kitten-basic</TD><TD>- Kitten tricks!</TD><TD></TD></TR>
    <TR><TD>    <B>signals</B></TD><TD>- User signals</TD></TR>
    <TR><TD>        DELIVERY</TD><TD>- The DELIVERY signal [P:60000]</TD></TR>
    <TR><TD>        MOOD</TD><TD>- The MOOD signal [P:100]</TD></TR>
    <TR><TD>&nbsp;</TD></TR>
    <TR><TD><ROOT>NIP</ROOT></TD><TD>- <ROOT>NIP objects/related things</ROOT></TD></TR>
    <TR><TD>    <B>bodies</B></TD><TD>- NIP NPC bodies</TD></TR>
    <TR><TD>    <B>code</B></TD><TD>- Code indirectly related to NIP</TD></TR>
    <TR><TD>    <B>items</B></TD><TD>- Items related to NIP...</TD></TR>
    <TR><TD>        scroll</TD><TD>- ...like scrolls.</TD></TR>
    <TR><TD>&nbsp;</TD></TR>
    <TR><TD><ROOT>Neoct:NIP</ROOT></TD><TD>- <ROOT>The neo-action NIP folder (parser commands)</ROOT></TD></TR>
    <TR><TD>    <B>Actions</B></TD><TD>- Action objects for system socials</TD></TR>
    <TR><TD>        +ask</TD><TD>- The +ask beta-ask action.</TD></TR>
    <TR><TD>        +ncs</TD><TD>- The +ncs action object</TD></TR>
    <TR><TD>        +nip</TD><TD>- The +nip action object</TD></TR>
    <TR><TD>    <B>Verbs</B></TD><TD>- Verb (social) objects</TD></TR>
    <TR><TD>        +ask</TD><TD>- The +ask beta-ask verb.</TD></TR>
    <TR><TD>        +ncs</TD><TD>- The +ncs verb object</TD></TR>
    <TR><TD>        +nip</TD><TD>- The +nip verb object</TD></TR>

    </TABLE>

\-- Main.KalleAlm - 15 Nov 2003
