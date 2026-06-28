# Design System

## 1. Product experience principles

Clean Out should feel calm, fast, useful, and quietly premium. The app should make local cleanup activity feel easy to understand and easy to join, without feeling like a council form, a complaints board, or a social network.

The core experience should be:

- **Map-first**: the map is the product’s centre of gravity.
- **Action-led**: users should always understand the next useful action: report, create, join, complete.
- **Lightweight social**: the app should help people meet through real-world cleanups, not through chat, feeds, or profiles.
- **Positive and practical**: the product should focus on action and visible impact, not just problems.
- **Clean and high-end**: the UI should use space, restraint, and clear hierarchy rather than busy panels or gamified clutter.
- **Trustworthy**: public user-generated content should feel moderated, safe, and structured.
- **Mobile-first**: v1 should feel excellent on iOS and Android before expanding web functionality.

The app should feel like:

> “I can quickly see what needs cleaning nearby, join something useful, and help improve my area.”

It should not feel like:

> “I am filing a formal civic complaint.”

or:

> “I am joining another social media platform.”

---

## 2. Core user loop

The main repeated journey is:

1. User opens the map.
2. User sees reports as pins and cleanups as route lines.
3. User reports a dirty place, creates a cleanup, or joins an existing cleanup.
4. A scheduled cleanup happens in the real world.
5. The cleanup creator uploads before/after proof.
6. The cleanup creator marks the cleanup as completed.
7. The map shows visible local impact.

The emotional loop is:

> See a local problem → join or create a cleanup → meet people → clean the area → show the result → repeat.

The UI should support this loop without adding unnecessary social mechanics. Users should not need chat, comments, full profiles, or complex group management to understand what is happening.

---

## 3. Map mental model

The map is the home screen and the main product surface. It should remain visible behind most creation and detail interactions.

### Core map objects

There are two public map object types in v1:

1. **Reports**
   - Shown as pins.
   - Represent single dirty places or problem spots.
   - Examples: litter, fly-tipping, dumped rubbish, overflowing bins, dirty alleyways.

2. **Cleanups**
   - Shown as route lines.
   - Represent scheduled cleanup activity.
   - Examples: cleaning part of a road, a footpath, a street stretch, an alley, or a route through a park.

### Reports as pins

Report pins should feel like clear points of attention, not emergency alarms.

Report pins should show:

- A simple pin shape.
- A category or status cue where possible.
- A selected state when tapped.
- A muted state for resolved reports if visible.

Report pins should not feel like official council case markers.

### Cleanups as routes/segments

Cleanup routes should appear as clean coloured lines on the map.

A cleanup route may technically be made of multiple points and line segments, but the user should experience it as one route. V1 should not expose advanced route editing, road snapping, or segment management.

Cleanup route lines should show:

- Planned state.
- Completed state.
- Selected state.
- Hidden/muted treatment for cancelled or unavailable items.

Route lines are approximate. They represent public intent, not official boundaries or survey-accurate paths.

### Statuses on the map

Statuses should be visually clear but not noisy.

Reports:

- **Open**: visible pin.
- **Resolved**: muted pin or hidden by filter depending on map settings.
- **Flagged / hidden**: not visible to normal users.

Cleanups:

- **Planned**: clear route line.
- **Completed**: calmer completed-state route line.
- **Cancelled**: hidden or muted.
- **Flagged / hidden**: not visible to normal users.

### Bottom sheets

Tapping a pin or route should open a bottom sheet over the map.

Bottom sheets should:

- Preserve map context.
- Show the most important information first.
- Avoid looking like long forms.
- Use clear primary actions.
- Allow quick dismissal back to the map.

Report and cleanup details should not feel like separate unrelated pages on mobile unless there is a strong reason.

### Report-cleanup relationship

Reports and cleanups are separate objects in v1.

A cleanup route may visually pass near or through areas with existing reports, but the app should not automatically:

- Link the cleanup to those reports.
- Merge report photos with cleanup photos.
- Resolve nearby reports.
- Notify report creators that their report has been addressed.

This keeps v1 simple and avoids false claims about what was cleaned.

---

## 4. Report and cleanup mental model

### Report

A report means:

> “This place needs cleaning.”

A report is quick, lightweight, and location-specific.

A report should answer:

- Where is the problem?
- What type of problem is it?
- Is there a photo or short description?
- Is it open or resolved?

A report should not feel like a formal complaint, case file, or council ticket.

### Cleanup

A cleanup means:

> “Someone is cleaning this route at this time.”

A cleanup is more active than a report. It is scheduled, joinable, and connected to real-world action.

A cleanup should answer:

- What route is being cleaned?
- When is it happening?
- Where should people meet, if a meeting point is added?
- Who organised it?
- How many people have joined?
- Has it been completed?
- Are there before/after photos?

### Joining a cleanup

Joining a cleanup means:

> “I intend to attend.”

Joining is a lightweight RSVP. It should not imply:

- Chat access.
- Attendance tracking.
- Organiser approval.
- Legal responsibility inside the app.
- Public attendee listing.

The UI should show participant count, not public attendee lists.

### Completing a cleanup

Completing a cleanup means:

> “The cleanup creator says this cleanup has happened.”

Completion is creator/admin controlled in v1. It is not independently verified.

The completion experience should encourage an after photo, but should not make after photos mandatory unless the product spec changes later.

---

## 5. Navigation and interaction rules

### Main navigation rule

Use this hierarchy:

1. **Map first.**
2. **Overlays and sheets second.**
3. **Full pages only when necessary.**

The main map should feel persistent. Users should rarely feel thrown away from the map unless they intentionally open My Activity, Settings, or a web detail page.

### Main mobile layout

The main map should include:

- Full-screen map.
- Floating create action in a corner or accessible bottom area.
- Account/login entry in a top corner or top bar.
- Simple filters for map layers.
- Bottom sheets for selected reports and cleanups.

### Create action

The create action should open a sheet over the map with two choices:

- Report a dirty place.
- Create a cleanup route.

The create action should not open a complex dashboard or multi-feature menu.

### Account/login entry

Logged-out state:

- Show a small “Log in” entry or account icon.
- Do not force login on app launch.

Logged-in state:

- Show username or a simple account icon.
- Tapping opens an account sheet with username, My Activity, Settings, guidelines, support/contact, and logout.

### Auth interaction

Auth should appear as a lightweight sheet or modal when a user tries to perform a restricted action.

The app should already know whether the user is signed in or signed out from the current session. Normal flows should not show unnecessary “checking auth” loading states.

### Creation interactions

Report creation should happen over the map:

- Confirm pin location.
- Choose category.
- Add optional photo.
- Add optional description.
- Submit.

Cleanup creation should happen over the map:

- Define approximate route line.
- Add title.
- Add date/time.
- Add optional meeting point.
- Add optional description.
- Add optional before photo.
- Publish.

### Detail interactions

Report and cleanup details should open as bottom sheets.

Actions should be contextual:

- Open report: mark resolved only if creator/admin.
- Planned cleanup: join if eligible.
- Joined cleanup: leave.
- Created cleanup: add photos, cancel, complete.
- Any visible public content: flag if signed in.

### Web interaction

Web v1 should be for viewing and sharing only.

Web should not introduce full creation, joining, or account-heavy flows unless the product spec changes.

---

## 6. Visual identity

### Overall direction

The visual identity should feel:

- Clean.
- Fresh.
- Calm.
- Civic but not bureaucratic.
- Social but not noisy.
- Premium without feeling cold.

The product should feel more like a polished local action tool than a government portal or volunteer database.

### Colour direction

Use a restrained palette.

Recommended colour roles:

- **Neutral base**: warm off-white, soft grey, charcoal text.
- **Primary action**: clean green or fresh teal.
- **Reports**: warm amber/orange or similar attention colour that does not feel like emergency red.
- **Planned cleanups**: confident green/teal route line.
- **Completed cleanups**: softer green/sage or muted success treatment.
- **Cancelled/unavailable**: neutral grey.
- **Errors/destructive actions**: restrained red only where needed.

Avoid a rainbow map. Reports, cleanups, statuses, and actions should be easy to distinguish but visually calm.

### Typography direction

Typography should be simple, modern, and highly readable.

Use:

- Clear title styles for sheet headers and major actions.
- Comfortable body text for descriptions and safety copy.
- Small but readable metadata text for dates, status, participant count, and usernames.
- Strong but not shouty button labels.

Avoid overly playful, novelty, or government-style typography.

### Spacing

Spacing should create calm and confidence.

Use:

- Generous padding inside cards and sheets.
- Clear separation between primary actions and secondary actions.
- Enough vertical space for forms to feel easy on mobile.
- Compact metadata areas that do not crowd the main content.

Avoid dense civic-dashboard layouts.

### Shape

Use soft, modern shapes:

- Rounded bottom sheets.
- Rounded cards.
- Rounded buttons.
- Clear but simple map markers.

Shapes should feel friendly and premium, not cartoonish.

### Elevation

Use elevation sparingly:

- Bottom sheets should sit clearly above the map.
- Floating controls should be visible but not heavy.
- Cards should separate from the background without strong shadows.

Avoid stacked layers that make the UI feel cluttered.

### Tone of voice

The copy should be:

- Direct.
- Encouraging.
- Calm.
- Non-judgemental.
- Action-focused.

Good tone:

- “Create a cleanup route.”
- “Join this cleanup.”
- “No activity here yet.”
- “Add an after photo to show the impact.”

Avoid:

- Legal-heavy language in normal UI.
- Gamified hype.
- Shame-based messaging.
- Bureaucratic terms like “case submitted” or “incident reference”.

---

## 7. Core components

### Buttons

Button types:

- **Primary button**: main action on a sheet or form, such as Submit report, Publish cleanup, Join cleanup, Mark completed.
- **Secondary button**: lower-priority action, such as Cancel, Back, Continue browsing.
- **Destructive button**: actions such as Cancel cleanup, Delete account, or Block user.
- **Icon button**: compact actions on the map, account entry, close sheet, filter control.
- **Floating create button**: persistent map entry point for creating a report or cleanup.

Rules:

- Each sheet should have one obvious primary action.
- Do not show multiple competing primary buttons.
- Destructive actions should require clear intent.
- Disabled buttons should explain what is missing where appropriate.

### Inputs

Input types:

- Text input for title and short description.
- Category selector for report categories.
- Date/time selector for scheduled cleanups.
- Optional meeting point selector.
- Username input.

Rules:

- Keep forms short.
- Mark required fields clearly through context, not visual clutter.
- Preserve input after upload or submission errors.
- Do not make optional fields feel required.

### Cards

Cards should be used for:

- Selected report summary.
- Selected cleanup summary.
- My Activity list items.
- Admin moderation previews.

Card rules:

- Show the object type clearly.
- Show status visibly but calmly.
- Prioritise the next action.
- Avoid overloading cards with every field.

### Bottom sheets

Bottom sheets are the main mobile detail surface.

Bottom sheet rules:

- Start with the most important information.
- Keep the map visible behind the sheet.
- Support quick dismissal.
- Use clear scroll behaviour for longer content.
- Place the primary action in a predictable position.

### Map markers

Report pins:

- Use a clear pin shape.
- Use status/category cues carefully.
- Show selected state when tapped.
- Keep resolved reports visually muted if visible.

Cleanup route lines:

- Use clear line weight.
- Make selected routes visually distinct.
- Make completed routes calmer than planned routes.
- Do not use radius circles for cleanup areas.
- Do not use polygon boundaries in v1.

### Report cards

Report cards/sheets should include:

- Category.
- Status.
- Optional photo.
- Optional description.
- Created date.
- Creator username where appropriate.
- Mark resolved action for creator/admin.
- Flag/block actions where permitted.

Report cards should not look like official council case files.

### Cleanup cards

Cleanup cards/sheets should include:

- Title.
- Status.
- Date/time.
- Route preview or visible route context.
- Optional meeting point.
- Optional description.
- Organiser username.
- Participant count.
- Before/after photos where available.
- Join/leave action where eligible.
- Creator/admin controls where permitted.

Cleanup cards should make the event feel real, scheduled, and easy to understand.

### Status chips

Status chips should be short and clear.

Report status chips:

- Open.
- Resolved.
- Hidden, where relevant to admin.

Cleanup status chips:

- Planned.
- Completed.
- Cancelled.
- Hidden, where relevant to admin.

Photo status chips, where needed:

- Visible.
- Flagged.
- Hidden.

Rules:

- Do not overuse chips.
- Use chips to clarify state, not decorate the UI.
- Hidden/flagged states should mainly appear in admin or creator contexts.

### Photo upload components

Photo upload should be a reusable component or sheet, used in:

- Report creation.
- Cleanup creation for optional before photo.
- Cleanup detail/completion for optional before/after photos.

Rules:

- Show selected photo preview.
- Allow replace/remove before submission.
- Show upload progress when needed.
- Allow retry on upload failure.
- Make photos optional in v1.
- Keep report photos and cleanup photos separate.

### Account/login entry points

Account entry should be simple and unobtrusive.

Logged out:

- Show “Log in” or an account icon.
- Opening it shows Auth Sheet.

Logged in:

- Show username or account icon.
- Opening it shows Account Sheet.

Account Sheet should include:

- Username.
- My Activity.
- Settings.
- Community guidelines.
- Support/contact.
- Log out.

Avoid full social profiles in v1.

---

## 8. Screen state rules

### Empty states

Empty states should be short, calm, and useful.

Rules:

- Keep the map visible where possible.
- Do not make an empty area feel like failure.
- Offer a relevant next action when appropriate.
- Avoid long explanations.

Examples of direction:

- No local activity: explain that nothing is visible here yet and offer report/create actions.
- No My Activity: encourage the user to create a report or join/create a cleanup.
- Missing optional content: omit the section rather than showing heavy placeholders.

Detailed empty-state copy can be refined during visual design.

### Loading states

Loading should feel fast and local.

Rules:

- Load the map first, then pins/routes.
- Use compact skeletons or loading rows for lists and sheets.
- Disable duplicate submit buttons while saving.
- Preserve user input during uploads and submissions.
- Avoid visible auth-check loading during normal flows.

### Error states

Errors should be plain-language and recoverable.

Rules:

- Tell the user what failed.
- Preserve entered information where possible.
- Offer retry for network, upload, or save failures.
- Return safely to the map if an item is unavailable.
- Do not expose technical error messages.

Common error patterns:

- Map failed to load: full-screen retry.
- Map data failed: keep map visible and retry map objects.
- Item unavailable/hidden: show unavailable message and return to map.
- Upload failed: retry or continue without optional photo where allowed.
- Submission failed: preserve form and retry.

### Success states

Success should be clear but not loud.

Rules:

- After creating a report, return to the map with the new pin visible or selected.
- After creating a cleanup, return to the map with the new route visible or selected.
- After joining a cleanup, update the button state and participant count.
- After completing a cleanup, update the route to completed state.
- Use subtle confirmation feedback rather than large celebration screens.

---

## 9. Accessibility rules

### Readability

- Text should be large enough to read comfortably on mobile.
- Avoid long paragraphs in sheets.
- Use clear headings and short labels.
- Metadata should remain readable, not tiny.

### Touch targets

- Primary actions, map controls, close buttons, and account/create buttons should be easy to tap.
- Avoid placing small controls too close together on the map.
- Bottom sheet actions should be reachable on one-handed mobile use where possible.

### Contrast

- Text must have strong contrast against cards, sheets, and map overlays.
- Map pins and route lines must remain visible against varied map backgrounds.
- Do not rely on colour alone to communicate status.
- Selected states should use shape, weight, label, or elevation as well as colour.

### Motion and interaction

- Sheet animations should be smooth and quick.
- Avoid excessive motion or playful animation.
- Do not make critical actions depend on precise gestures.
- Route creation should be forgiving and should support correction where possible.

### Mobile usability

- Forms should avoid unnecessary typing.
- Category selection should be quick.
- Date/time selection should be clear.
- Photo upload should work comfortably from camera or library.
- Error messages should appear near the relevant action or field.

---

## 10. What not to do

Do not design v1 as:

- A council reporting portal.
- A full social network.
- A chat app.
- A volunteering marketplace.
- An advanced GIS/map editing tool.
- A gamified leaderboard product.

Avoid these v1 design choices:

- Full-screen onboarding carousel before the map.
- Forced sign-up on app open.
- Heavy profile screens.
- Profile photos or public bios.
- Public attendee lists.
- Comments, likes, DMs, or feeds.
- Radius circles for cleanup areas.
- Polygon/area cleanup drawing.
- Automatic road snapping.
- Automatic report-cleanup linking.
- Automatic report resolution when a cleanup is completed.
- Busy map layers with too many colours.
- Dense admin/civic-dashboard UI for normal users.
- Overly playful gamification.
- Alarmist red-heavy visuals for normal reports.
- Long forms for simple reports.
- Complex safety/risk workflows in the core v1 user journey.

The v1 design should stay focused on the simplest useful experience:

> Open the map, understand local cleanup activity, report a problem, create or join a scheduled route, and show the impact.
