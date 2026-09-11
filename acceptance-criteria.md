# LuxLink v0.1 — Acceptance Criteria

## Authentication / onboarding
- Invited user can create account.
- User is tied to one organization.
- Volunteer cannot access coordinator/admin routes.
- Coordinator cannot manage admin-only user permissions.
- Vetted status is visible to coordinator.

## Needs feed
- Volunteer sees open and offers-pending needs for own organization.
- Covered needs remain visible but clearly marked as covered.
- Need cards show type, timing, animal name (if applicable), and status.
- User can filter by Foster, Takeover, Transport, Adoption Hours, Volunteer.

## Foster specialization
- Volunteer profile can store specialization tags.
- Coordinator can view those tags on an offer.
- Medical/puppy foster needs can optionally target corresponding tagged volunteers.

## Offers
- Volunteer can submit exactly one active offer per need.
- Coordinator can view all offers for a need.
- Coordinator can mark offer Contacted.
- Coordinator can confirm one offer.
- Confirming offer automatically marks need Covered.
- Confirmed volunteer receives confirmation notification.

## Current foster requests
- Current foster can view animals assigned to them.
- Current foster can request takeover, transport, or adoption-hours support.
- Coordinator can review and publish/approve the request.

## Transport
- Transport need supports origin, destination, and time window.
- Volunteer can offer transport.
- Coordinator can confirm a transport offer.

## Adoption hours
- Adoption-hours request can capture pickup, event window, return needs, and notes.
- Volunteer can offer coverage.
- Coordinator can confirm coverage.

## Community
- Coordinator can create a community post.
- Community post may reference animal, need, and volunteer.
- After a need is covered, coordinator is prompted to create a thank-you post.
- Community feed is readable by volunteers and coordinators in the organization.

## Photos
- Coordinator can upload/take a photo when creating animal or need.
- Animal image is visible in need feed and detail page.
- Image upload works on mobile.

## Status
- Need statuses are visible as text, not color only.
- Need status can be changed by coordinator.
- Covered state is reflected immediately in volunteer view after confirmation.

## Mobile
- All MVP workflows work at 390px viewport width.
- Bottom navigation is thumb-friendly.
- No horizontal scrolling on primary screens.
- Create-need and offer flows are usable one-handed.

## Notifications
- User can opt in/out of alert types.
- Creating a need generates in-app notification records for eligible users.
- PWA push integration is behind a feature flag if platform setup is incomplete.
- App still functions if push is disabled.

## Security
- Row-level security prevents cross-organization access.
- Volunteer cannot modify another volunteer's profile or offers.
- Only coordinators/admins can confirm assignments.
