# Product Spec

## 1. Product summary

Clean Out is a mobile-first community cleanup app for iOS, Android, and web. It gives local residents a public map where they can report dirty places, create scheduled cleanup routes, join nearby cleanups, and show visible before/after impact.

The app is not a council reporting system, a full social network, or an advanced GIS tool. The v1 product should stay focused on simple real-world action: find a local problem, organise or join a cleanup, and mark the result.

## 2. One-line description

This app lets local residents report dirty places and join scheduled cleanup routes so they can improve their area and meet good people through simple local action.

## 3. V1 locked decisions

- The app is mobile-first.
- The v1 audience is local adult residents; the product should not intentionally target minors in v1.
- Public map viewing does not require an account.
- Creating reports, creating cleanups, joining cleanups, uploading photos, resolving reports, completing cleanups, flagging content, and blocking users require an account.
- Reports are shown as map pins.
- Cleanups are shown as scheduled route lines.
- Cleanup routes are approximate and do not need official route precision.
- Join means lightweight RSVP.
- Participant count is shown; public attendee lists are not shown in v1.
- Public profiles are username-only.
- Only creators and admins can change key statuses such as resolving reports, cancelling cleanups, or completing cleanups.
- Report photos and cleanup before/after photos are creator-only in v1.
- Report photos and cleanup photos are separate in v1. Cleanup routes do not automatically link, merge, or resolve nearby reports.
- Web v1 is for viewing and sharing only.
- V1 does not include chat, comments, DMs, social feeds, council workflows, area polygons, automatic road snapping, or advanced GIS.

## 4. Target users

### Primary v1 users

- Local residents acting individually.
- Younger adults who want a low-pressure way to socialise while doing something useful.
- People who notice litter, fly-tipping, dumped rubbish, overflowing bins, dirty alleyways, or neglected public spaces.

### Secondary v1 users

- Informal local cleanup organisers.
- Small community volunteer groups.
- People who want to join occasional cleanups without joining a club, WhatsApp group, or Facebook group.

### Not target users for v1

- Councils.
- Waste contractors.
- Schools.
- Large charities.
- Corporate volunteering teams.
- Advanced environmental or GIS users.

## 5. Core problem

Local people often notice dirty streets, paths, roads, alleys, and public spaces, but there is no simple, visual, social way to turn that concern into action.

Existing options are fragmented. People may post in social media groups, message friends, complain to councils, or organise informally, but this does not create a clear public map of what needs cleaning, what is already planned, and what has been completed.

The app solves this by making cleanup activity visible, joinable, and easy to coordinate without requiring chat, complex group management, or official council workflows.

## 6. Core user action

The repeated user action is:

1. See or report a dirty place.
2. Create or join a scheduled cleanup route.
3. Attend the cleanup.
4. Upload before/after proof.
5. Mark the cleanup as completed.

The core loop should feel simple and positive:

> See a local problem → join or create a cleanup → meet people → clean the area → show the result → repeat.

## 7. V1 MVP scope

V1 should be a strict, mobile-first MVP. The goal is to prove that people will use a public map to report dirty places, create scheduled cleanup routes, join others, and show completed impact.

### Account and profile

- Sign up and log in.
- Username-only public profile.
- Public viewing without an account.
- Account required to create reports, create cleanups, join cleanups, upload photos, resolve reports, complete cleanups, flag content, or block users.
- Basic account settings.
- Delete account.

### Public map

- Map-based home screen.
- Reports shown as pins.
- Cleanups shown as coloured route lines.
- Map-first interface with lightweight sheets and overlays rather than heavy separate pages where possible.
- Tap a report pin to open a report detail sheet.
- Tap a cleanup line to open a cleanup detail sheet.
- Basic filters:
  - Reports.
  - Planned cleanups.
  - Completed cleanups.
- No live user location sharing.

### Reports

A report is a single map point showing something that needs cleaning.

V1 report features:

- Create a report at a location.
- Choose a report category.
- Add an optional photo.
- Add an optional short description.
- View report details.
- Mark own report as resolved.
- Admin can resolve or hide reports.
- Flag inappropriate reports.

V1 report categories should be simple:

- Litter.
- Fly-tipping.
- Dumped rubbish.
- Overflowing bin.
- Dirty alleyway.
- Broken glass or hazardous litter.
- Other.

V1 report statuses:

- Open.
- Resolved.
- Flagged / hidden.

Only the report creator or an admin can resolve a report.

### Cleanups

A cleanup is a scheduled public activity where someone says they are cleaning a road, path, street, alley, park route, or similar route at a specific time.

V1 cleanup features:

- Create a scheduled cleanup.
- Draw or define an approximate cleanup route as a line on the map.
- Add a title.
- Add a date and time.
- Add an optional meeting point.
- Add an optional short description.
- Add an optional before photo during creation or from the cleanup detail view.
- View cleanup details.
- Join a cleanup.
- Leave a cleanup.
- Show participant count.
- Cancel own cleanup.
- Mark own cleanup as completed.
- Add an optional after photo when completing the cleanup.
- Admin can hide, cancel, or moderate cleanups.

V1 cleanup statuses:

- Planned.
- Completed.
- Cancelled.
- Flagged / hidden.

Only the cleanup creator or an admin can cancel or complete a cleanup.

The cleanup route line is an approximate public intent, not an official boundary or survey-accurate route.

### Report-cleanup relationship

Reports and cleanups are separate objects in v1.

A cleanup route may visually pass near or through reported areas on the map, but this does not automatically link the cleanup to those reports, merge their photos, or resolve the reports.

Only the report creator or an admin can resolve a report. A future version may add report-cleanup linking after the core loop is proven.

### Before/after photos

Before/after photos are part of the core MVP because they show visible proof of impact.

V1 photo rules:

- Report creator can upload a report photo.
- Cleanup creator can upload before/after cleanup photos.
- Report photos are optional.
- Cleanup before/after photos are optional but encouraged.
- Photos can be flagged for moderation.
- Flagged photos can be hidden by an admin.

For v1, cleanup joiners should not upload photos unless this is deliberately added later after moderation is proven.

### Lightweight social interaction

The app should support real-world socialising without becoming a social network.

V1 should include:

- Username.
- Organiser username on cleanup detail pages.
- Join cleanup.
- Leave cleanup.
- Participant count.
- My Activity view for cleanups and reports linked to the current user.

V1 should not include chat, comments, DMs, followers, likes, full bios, or public social feeds.

### My Activity

Users should have a simple place to view their own activity.

V1 My Activity should include:

- Reports created by the user.
- Cleanups created by the user.
- Cleanups joined by the user.
- Completed cleanups created by the user.

### Moderation and trust

Because the app includes public user-generated content, public locations, usernames, and photos, basic trust and safety features are part of the MVP.

V1 should include:

- Report content.
- Report user.
- Block user.
- Basic admin moderation view.
- Hide flagged reports, cleanups, photos, or users.
- Community guidelines.
- Basic safety notice before creating or joining a cleanup.
- Public support/contact email.

### Web v1

The web app should be narrower than the mobile app.

V1 web should include:

- Public map viewing.
- View report details.
- View cleanup details.
- Shareable links for reports and cleanups.

Creating reports and cleanups should be mobile-first. Web creation is out of scope for v1.

## 8. Out of scope for v1

The following features are deliberately delayed to protect the MVP from feature creep.

### Social features out of scope

- Private chat.
- Group chat.
- Direct messages.
- Comments.
- Likes or reactions.
- Followers.
- Friend lists.
- Public activity feeds.
- User tagging.
- Leaderboards.
- Dating-style profiles.
- Public bios.
- Public attendee lists.
- Profile photos.

### Map and GIS features out of scope

- Radius circles.
- Polygon or area cleanups.
- Council boundaries.
- Ward/parish/neighbourhood boundaries.
- Automatic road or path snapping.
- Route optimisation.
- Heatmaps.
- Duplicate detection.
- Advanced geofencing.
- Advanced search and filtering.
- Survey-accurate map editing.

### Council and organisation features out of scope

- Council dashboard.
- Official case management.
- Waste collection requests.
- Contractor workflows.
- Charity accounts.
- Organisation accounts.
- Team permissions.
- Corporate volunteering.
- School-specific flows.
- Equipment inventory.
- Insurance documents.
- Risk assessment workflows.

### Notification features out of scope

- Chat notifications.
- Social engagement notifications.
- Nearby activity spam.
- Comment notifications.
- Like/reaction notifications.

A minimal reminder or cancellation notification may be considered later, but it should not expand the core MVP unless required for usability.

### Other out-of-scope features

- Payments.
- Rewards marketplace.
- Gamification beyond basic completed activity counts.
- Public API.
- Advanced analytics dashboards.
- Multi-language support unless required for the launch area.
- Automatic report-cleanup linking or automatic report resolution.

## 9. Key user flows

### 9.1 Create an account

1. User opens the app.
2. User can view the public map without signing in.
3. User chooses to create something, join something, upload a photo, flag content, or block a user.
4. App prompts the user to sign up or log in using a lightweight auth sheet.
5. User creates an account or logs in.
6. New user chooses a username.
7. User can now create reports, create cleanups, join cleanups, and manage their own activity.

### 9.2 View the map

1. User opens the app.
2. App shows the public map.
3. Reports appear as pins.
4. Planned cleanups appear as coloured route lines.
5. Completed cleanups appear as completed/muted route lines or can be filtered.
6. User taps a pin or line to open a detail sheet.
7. User can filter between reports, planned cleanups, and completed cleanups.
8. User can use the account entry point to log in or open their account sheet.

### 9.3 Create a report

1. Signed-in user taps the create action on the map.
2. User chooses “Report a dirty place”.
3. User confirms the location on the map.
4. User chooses a category.
5. User optionally adds a photo.
6. User optionally adds a short description.
7. User submits the report.
8. The report appears as a public pin with status “Open”.

A basic report should be possible in under 30 seconds.

### 9.4 Resolve a report

1. Report creator opens their report.
2. User taps “Mark resolved”.
3. Report status changes from “Open” to “Resolved”.
4. Resolved reports remain visible or muted depending on map filter behaviour.

Only the report creator or an admin can resolve a report.

### 9.5 Create a cleanup

1. Signed-in user taps the create action on the map.
2. User chooses “Create a cleanup route”.
3. User draws or defines an approximate route line on the map.
4. User adds a cleanup title.
5. User adds a date and time.
6. User optionally adds a meeting point.
7. User optionally adds a short description.
8. User optionally adds a before photo.
9. User publishes the cleanup.
10. The cleanup appears as a planned route line on the public map.

The route drawing experience should be simple and forgiving. It does not need road snapping or official route precision in v1.

### 9.6 Join a cleanup

1. User taps a planned cleanup route line.
2. App opens the cleanup detail sheet.
3. User views title, time, meeting point, organiser username, description, route, and participant count.
4. Signed-in user taps “Join”.
5. Participant count increases.
6. Cleanup appears in the user’s My Activity view.

Joining is a lightweight RSVP. It does not create chat, attendance tracking, organiser approval, or legal responsibility inside the app.

### 9.7 Leave a cleanup

1. User opens a cleanup they have joined.
2. User taps “Leave”.
3. Participant count decreases.
4. Cleanup is removed from the user’s joined cleanups list.

### 9.8 Upload before/after photos

1. Cleanup creator opens their cleanup.
2. Creator optionally uploads a before photo before or near the time of the cleanup.
3. Creator optionally uploads an after photo once the cleanup is done.
4. Photos appear on the cleanup detail page.
5. Other users can flag inappropriate photos.
6. Admin can hide flagged photos.

Before/after photos are important because they make the app feel alive and prove real-world impact.

### 9.9 Mark cleanup completed

1. Cleanup creator opens their cleanup.
2. Creator optionally uploads an after photo.
3. Creator taps “Mark completed”.
4. Cleanup status changes from “Planned” to “Completed”.
5. The route line changes visual state on the map.
6. The cleanup appears as completed impact proof.

Only the cleanup creator or an admin can mark a cleanup completed.

### 9.10 Cancel a cleanup

1. Cleanup creator opens their planned cleanup.
2. Creator taps “Cancel cleanup”.
3. Cleanup status changes to “Cancelled”.
4. Cancelled cleanups are hidden or muted on the public map.

Only the cleanup creator or an admin can cancel a cleanup.

### 9.11 Flag or block content/users

1. User opens a report, cleanup, photo, or user profile.
2. User taps “Report” or “Block”.
3. App records the moderation action.
4. Flagged content enters the admin moderation queue.
5. Admin can hide or restore content.

## 10. Main data objects

### User

Represents a registered account. A user can create reports, create cleanups, join cleanups, upload permitted photos, flag content, block users, and manage their own activity.

V1 public identity should be username-only.

### Report

Represents a single dirty place or problem spot on the map. A report is shown as a pin and can include category, location, optional photo, optional description, creator, status, and timestamps.

### Cleanup

Represents a scheduled cleanup activity. A cleanup is shown as a route line and includes title, route, date/time, organiser, optional meeting point, optional description, participant count, photos, status, and timestamps.

### Participation

Represents a user joining a cleanup. It connects a user to a cleanup and supports join/leave behaviour and participant counts.

### Photo

Represents an uploaded image. A photo may belong to a report or cleanup. Cleanup photos should support before/after type. Photos need moderation status because they are public user-generated content.

### Status

Represents the lifecycle state of reports, cleanups, photos, and moderation items.

Core v1 statuses include:

- Report: Open, Resolved, Flagged / Hidden.
- Cleanup: Planned, Completed, Cancelled, Flagged / Hidden.
- Photo: Visible, Flagged, Hidden.

### Location

Represents a geographic point or route geometry.

V1 location types:

- Report pin location.
- Cleanup route line.
- Optional cleanup meeting point.

### Moderation flag

Represents a user-submitted report about inappropriate content or behaviour. It should include the flagged object, reporting user, reason, status, and admin review outcome.

### Block

Represents one user blocking another user. Blocking should reduce unwanted interaction and support basic trust and safety requirements.

## 11. Success criteria

The MVP is working if it proves that people will use the map to create and join real cleanup activity, not just browse or complain.

### Primary success metric

- Completed cleanups with after photos.

This is the strongest signal because it proves real-world action and visible impact.

### Secondary success metrics

- Number of cleanup routes created.
- Number of users joining cleanups.
- Percentage of planned cleanups that become completed cleanups.
- Percentage of completed cleanups with after photos.
- Number of reports created.
- Number of reports resolved.
- Repeat cleanup creators.
- Repeat cleanup joiners.

### Qualitative success signs

- Users understand the map quickly.
- Users can create a report without confusion.
- Users can create a cleanup route without needing advanced map tools.
- Join feels lightweight and safe.
- The app feels like positive local action, not a complaints board.
- The map does not feel cluttered or overwhelming.

## 12. Risks and assumptions

### Product risks

- The app may become too broad if it tries to support reporting, social networking, council workflows, volunteering, and GIS tools at the same time.
- Reports may dominate the experience and make the app feel negative if cleanups are not created and completed.
- Users may expect council involvement if reports look too much like official civic issue reports.
- Before/after photos may be underused if uploading them feels like extra work.
- Automatic report-cleanup linking may be useful later, but adding it in v1 would create product, UX, and trust complexity.

### UX risks

- Drawing cleanup route lines on mobile may be harder than expected.
- The map may become cluttered if pins, lines, and completed activity are not visually prioritised.
- Users may not understand the difference between reports and cleanups.
- Users may not understand that cleanup route lines are approximate.
- Joining a cleanup may feel too vague if date, time, and meeting point are not clear.

### Trust and safety risks

- Public user-generated content creates moderation requirements from the start.
- Public meetups create safety concerns, especially if the app attracts younger users.
- Photos may contain inappropriate, identifying, or sensitive content.
- Fake reports, spam reports, or malicious cleanup events could damage trust.
- Hazardous waste, roads, private land, or unsafe locations may require clearer safety guidance later.
- Completion is self-reported by the cleanup creator and is not independently verified in v1.

### Technical risks

- Map provider choice may affect cost, performance, licensing, and cross-platform consistency.
- Route-line drawing needs to work well across iOS, Android, and web viewing.
- Photo uploads and storage need to be reliable and cost-controlled.
- Location data needs to be stored carefully and queried efficiently.
- Moderation/admin tooling must exist early enough to support public launch.
- Web and mobile map implementations may differ depending on the chosen map provider.

### Adoption risks

- A broad launch may create an empty-map problem. V1 should ideally launch in a focused local area where reports and cleanups can appear quickly.
- The assumption that younger adults want to socialise through cleanup activity needs validation.
- Users may prefer existing WhatsApp, Facebook, or community groups unless Clean Out makes discovery and joining much easier.
- Local network effects are important: the product becomes more useful only when enough nearby reports and cleanups exist.

## 13. Open questions

These questions should be answered before final UX design, architecture planning, or implementation tickets are finalised.

### 1. What is the first launch area?

The app may technically support any location, but the first launch should probably focus on one town, city area, campus, or neighbourhood to avoid an empty map.

### 2. Which map provider should be used?

Google Maps or a similar provider can supply the base map, roads, paths, pins, and route-line display. The app still needs its own data layer for users, reports, cleanups, photos, statuses, joins, and moderation.

The final provider choice should consider cost, licensing, Expo/React Native support, web support, performance, and design quality.

### 3. Does v1 need maximum group sizes?

V1 currently assumes no maximum group size. This may need to change if small social cleanups need limits for safety, comfort, or organiser control.

### 4. Are basic cleanup reminders needed in v1?

The MVP does not require a full notification system. It is still open whether joined users need basic reminders or cancellation notices in v1.

### 5. How should hazardous or unsafe reports be handled?

V1 includes only basic safety notices and simple categories. It is still open whether hazardous waste, roadside danger, private land, or other unsafe situations need a separate flow, warning, or restricted cleanup creation.

### 6. What is the minimum admin moderation workflow?

V1 needs basic moderation, but the exact admin workflow still needs definition:

- What can be flagged?
- What reasons can users choose?
- What does an admin see?
- What actions can an admin take?
- What happens to repeat offenders?
- When is content automatically hidden?

### 7. How much profile information is allowed later?

V1 should use username-only profiles. It is still open whether profile photos, short bios, or social links should ever be added later. They should not be included in v1.
