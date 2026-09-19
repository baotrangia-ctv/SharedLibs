# Request–Check–Process review

The current public Manager surface is read/query oriented:

- `RequestLeaderboard` validates the type, loads/caches read-only score rows, and
  returns state plus current-player details.
- It performs no persistent mutation and has no `Process` phase.
- `ReloadLeaderboard` and `SetMockState` mutate only temporary mock/cache state for
  state testing; they do not grant rewards or write persistence.

Therefore the full mutation-oriented Request → Check → Process split is not
applicable. When real score publishing is added, it must use a separate Request →
Check → Process flow rather than adding writes to `RequestLeaderboard`.
