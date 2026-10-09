# Backend

.NET 11. SQLite. Entity Framework Core. One service process.

Users, organizations, memberships, devices, pairing records, sessions, repositories. Personal is an organization of one. Session rows do not hold transcript bodies.

| Project | Role |
| --- | --- |
| `Api/AppHost` | Aspire host, local only. Not the first cut. |
| `Api/Services/Relay` | Switchboard. WebTransport via NuGet. |
| `Api/Libraries/Rig.Data` | EF model and migrations. |
| `Api/Tests` | TUnit. Membership rules first. |

The backend is not the credential store, the git host, or a queue for sleeping hosts.
