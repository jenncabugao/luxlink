# LuxLink v0.1 — Product Requirements Document

## Product summary

LuxLink is a mobile-first coordination platform for municipal animal shelters and the communities that support them.

The initial wedge is not foster recruitment. It is activating an existing, vetted community faster and more clearly when animals need foster placement, temporary takeover coverage, transport, adoption-hours support, or other volunteer help.

LuxLink is built around the idea that better outcomes for shelter animals are made possible by communities that foster, transport, volunteer, donate, and care.

## Problem

Municipal shelters such as Oakland Animal Services can already have large, active foster communities. The coordination problem is fragmented:

- Foster and volunteer asks are posted in social/community channels and internal tools.
- People respond in comments, direct messages, email, text, and foster phone lines.
- Coordinators must interpret free-form offers, determine fit, follow up manually, and track whether a need is actually covered.
- Status updates can be missed, so community members may continue asking whether an animal still needs help.
- Vetted fosters often need to proactively check for requests instead of being alerted when a relevant need arises.
- The community and recognition loop is valuable and should be preserved rather than removed.

## Product hypothesis

If municipal shelters can send timely, targeted mobile alerts to vetted community members and convert responses into structured offers and assignments, then animals can receive support faster while coordinators spend less time manually piecing together comments, messages, and status updates.

## Goals

Primary:
- Reduce time from need creation to confirmed coverage.

Secondary:
- Reduce coordinator administrative burden.
- Reduce uncertainty about whether a need is still open.
- Preserve and strengthen the social/community recognition loop.
- Give vetted fosters and volunteers a useful mobile experience without requiring constant proactive checking.
- Make coordinator workflows usable from a phone.

## Non-goals for v0.1

- Adoption application processing
- Public adoption marketplace
- Medical records
- Animal control case management
- Boarding
- Rescue CRM
- Donation processing
- Public foster vetting / applications
- Background checks
- Full social network replacement
- Full shelter management system
- SMS
- Multi-leg transport routing
- AI matching

## Users

### Shelter Admin
Manages access, roles, organization settings, and program-level visibility.

### Foster Coordinator
Creates and updates animal needs, reviews offers, contacts community members, confirms assignments, closes needs, and publishes community thank-yous.

### Vetted Foster / Volunteer
Already approved by the municipal shelter. Can receive alerts, respond to needs, transport, cover adoption hours, provide temporary takeover coverage, and volunteer for community support needs.

A foster can also be a current foster who needs help with an animal already in their care.

## Core concepts

### Animal
Represents the shelter animal.

Key dimensions are independent:
- Shelter status: stray hold, available, rescue pending, other
- Housing status: in shelter, in foster, temporary foster
- Current needs: zero or more active needs

### Need
The central coordination object.

Lifecycle:
Open → Offers Pending → Covered → Closed/Cancelled

v0.1 need types:
- foster
- takeover
- transport
- adoption_hours
- volunteer

Volunteer requests may include:
- community clinic support
- bagging dog food
- other shelter support

### Offer
A vetted community member's structured response to a need.

Lifecycle:
New → Contacted → Confirmed
Optional terminal states:
Declined / Unavailable

### Assignment
Represents a confirmed person responsible for a need.

### Community Update
A lightweight recognition/update post, ideally generated from operational activity.

Examples:
- "Orchid is covered — thank you, Jen!"
- "Buddy made it to Sacramento — thank you, Alex!"
- "Thank you to everyone who helped at today's community clinic."

## Foster / volunteer profile

Core fields:
- name
- email
- phone
- shelter affiliation
- vetted status
- approximate location
- currently available / unavailable
- willing to foster
- willing to provide takeover coverage
- willing to transport
- willing to cover adoption hours
- willing to volunteer

Specialization tags:
- medical foster
- puppies
- seniors
- large dogs
- behavioral experience

Foster duration is flexible and should be expressed per offer/request rather than as a fixed category. It can range from one night to several weeks.

## Mobile navigation

### Foster / Volunteer
- Needs
- Community
- My Fosters
- Profile

### Coordinator
- Needs
- Offers
- Community
- Animals
- More

## Core mobile flows

### 1. Foster placement
Coordinator creates foster need → relevant vetted fosters are notified → foster opens request → foster offers help → coordinator reviews → coordinator confirms → need becomes Covered → optional thank-you post is generated.

### 2. Temporary takeover
Current foster requests coverage or coordinator creates on their behalf → vetted users are alerted → user offers coverage → coordinator confirms → takeover becomes Covered.

### 3. Transport
Coordinator creates origin, destination, date/time window → relevant volunteers are alerted → volunteer offers/claims → coordinator confirms.

### 4. Adoption-hours coverage
Current foster cannot bring the dog to adoption hours → coordinator or current foster creates request → volunteer offers to pick up / host dog during adoption hours / return dog → coordinator confirms.

### 5. Community volunteer ask
Coordinator posts a non-animal-specific ask such as clinic help or bagging dog food → relevant volunteers are alerted → volunteers respond → coordinator confirms / closes.

## Community product pillar

The community is not incidental. It is part of why the model works.

LuxLink should include a lightweight community recognition feed that:
- celebrates successful coverage
- tags / credits the person who helped
- includes photos
- makes positive outcomes visible
- reinforces participation

v0.1 should not become a general social network. Recognition posts should be tied to shelter/community activity.

## Photos

Mobile photo capture is a first-class requirement.

Coordinator must be able to:
- take a photo from phone camera
- upload from camera roll
- attach photos while creating or updating an animal need

Usability target:
A coordinator should be able to create an urgent request from a phone in under 60 seconds.

## Notifications

Notifications are a core feature.

Examples:
- "Urgent foster needed: Orchid can leave OAS today."
- "Weekend takeover needed: Miley needs coverage Fri–Sun."
- "Transport needed tonight: OAS → SF after 5 PM."
- "Volunteer help needed: Community clinic Saturday morning."

Notification targeting may use simple rule-based filtering in v0.1:
- role / capability
- specialization tags
- availability
- distance (if practical)

## Success metrics

Primary:
- Median time from need created → confirmed assignment
- Median time from need created → first qualified offer
- Coverage rate (% of needs that become covered)

Secondary:
- Alert → offer conversion
- % of open needs with at least one qualified response
- Number of takeover requests successfully covered
- Number of transport requests successfully covered
- Coordinator touches per confirmed assignment
- % of community updates generated after successful assignment
- % of users who respond to at least one alert

## Mission principle

LuxLink should reduce burden on resource-constrained municipal shelters, not create another financial or administrative burden.

v0.1 is designed around municipal shelters and their vetted communities.
