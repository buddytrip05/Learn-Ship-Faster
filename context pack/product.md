# product.md

**Product:** Terraloom — project handoff and file management platform for architecture and construction firms.

**Core value prop:** Terraloom eliminates the version chaos and communication breakdowns that happen when projects move from design to build — so field teams always work from the current drawing, and project managers always know what changed and who approved it.

**Primary features:**
- **File handoff module** — structured workflow for publishing drawings and specs from design team to construction team, with version tracking and client publish gate
- **Task and milestone tracking** — project-level task assignment, status tracking, and dependency mapping across disciplines
- **Notification and activity feed** — real-time updates on file changes, task assignments, and approval requests
- **Admin and permissions management** — role-based access control, project membership, and firm-level user management
- **Mobile companion app** — field access to current drawings, task completion, and photo documentation (iOS and Android, currently limited feature set)
- **Reporting dashboard** — project health snapshots, overdue task counts, and file version history for project managers

**Current quarter focus (Q3):**
Engineering is focused on two areas: (1) File handoff v2 — improving the reliability of the publish-to-client step and adding email notification when a new drawing set is published; (2) Admin onboarding flow — rebuilding the new user invitation and permissions setup to reduce time from contract to first active user.

**Known pain points (be honest):**
- The publish-to-client step in file handoff has a 23% drop-off rate — users initiate it but don't complete it, usually because the approval step is confusing
- Notification volume is too high for most users — everything generates a notification and users are tuning out, which means they miss the important ones
- Mobile app is used by only 8% of weekly active users — field teams still default to emailing PDFs to themselves
- New admin setup takes an average of 4.5 hours across 3+ support touchpoints — it's our #1 support ticket category
- Notification preferences exist but only 12% of users have ever opened that settings page

**Tech constraints relevant to PM decisions:**
- Auth system is legacy and expensive to change — any feature touching user identity, SSO, or permissions requires a minimum 3-sprint lead time and senior eng involvement
- File storage and versioning layer is stable but not easily extensible — adding new file types or new version comparison features requires backend work that can't be parallelized
- Mobile app is a separate codebase (React Native) — features that exist in web do not automatically exist in mobile and vice versa; any mobile parity work requires a dedicated sprint
- Notification system is event-driven but not user-preference-aware — rebuilding it to support per-user preferences is a 6–8 week project on its own

**Open questions the team is actively debating:**
- Should notification preferences be rebuilt from scratch or patched to support basic mute/frequency controls? The patch is faster but creates tech debt.
- Is the mobile drop-off a feature gap problem or an awareness and adoption problem? (We don't have clear data yet.)
- Should file handoff v2 prioritize the approval UX or the publish notification flow first? Both are blocking adoption but we can't do both this quarter.
- How do we measure "successful handoff" for NRR purposes — is it the publish event, client download, or client acknowledgment?
