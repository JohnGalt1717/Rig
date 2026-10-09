# Problems

The problems panel is the diagnostics contract. Analyze, build, and test all write rows into it. A row is severity, file, range, code, message, and the tool that produced it. The user sees the row as it arrives. The agent reads the same row.

Analyze stays resident. A file change through the proxy invalidates that file and the analyzer pushes. Roslyn is the C# case: problems without a rebuild. Other languages use the watcher that language already ships. Starting a linter per edit is a pack bug.

Build is a separate tool. Its errors parse into the same panel, tagged as build. A language pack owns the parser. The agent does not scrape stdout.

The panel is what the stop hook returns. The agent does not shell out to see if the file is clean.
