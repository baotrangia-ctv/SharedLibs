# Action Flow Checklist

Use this reference only when the module exposes user actions or public Manager methods.

Check:

- HUD calls `Request`, not `Process`
- `Request` always calls `Check`
- `Check` does not mutate state
- `Check` does not write persistence
- `Process` owns authoritative mutation
- `Process` owns persistence mutation or documented internal persistence methods
- Failure exits before side effects
- Public results expose success, failure reason, and enough information for display updates
- Cross-Manager calls use public APIs
- Database mutation remains Manager-owned
