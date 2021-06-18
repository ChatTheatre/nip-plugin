%META:TOPICINFO{author=\"kallea\" date=\"1092848742\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>Signals; technical summary\</font\>

Signals are really just extended libraries. They have a few more
features and are expected to contain a signal identifier. In general,
signals are defined as signals by giving them an ALL-CAPS NAME.

That is, a signal for \"hunting\" should be called \"HUNTING\", not
\"hunting\" or \"Hunting\".

Again, be aware that all features available in libraries, are also
available to signals. Check out the [libraries; technical
summary](NIPSummaryLibraries) page for further information.

The following properties are available to all signals:

  ------------------- --------------------------------------------------- -----------------------------------------------------------------------------
  **Property-name**   **Property-type**                                   **Description**
  init:signals        (\[ \"*\<identifier\>\" : *numeric priority** \])   A list of signals that should be inherited, with preferred signal priority.
  ------------------- --------------------------------------------------- -----------------------------------------------------------------------------

\-- Main.KalleAlm - 25 Nov 2003
