# Codex Starter Prompt — LuxLink v0.1

You are implementing LuxLink, a mobile-first coordination platform for municipal animal shelters and the vetted communities that support them.

Read these files before changing code:
- /docs/product-spec.md
- /docs/engineering-spec.md
- /docs/user-flows.md
- /docs/acceptance-criteria.md

Important constraints:
1. Do not add features that are not in the spec.
2. Do not build a general shelter-management system.
3. Keep the app mobile-first.
4. Preserve the generic Need → Offer → Assignment workflow.
5. Use Next.js + TypeScript + Tailwind + Supabase.
6. Use Supabase row-level security.
7. PWA support is required, but native iOS/Android is not.
8. Push notification integration may be feature-flagged if external setup is not complete.
9. Prefer simple, maintainable implementation over abstractions.
10. Before coding, propose:
   - repository file structure
   - database migration plan
   - auth/role strategy
   - implementation order

FIRST IMPLEMENTATION TASK:
Build only the Foster Placement vertical slice end to end.

The slice must support:
- invited/vetted volunteer login
- coordinator login
- coordinator creates an animal
- coordinator creates a foster need
- volunteer sees the need in a mobile feed
- volunteer opens the need
- volunteer submits "I can help"
- coordinator sees the offer
- coordinator marks Contacted
- coordinator confirms the offer
- need becomes Covered
- volunteer receives an in-app confirmation
- coordinator is prompted to create a thank-you community post
- community post appears in the Community feed

Do not implement takeover, transport, adoption-hours, or general volunteer asks until this vertical slice is complete and passes the acceptance criteria.

Seed the database with:
Organization: Oakland Animal Services Pilot
Coordinator: Alex Coordinator
Volunteer: Jen Foster
Animal: Orchid
Need: Foster needed starting tomorrow
Animal status: stray_hold
Housing status: in_shelter

UI direction:
- warm, trustworthy, modern
- mobile-first
- simple status language
- large animal photos
- LuxLink dog mascot can appear in brand chrome
- no excessive gradients or decorative complexity
- status must never rely on color alone

After proposing the plan, wait for approval before writing code.
