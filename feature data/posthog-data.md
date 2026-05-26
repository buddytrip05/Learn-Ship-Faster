# PostHog product analytics — July 1–8, 2025
**Exported by:** Data team  
**Date range:** Last 90 days (April 8 – July 8, 2025)  
**Cohort:** All active accounts (paid seats with at least 1 login in last 30 days)

---

## 1. Task dependency feature — funnel and behavior analysis

The task dependency feature shipped January 14, 2025. This is the first full-quarter usage analysis.

### Adoption funnel

| Step | Users who reached this step | % of active users |
|------|----------------------------|-------------------|
| Viewed dependency settings | 2,841 | 61% |
| Created at least 1 dependency | 1,203 | 26% |
| Created 3+ dependencies on a single project | 489 | 11% |
| Still using dependencies after 30 days | 201 | 4% |

**Observation:** Drop-off between "created at least 1" and "still using after 30 days" is severe — 83% of users who try dependencies abandon them within a month.

### Abandonment behavior

When users who created dependencies stop using the feature, what do they do next?

- **47%** delete all existing dependencies within 7 days of last use
- **31%** leave dependencies in place but stop creating new ones
- **22%** contact support or file a bug report (this cohort has a 6x higher support ticket rate than average)

### The silent corruption pattern — flagged July 3

Our data team identified an anomaly on July 3. Users who have created 3+ dependencies on a project show a statistically abnormal task deletion rate — **3.8x higher** than users without dependencies on equivalent projects.

Deeper analysis shows the deletions are not intentional:
- 94% of "deleted" tasks are deleted within 60 seconds of a parent task being marked complete
- Users who "delete" tasks this way have a significantly higher return rate to that project within 10 minutes (likely noticing the task is gone)
- Zero of these users have a "bulk delete" event in the same session — they are not intentionally cleaning up

**Our interpretation:** Marking a parent task complete is triggering dependent task deletion as a side effect. This is not documented behavior. Users are losing task data without knowing why or how to recover it.

### Scope of impact

- **201 active users** currently have 3+ dependencies set on at least one project
- Estimated **1,400–1,800 tasks silently deleted** in the last 90 days based on the pattern above
- **31 support tickets** referencing task disappearance in last 30 days (cross-referenced with ticket data)
- Zero users have been notified that this is a known issue

### Revenue exposure

- 11 of the 201 affected users are at accounts with renewal dates in the next 90 days
- 3 of those accounts are in the $80K–$200K ARR tier
- One account (Hargrove Partners, $180K ARR, renewal August 30) filed 4 tickets referencing this bug in the last 14 days

---

## 2. Mobile drawing sync — usage and failure rate analysis

### Mobile app session data

| Metric | Value |
|--------|-------|
| Mobile DAU / Web DAU ratio | 0.09 (9%) |
| Median session duration (mobile) | 2m 14s |
| Median session duration (web) | 18m 43s |
| Drawing opens per session (mobile) | 1.2 |
| Drawing opens per session (web) | 6.8 |
| Sessions ending within 30 seconds (mobile) | 34% |

Mobile sessions are short, shallow, and frequently abandoned. This is consistent with a population that opens the app, can't find what they need, and closes it.

### Drawing sync failure rate

Our event tracking logs a `drawing_sync_verified` event when a user opens a drawing and the version hash matches the latest published version. We log `drawing_sync_stale` when it does not match.

| Event | Last 7 days | Last 30 days |
|-------|-------------|--------------|
| `drawing_sync_verified` | 3,841 | 16,204 |
| `drawing_sync_stale` | 1,029 | 3,876 |
| Stale rate | **21%** | **19%** |

**1 in 5 drawing opens on mobile serves a version that is not the current published version.**

### Stale sync by platform and network

| Condition | Stale rate |
|-----------|-----------|
| iOS, WiFi | 8% |
| iOS, cellular | 24% |
| Android, WiFi | 14% |
| Android, cellular | 31% |
| Android, cellular, low signal (<2 bars) | 51% |

The stale rate is dramatically worse on cellular and Android. Our primary field user persona (construction superintendent) is almost exclusively on cellular, often in low-signal environments.

### Stale drawing consequence events

We do not directly track whether a stale drawing caused an on-site error, but we can track downstream behavior after a `drawing_sync_stale` event:

- **38%** of stale events are followed by the user opening the same drawing on web within 10 minutes (likely cross-checking)
- **19%** of stale events are followed by a support ticket within 24 hours
- **6%** of stale events are followed by account-level churn within 90 days (compared to 1.2% baseline churn rate)

---

## 3. Reporting and cross-project views — feature request signal

This is not a shipped feature — we are tracking proxy behaviors that indicate demand.

### Proxy behaviors tracked

| Behavior | 30-day count | Notes |
|----------|-------------|-------|
| Users who exported data from 3+ individual projects in same session | 312 | Likely building a manual cross-project view |
| Users who visited the "reports" tab (currently empty/placeholder) | 891 | 19% of active users clicked on a tab that has no content |
| Average number of browser tabs open during a project-switching session | 4.2 | Users are managing context across multiple browser tabs |
| Support tickets explicitly requesting cross-project reporting | 14 | Last 30 days |

### Account concentration

Cross-project export behavior is concentrated in larger accounts:

| Account size | % who exported from 3+ projects in one session |
|--------------|------------------------------------------------|
| 10–50 seats | 4% |
| 51–150 seats | 11% |
| 151–300 seats | 28% |
| 300+ seats | 44% |

Reporting demand scales directly with account size. Our enterprise tier (the tier we're trying to grow) shows the highest signal.

### Revenue concentration of requesters

- The 312 users who exported from 3+ projects represent **41 unique accounts**
- Those 41 accounts represent **$2.1M of our $4.8M ARR** (44%)
- 9 of those accounts are up for renewal in the next 120 days
- Average ARR of those 9 accounts: $94K

---

## 4. Summary — three signals in conflict

| Signal source | Feature / issue | Urgency | Revenue exposure |
|---------------|-----------------|---------|-----------------|
| Leadership memo | Cross-project reporting dashboard | 45-day renewal deadline (1 account, $340K ARR) | High but concentrated |
| Support tickets (dominant theme) | Mobile drawing sync — stale/incorrect versions served to field | Active safety incidents, 6 critical escalations in 7 days | Diffuse — affects all mid-market field users |
| PostHog (silent pattern) | Task dependency data corruption — tasks silently deleted on parent completion | Growing — 201 affected users, invisible to most | Medium — 3 renewal accounts at risk, bug is invisible so users don't know to complain yet |

**The tension the PM team needs to resolve:**  
Leadership is pushing a feature that affects 1 account loudly.  
Support tickets are screaming about a bug that affects field teams across the mid-market segment.  
PostHog is quietly showing a data integrity problem that most users don't even know they have yet — but will.
