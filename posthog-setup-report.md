<wizard-report>
# PostHog post-wizard report

The wizard has completed a deep integration of PostHog analytics into the Spotly/DevEvent Next.js App Router project.

## Summary of changes

- **`instrumentation-client.ts`** (new): Initializes PostHog client-side using the recommended Next.js 15.3+ approach. Includes error tracking (`capture_exceptions: true`), a reverse proxy host (`/ingest`), and debug mode in development.
- **`next.config.ts`** (updated): Added reverse proxy rewrites so PostHog requests route through `/ingest` to reduce tracking-blocker interference. Also set `skipTrailingSlashRedirect: true` as required by PostHog.
- **`components/ExploreBtn.tsx`** (updated): Added `posthog.capture('explore_events_clicked')` in the button's click handler to track when users engage with the hero CTA.
- **`components/EventCard.tsx`** (updated): Added `'use client'` directive and `posthog.capture('event_card_clicked', {...})` with rich properties (title, slug, location, date) to track which events users click on.
- **`.env.local`** (new): Created with `NEXT_PUBLIC_POSTHOG_PROJECT_TOKEN` and `NEXT_PUBLIC_POSTHOG_HOST` environment variables.

## Events instrumented

| Event Name | Description | File |
|---|---|---|
| `explore_events_clicked` | User clicks the "Explore Events" CTA button on the homepage hero | `components/ExploreBtn.tsx` |
| `event_card_clicked` | User clicks on an event card to view event details (includes title, slug, location, date as properties) | `components/EventCard.tsx` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- **Dashboard — Analytics basics**: https://us.posthog.com/project/350365/dashboard/1382004
- **Explore Events button clicks** (trend): https://us.posthog.com/project/350365/insights/7cll4Erk
- **Event card clicks** (trend): https://us.posthog.com/project/350365/insights/oHxAoByE
- **Explore to event click conversion funnel**: https://us.posthog.com/project/350365/insights/B65tNG7K
- **Most clicked events** (breakdown by event title): https://us.posthog.com/project/350365/insights/wluBDTVA

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.

</wizard-report>
