# LuxLink v0.1 — Engineering Specification

## Recommended stack

- Frontend: Next.js (App Router) + TypeScript
- Styling: Tailwind CSS
- Backend: Supabase
- Database: Postgres (via Supabase)
- Auth: Supabase Auth
- File storage: Supabase Storage
- Hosting: Vercel
- Notifications: Web Push / PWA-friendly notification layer for v0.1
- Analytics: lightweight event tracking (can start with app events in database)

## Architectural principles

1. Mobile-first UI.
2. Keep operational objects simple and normalized.
3. Preserve independent dimensions:
   - animal status
   - housing status
   - active needs
4. All core workflows should be possible from a phone.
5. The Need object is generic enough to support multiple coordination workflows.
6. Community posts should be generated from real operational activity where possible.
7. Avoid building a full shelter-management system.

## Roles

Enum:
- admin
- coordinator
- volunteer

All volunteers in v0.1 are assumed to be vetted by the shelter before activation.

## Database schema

### organizations
- id uuid pk
- name text
- slug text unique
- created_at timestamptz

### profiles
- id uuid pk references auth.users
- organization_id uuid references organizations
- role enum(admin, coordinator, volunteer)
- full_name text
- email text
- phone text nullable
- city text nullable
- state text nullable
- latitude numeric nullable
- longitude numeric nullable
- vetted boolean default false
- available boolean default true
- created_at timestamptz
- updated_at timestamptz

### volunteer_preferences
- id uuid pk
- profile_id uuid unique references profiles
- can_foster boolean default false
- can_takeover boolean default false
- can_transport boolean default false
- can_adoption_hours boolean default false
- can_volunteer boolean default false
- medical_foster boolean default false
- puppy_foster boolean default false
- senior_foster boolean default false
- large_dog_foster boolean default false
- behavioral_foster boolean default false
- max_distance_miles integer nullable
- notes text nullable

### animals
- id uuid pk
- organization_id uuid references organizations
- name text
- primary_photo_url text nullable
- shelter_status enum(stray_hold, available, rescue_pending, other)
- housing_status enum(in_shelter, in_foster, temporary_foster, other)
- current_foster_id uuid nullable references profiles
- weight_lbs numeric nullable
- dog_friendly boolean nullable
- cat_friendly boolean nullable
- kid_friendly boolean nullable
- medical_notes text nullable
- behavior_notes text nullable
- active boolean default true
- created_at timestamptz
- updated_at timestamptz

### needs
- id uuid pk
- organization_id uuid references organizations
- animal_id uuid nullable references animals
- type enum(foster, takeover, transport, adoption_hours, volunteer)
- title text
- description text nullable
- status enum(open, offers_pending, covered, closed, cancelled)
- urgency enum(normal, urgent)
- start_at timestamptz nullable
- end_at timestamptz nullable
- origin_text text nullable
- destination_text text nullable
- created_by uuid references profiles
- confirmed_assignment_id uuid nullable
- created_at timestamptz
- updated_at timestamptz

### offers
- id uuid pk
- need_id uuid references needs
- volunteer_id uuid references profiles
- status enum(new, contacted, confirmed, declined, unavailable)
- availability_text text nullable
- notes text nullable
- created_at timestamptz
- updated_at timestamptz

### assignments
- id uuid pk
- need_id uuid unique references needs
- volunteer_id uuid references profiles
- confirmed_by uuid references profiles
- confirmed_at timestamptz
- notes text nullable

### community_posts
- id uuid pk
- organization_id uuid references organizations
- animal_id uuid nullable references animals
- need_id uuid nullable references needs
- author_id uuid references profiles
- featured_volunteer_id uuid nullable references profiles
- body text
- image_url text nullable
- post_type enum(thank_you, outcome, update, volunteer_recognition)
- created_at timestamptz

### notification_preferences
- id uuid pk
- profile_id uuid unique references profiles
- foster_alerts boolean default true
- takeover_alerts boolean default true
- transport_alerts boolean default true
- adoption_hours_alerts boolean default true
- volunteer_alerts boolean default true

### notifications
- id uuid pk
- profile_id uuid references profiles
- need_id uuid nullable references needs
- title text
- body text
- read_at timestamptz nullable
- created_at timestamptz

## Row-level security

Minimum policy expectations:

Volunteer:
- can read active animals in own organization
- can read open/pending/covered needs in own organization
- can create offers for own profile
- can read/update own offers
- can read community posts in own organization
- can update own profile/preferences
- can create takeover/adoption-hours/transport requests only for an animal currently assigned to them, if product decides this is enabled

Coordinator:
- all volunteer permissions
- can create/update animals in own organization
- can create/update/close needs in own organization
- can update offer status
- can create assignments
- can create community posts

Admin:
- all coordinator permissions
- can manage organization users/roles

## State transitions

Need:
- open -> offers_pending
- open -> covered
- offers_pending -> covered
- open -> cancelled
- offers_pending -> cancelled
- covered -> closed

Offer:
- new -> contacted
- new -> confirmed
- new -> declined
- new -> unavailable
- contacted -> confirmed
- contacted -> declined
- contacted -> unavailable

On offer confirmation:
1. create assignment
2. set offer.status = confirmed
3. set need.status = covered
4. set need.confirmed_assignment_id
5. optionally update animal.current_foster_id for foster/takeover
6. create notification for volunteer
7. prompt coordinator to create community thank-you post

## App routes

Public/auth:
- /login
- /invite/[token]

Volunteer:
- /needs
- /needs/[id]
- /community
- /my-fosters
- /profile

Coordinator:
- /coordinator/needs
- /coordinator/needs/new
- /coordinator/needs/[id]
- /coordinator/offers
- /coordinator/animals
- /coordinator/animals/[id]
- /coordinator/community
- /coordinator/more

Admin:
- /admin/users
- /admin/settings

## Component map

Core:
- MobileShell
- BottomNav
- NeedCard
- NeedStatusBadge
- AnimalCard
- AnimalPhoto
- OfferHelpSheet
- OfferStatusChip
- CoordinatorOfferList
- CreateNeedForm
- ConfirmAssignmentDialog
- CommunityPostCard
- PhotoCapture
- AvailabilityToggle
- SpecializationTags
- NotificationSettings

## Notification targeting rules (v0.1)

Foster:
- volunteer_preferences.can_foster = true
- profiles.available = true

Takeover:
- can_takeover = true
- available = true

Transport:
- can_transport = true
- available = true

Adoption hours:
- can_adoption_hours = true
- available = true

Volunteer:
- can_volunteer = true
- available = true

Specialization can narrow foster notifications:
- medical need -> medical_foster
- puppy need -> puppy_foster

Do not build a scoring system yet.

## Analytics events

- need_created
- need_viewed
- notification_sent
- notification_opened
- offer_submitted
- offer_contacted
- offer_confirmed
- need_covered
- takeover_requested
- transport_requested
- adoption_hours_requested
- volunteer_request_created
- community_post_created

## PWA requirements

- installable manifest
- mobile app icon
- service worker
- add-to-home-screen support
- notification permission flow
- responsive design
- support modern iOS/Android browsers

## Performance / UX

- first meaningful page render under 2.5s on mobile connection target
- large tap targets
- no desktop-only critical workflows
- create-need flow should take <60 seconds for a coordinator with photo already available
- offer-help flow should take <30 seconds

## Accessibility

- WCAG AA color contrast
- semantic labels
- keyboard navigability
- alt text for animal photos
- visible status labels not dependent on color alone
