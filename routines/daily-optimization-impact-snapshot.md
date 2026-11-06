# Daily optimization-impact snapshot (disabled recipe)

This is documentation only. Importing the pack or loading `usage-optimization-impact-report` does **not** enable this schedule. Each usage read itself consumes usage.

- Suggested cadence: once daily in the evening of the adopting owner's confirmed timezone, flexible.
- Enablement requires an explicit owner yes.

Prompt intent:

If the owner enabled a daily optimization-impact snapshot, take at most one usage snapshot through supported tools and update the existing impact report page using usage-optimization-impact-report. Append no invented savings. Record only observed usage with source, period and denominators. Update rows whose comparable window is now available. If nothing new can be recorded and no snapshot was authorized for this run, end without an extra usage read.
Deliver a short owner notice only when a new intervention was recorded that day or a comparison became available; otherwise stay silent.
