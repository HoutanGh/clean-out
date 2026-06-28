# Screen Flows

## 1. Purpose

This document translates `docs/product-spec.md` into simple v1 screens, sheets, and map overlays. It is intended for UX design, architecture planning, and later implementation tickets.

This document does not add new product features. It keeps the MVP focused on:

- Public map viewing.
- Reports as pins.
- Scheduled cleanup routes as lines.
- Lightweight joining.
- Creator-controlled report and cleanup photos.
- Creator/admin-controlled status changes.
- Basic trust and moderation.

## 2. V1 UX principles

- Keep the map as the centre of the product.
- Use overlays and bottom sheets over the map where possible.
- Use separate full pages only when they clearly improve focus, such as My Activity, Settings, or web detail pages.
- Let logged-out users browse before asking them to create an account.
- Ask users to sign in only when they try to take an action.
- Keep every creation flow short and forgiving.
- Use structured actions instead of chat or comments.
- Make scheduled cleanups feel social, but do not turn the app into a social network.
- Treat before/after photos as proof of impact.
- Keep web v1 focused on viewing and sharing.

## 3. Logged-out vs logged-in behaviour

| Action | Logged-out user | Logged-in user |
|---|---|---|
| View public map | Allowed | Allowed |
| View report details | Allowed | Allowed |
| View cleanup details | Allowed | Allowed |
| View share links | Allowed | Allowed |
| Create report | Auth required | Allowed |
| Create cleanup | Auth required | Allowed |
| Join cleanup | Auth required | Allowed |
| Leave cleanup | Not applicable | Allowed if joined |
| Upload report photo | Auth required | Allowed if report creator |
| Upload cleanup before/after photos | Auth required | Allowed if cleanup creator |
| Resolve report | Auth required | Allowed if report creator or admin |
| Cancel cleanup | Auth required | Allowed if cleanup creator or admin |
| Complete cleanup | Auth required | Allowed if cleanup creator or admin |
| Flag content | Auth required | Allowed |
| Block user | Auth required | Allowed |
| View My Activity | Auth required | Allowed |
| View account/settings | Auth required | Allowed |

Logged-out users should not hit a hard sign-up wall on app open. They should see the map first, understand the value, and only be asked to sign in when they try to act.

The app should already know whether the user is signed in or signed out from the current session. There should not be a visible auth-check loading state inside normal create, join, or account flows. If the session is unknown during app launch, use a normal app launch/loading state before showing the map.

## 4. Navigation model

### Mobile v1

The mobile app should feel like one fast map product, not a stack of disconnected forms.

Primary structure:

- **Map**: the main home screen and persistent base layer.
- **Create action**: a floating button or corner control that opens a create sheet over the map.
- **Account entry**: a small top-bar or corner control.
- **My Activity**: the user’s own reports, created cleanups, joined cleanups, and completed cleanups.
- **Settings**: basic account actions, support, guidelines, logout, and delete account.

Most map-related experiences should appear as sheets or overlays:

- Report detail sheet.
- Cleanup detail sheet.
- Create report overlay.
- Create cleanup overlay.
- Auth sheet.
- Account sheet.
- Photo picker sheet/component.

### Web v1

Web v1 is for viewing and sharing only:

- Public map.
- Report detail pages.
- Cleanup detail pages.
- Shared report/cleanup links.

Web v1 should not include full report creation, cleanup creation, or joining unless the MVP scope is deliberately changed later.

---

# 5. V1 screens, sheets, and overlays

## 5.1 Public Map Screen

| Field | Description |
|---|---|
| **Screen name** | Public Map Screen |
| **Purpose** | Let users see reports and cleanup activity in a local area. This is the main product screen and persistent base layer. |
| **Main components** | Full-screen map, report pins, planned cleanup route lines, completed cleanup route lines, selected item bottom sheet, simple filters for Reports / Planned cleanups / Completed cleanups, create action button, account/login top-bar control. |
| **Primary action** | Select a report pin or cleanup route to view details. |
| **Secondary actions** | Open create sheet, filter map layers, move around the map, open account sheet/login sheet, open My Activity if signed in. |
| **Empty state** | If no visible reports or cleanups are in the current area, keep the map visible and show calm copy that there is no local activity yet, with actions to create a report or cleanup. |
| **Loading state** | On app launch, load the map first, then progressively load pins and route lines. Avoid blocking the whole screen longer than necessary. |
| **Error state** | If map data fails to load, keep the map visible if possible and show a retry message. If the base map fails, show a full-screen retry state. |
| **Navigation to/from** | Default entry after app launch. Opens Report Detail Sheet, Cleanup Detail Sheet, Create Action Sheet, Account Sheet/Auth Sheet, My Activity, and Settings. Returns from creation flows after successful submission. |

## 5.2 Create Action Sheet

| Field | Description |
|---|---|
| **Screen name** | Create Action Sheet |
| **Purpose** | Let users choose whether they want to report a dirty place or create a cleanup route. It opens over the map. |
| **Main components** | Two clear options: “Report a dirty place” and “Create a cleanup route”. Short explanatory text for each option. Dismiss control. |
| **Primary action** | Choose one creation path. |
| **Secondary actions** | Dismiss and return to map. |
| **Empty state** | Not needed; the sheet always has the two options. |
| **Loading state** | None. Use the current signed-in/signed-out state. If the user is signed out and chooses a restricted action, show the Auth Sheet. |
| **Error state** | If the action cannot open, show a simple retry message and keep the user on the map. |
| **Navigation to/from** | Opens from Public Map. If logged out, goes to Auth Sheet. If logged in, opens Report Creation Overlay or Cleanup Creation Overlay. |

## 5.3 Auth Sheet

| Field | Description |
|---|---|
| **Screen name** | Auth Sheet |
| **Purpose** | Explain that an account is required for actions that change public data or user activity. It should appear over the current context instead of feeling like a heavy separate page. |
| **Main components** | Short reason for sign-in, sign up option, log in option, continue browsing option. |
| **Primary action** | Sign up or log in. |
| **Secondary actions** | Continue browsing and return to the previous screen without taking the action. |
| **Empty state** | Not applicable. |
| **Loading state** | Show progress only while submitting auth credentials. Do not show a visible auth-check loader in normal flows. |
| **Error state** | Show plain-language auth error and allow retry. |
| **Navigation to/from** | Opens when a logged-out user tries to create, join, upload, resolve, complete, flag, block, or open protected account areas. After successful auth, return to the intended action where possible. |

## 5.4 Sign Up / Log In Sheet

| Field | Description |
|---|---|
| **Screen name** | Sign Up / Log In Sheet |
| **Purpose** | Let users create an account or access an existing account without losing map context. |
| **Main components** | Auth form, sign up/log in mode switch, terms/community guidelines acknowledgement where needed, error messaging. |
| **Primary action** | Submit sign up or log in. |
| **Secondary actions** | Switch between sign up and log in, cancel back to map or previous sheet. |
| **Empty state** | Not applicable. |
| **Loading state** | Disable submit and show progress while the auth request is in progress. |
| **Error state** | Show field-level or form-level error. Do not clear user input unnecessarily. |
| **Navigation to/from** | Opens from Auth Sheet or account entry. New users proceed to Username Setup Sheet. Existing users return to the interrupted action or Public Map. |

## 5.5 Username Setup Sheet

| Field | Description |
|---|---|
| **Screen name** | Username Setup Sheet |
| **Purpose** | Create the user’s simple public identity for v1. |
| **Main components** | Username input, username availability/validation message, brief note that public profiles are username-only in v1. |
| **Primary action** | Save username. |
| **Secondary actions** | Back to auth if account setup is incomplete. |
| **Empty state** | Empty username field with helper text. |
| **Loading state** | Show progress while saving username. If availability checking exists, keep it lightweight and non-disruptive. |
| **Error state** | Show clear validation errors such as username unavailable or invalid format. |
| **Navigation to/from** | Opens after sign up if username is missing. Returns to intended action, Public Map, or Account Sheet after completion. |

## 5.6 Account Entry and Account Sheet

| Field | Description |
|---|---|
| **Screen name** | Account Entry / Account Sheet |
| **Purpose** | Give users a clean way to log in, view their account, and access My Activity or settings. |
| **Main components** | On the map: small top-bar or corner control. Logged out state shows “Log in” or an account icon. Logged in state shows username or account icon. Account sheet includes username, My Activity, Settings, community guidelines, support/contact, and logout. |
| **Primary action** | Logged out: open Auth Sheet. Logged in: open Account Sheet. |
| **Secondary actions** | Open My Activity, open Settings, open support/guidelines, log out. |
| **Empty state** | If username is missing, prompt user to complete Username Setup. |
| **Loading state** | Account sheet may show a compact loading state while profile details load. The map should remain usable. |
| **Error state** | Show retry if account details cannot be loaded. |
| **Navigation to/from** | Opens from Public Map top control. Can navigate to Auth Sheet, My Activity, Settings, or back to Public Map. |

## 5.7 Report Detail Sheet

| Field | Description |
|---|---|
| **Screen name** | Report Detail Sheet |
| **Purpose** | Show information about a dirty place that has been reported. |
| **Main components** | Category, status, location preview, optional photo, optional short description, created date, creator username if appropriate, moderation/report action, creator/admin controls where permitted. |
| **Primary action** | For most users: view the report. For the report creator: mark as resolved if open. |
| **Secondary actions** | Flag report, block user where relevant, close detail sheet. Creator/admin may access permitted status actions. |
| **Empty state** | If optional photo or description is missing, show the rest of the report without placeholder clutter. |
| **Loading state** | Show a compact loading card while report details load. |
| **Error state** | If report cannot be loaded, show a retry option and allow returning to the map. If report has been hidden, show a simple unavailable message. |
| **Navigation to/from** | Opens from Public Map or shared link. Can navigate to Auth Sheet for restricted actions, Report/Block Sheet, or back to Public Map. |

## 5.8 Report Creation Overlay

| Field | Description |
|---|---|
| **Screen name** | Report Creation Overlay |
| **Purpose** | Let a signed-in user create a report quickly while keeping the map visible. |
| **Main components** | Map with confirmable report pin, bottom sheet with category selector, optional photo picker entry, optional short description, submit button, cancel/back actions. |
| **Primary action** | Submit report. |
| **Secondary actions** | Adjust pin, add/remove optional photo, edit description, cancel and return to map. |
| **Empty state** | Before category is selected, show a clear prompt. Optional photo and description can be empty. |
| **Loading state** | Disable submit and show progress while the report is being created and any selected photo is uploading. |
| **Error state** | Show clear errors for missing category, failed upload, or failed submission. Preserve entered details where possible. |
| **Navigation to/from** | Opens from Create Action Sheet after auth. Can open Photo Picker Component. On success, returns to Public Map with the new report selected or visible. |

## 5.9 Cleanup Detail Sheet

| Field | Description |
|---|---|
| **Screen name** | Cleanup Detail Sheet |
| **Purpose** | Show the details of a scheduled or completed cleanup route and let users join if eligible. |
| **Main components** | Title, status, route preview on map, date/time, optional meeting point, optional description, organiser username, participant count, before/after photos, join/leave button, moderation/report action, creator/admin controls where permitted. |
| **Primary action** | For non-joined signed-in users: join planned cleanup. For joined users: view details or leave. For creator: manage cleanup status and photos. |
| **Secondary actions** | Leave cleanup if joined, flag cleanup, block user where relevant, close detail sheet. Creator/admin may cancel or complete cleanup. |
| **Empty state** | If there are no photos yet, show the cleanup details without making the page feel broken. If optional meeting point or description is missing, omit those sections. |
| **Loading state** | Show a compact loading card while cleanup details load. |
| **Error state** | If cleanup cannot be loaded, show a retry option and allow returning to the map. If cleanup has been hidden, show a simple unavailable message. |
| **Navigation to/from** | Opens from Public Map, My Activity, or shared link. Can navigate to Auth Sheet, Photo Picker Component, Mark Completed Confirmation Sheet, Report/Block Sheet, or back to Public Map. |

## 5.10 Cleanup Creation Overlay

| Field | Description |
|---|---|
| **Screen name** | Cleanup Creation Overlay |
| **Purpose** | Let a signed-in user create a scheduled cleanup route while keeping the map central. |
| **Main components** | Map route creation mode, visible route line, route instructions, undo/clear actions if supported, bottom sheet with title field, date/time selector, optional meeting point, optional short description, optional before photo picker entry, basic safety notice, publish button, cancel action, note that route lines are approximate. |
| **Primary action** | Publish cleanup. |
| **Secondary actions** | Adjust route, undo/clear route if supported, edit title, edit date/time, add/remove meeting point, add/remove optional before photo, edit description, cancel and return to map. |
| **Empty state** | Before a route is added, show simple instruction text explaining how to create the line. Required fields should show clear prompts when missing. |
| **Loading state** | Disable publish while the cleanup is being created and any selected before photo is uploading. |
| **Error state** | Show clear errors for missing route, missing title, missing date/time, failed upload, or failed submission. Preserve entered details where possible. |
| **Navigation to/from** | Opens from Create Action Sheet after auth. Can open Photo Picker Component. On success, returns to Public Map with the new cleanup selected or visible. |

## 5.11 Photo Picker Component / Sheet

| Field | Description |
|---|---|
| **Screen name** | Photo Picker Component / Sheet |
| **Purpose** | Let permitted creators add a report photo, cleanup before photo, or cleanup after photo. This is a reusable component, not a major standalone screen. |
| **Main components** | Photo picker/camera entry, selected image preview, replace/remove action, confirm/cancel action, upload progress if upload happens immediately. |
| **Primary action** | Select and confirm a photo. |
| **Secondary actions** | Replace selected photo, remove selected photo, cancel. |
| **Empty state** | Show a simple prompt to add a photo. |
| **Loading state** | Show upload or processing progress and prevent duplicate submissions if the upload is happening at that moment. |
| **Error state** | Show upload or selection failure message and allow retry or choosing another photo. |
| **Navigation to/from** | Opens from Report Creation Overlay, Cleanup Creation Overlay, Cleanup Detail Sheet, or Mark Completed Confirmation Sheet for permitted creators. Returns to the previous surface after confirm or cancel. |

## 5.12 Mark Completed Confirmation Sheet

| Field | Description |
|---|---|
| **Screen name** | Mark Completed Confirmation Sheet |
| **Purpose** | Confirm that the cleanup creator wants to mark a planned cleanup as completed. |
| **Main components** | Confirmation copy, optional prompt to add an after photo first, confirm button, cancel button. |
| **Primary action** | Mark cleanup completed. |
| **Secondary actions** | Add after photo first, cancel. |
| **Empty state** | Not applicable. |
| **Loading state** | Disable confirm and show progress while status is updated. |
| **Error state** | Show update failure message and allow retry. |
| **Navigation to/from** | Opens from Cleanup Detail Sheet for the cleanup creator or admin. Can open Photo Picker Component. Returns to Cleanup Detail Sheet after completion. |

## 5.13 My Activity Screen

| Field | Description |
|---|---|
| **Screen name** | My Activity Screen |
| **Purpose** | Give signed-in users a simple place to find their own reports and cleanups. |
| **Main components** | Sections or tabs for reports created, cleanups created, cleanups joined, and completed cleanups created by the user. Each item shows key status and date information. |
| **Primary action** | Open one of the user’s reports or cleanups. |
| **Secondary actions** | Navigate back to map, open Account Sheet or Settings. |
| **Empty state** | If the user has no activity, show simple copy encouraging them to create a report or cleanup from the map. |
| **Loading state** | Show list skeletons or loading rows. |
| **Error state** | Show retry if activity cannot be loaded. |
| **Navigation to/from** | Opens from Account Sheet or main navigation. Opens Report Detail Sheet or Cleanup Detail Sheet. Logged-out users go to Auth Sheet. |

## 5.14 Settings Screen

| Field | Description |
|---|---|
| **Screen name** | Settings Screen |
| **Purpose** | Let users manage basic account actions required for v1. |
| **Main components** | Username/account section, community guidelines, support/contact, log out, delete account. |
| **Primary action** | Manage account settings. |
| **Secondary actions** | Open support/guidelines, log out, delete account, return to map. |
| **Empty state** | Not applicable. |
| **Loading state** | Show progress for account actions. |
| **Error state** | Show clear error if account action fails. |
| **Navigation to/from** | Opens from Account Sheet. Returns to Account Sheet or Public Map after log out. |

## 5.15 Report / Block Sheet

| Field | Description |
|---|---|
| **Screen name** | Report / Block Sheet |
| **Purpose** | Let signed-in users flag inappropriate content or block a user. |
| **Main components** | Flag content action, block user action where relevant, simple reason selector if used, submit/cancel buttons. |
| **Primary action** | Submit report or confirm block. |
| **Secondary actions** | Cancel and return to previous screen. |
| **Empty state** | Not applicable. |
| **Loading state** | Show progress while moderation action is saved. |
| **Error state** | Show failure message and allow retry. |
| **Navigation to/from** | Opens from Report Detail Sheet, Cleanup Detail Sheet, Photo view, or Account/Profile context. Logged-out users go to Auth Sheet first. Returns to previous screen after action. |

## 5.16 Admin Moderation Screen

| Field | Description |
|---|---|
| **Screen name** | Admin Moderation Screen |
| **Purpose** | Give admins a basic way to review flagged reports, cleanups, photos, and users. |
| **Main components** | Flagged item list, item detail preview, status, reporting reason if captured, actions to hide, restore, or mark reviewed. Exact workflow remains an open question in the product spec. |
| **Primary action** | Review a flagged item and take a moderation action. |
| **Secondary actions** | Return to admin/home view. |
| **Empty state** | If no flagged items exist, show “No items to review”. |
| **Loading state** | Show loading list while flagged items load. |
| **Error state** | Show retry if moderation queue cannot be loaded or action fails. |
| **Navigation to/from** | Accessible only to admins. Opens flagged item detail previews and returns to moderation list. |

## 5.17 Web Public Map Screen

| Field | Description |
|---|---|
| **Screen name** | Web Public Map Screen |
| **Purpose** | Let web visitors view the public cleanup map and open shared items. |
| **Main components** | Web map, report pins, cleanup route lines, filters, selected item panel. |
| **Primary action** | View report or cleanup details. |
| **Secondary actions** | Share/open direct links and browse the map. Web v1 should not show full creation flows. |
| **Empty state** | If no items are visible in the current area, show simple copy that there is no local activity yet. |
| **Loading state** | Show map loading and then load public map objects. |
| **Error state** | Show retry if map or public data cannot load. |
| **Navigation to/from** | Opens from direct web visit or shared link. Opens Web Report Detail or Web Cleanup Detail panels/pages. |

## 5.18 Web Report Detail Page

| Field | Description |
|---|---|
| **Screen name** | Web Report Detail Page |
| **Purpose** | Let web visitors view a shared report. |
| **Main components** | Category, status, location preview, optional photo, optional description, created date, link back to map. |
| **Primary action** | View report. |
| **Secondary actions** | Return to web map. |
| **Empty state** | If optional photo or description is missing, omit that section. |
| **Loading state** | Show loading content state while report loads. |
| **Error state** | Show unavailable/retry state if report cannot be loaded or is hidden. |
| **Navigation to/from** | Opens from shared link or Web Public Map. Returns to Web Public Map. |

## 5.19 Web Cleanup Detail Page

| Field | Description |
|---|---|
| **Screen name** | Web Cleanup Detail Page |
| **Purpose** | Let web visitors view a shared cleanup. |
| **Main components** | Title, status, route preview, date/time, optional meeting point, optional description, organiser username, participant count, before/after photos, link back to map. |
| **Primary action** | View cleanup. |
| **Secondary actions** | Return to web map. Web v1 should not show full creation or joining flows. |
| **Empty state** | If optional photos, meeting point, or description are missing, omit those sections. |
| **Loading state** | Show loading content state while cleanup loads. |
| **Error state** | Show unavailable/retry state if cleanup cannot be loaded or is hidden. |
| **Navigation to/from** | Opens from shared link or Web Public Map. Returns to Web Public Map. |

---

# 6. Main onboarding flow

V1 should avoid a long onboarding carousel. The product should reveal itself through the map.

1. User opens app.
2. App shows Public Map.
3. User can browse reports and cleanups without signing in.
4. User taps a restricted action, such as Create Report, Create Cleanup, Join, Upload Photo, Flag, Block, My Activity, or Account Settings.
5. App shows Auth Sheet explaining why an account is needed.
6. User signs up or logs in.
7. New users choose a username.
8. App returns the user to the action they were trying to complete where possible.

## Onboarding rules

- No forced sign-up on first app open.
- No long questionnaire.
- No full profile setup.
- Username is the only public identity required in v1.
- Community/safety copy should be short and tied to relevant actions.
- Login should feel like a lightweight sheet or modal, not a heavy detached journey.

---

# 7. Main report creation flow

## Happy path

1. User taps create action on the Public Map.
2. Create Action Sheet opens over the map.
3. User chooses “Report a dirty place”.
4. If logged out, user completes Auth Sheet first.
5. Report Creation Overlay opens.
6. User confirms or adjusts the report pin location.
7. User chooses category.
8. User optionally adds a photo through the Photo Picker Component.
9. User optionally adds a short description.
10. User submits.
11. App returns to Public Map with the new report visible or selected.

## Required fields

- Location.
- Category.

## Optional fields

- Photo.
- Short description.

## Status after creation

- New reports are created as **Open**.

## Key UX constraints

- A basic report should be possible in under 30 seconds.
- Photo and description should never block submission.
- The flow should feel like a quick local action, not a council complaint form.
- The map should remain visible as much as possible.

---

# 8. Main cleanup creation and joining flow

## 8.1 Create cleanup happy path

1. User taps create action on the Public Map.
2. Create Action Sheet opens over the map.
3. User chooses “Create a cleanup route”.
4. If logged out, user completes Auth Sheet first.
5. Cleanup Creation Overlay opens.
6. User draws or defines an approximate route line on the map.
7. User adds title.
8. User adds date and time.
9. User optionally adds meeting point.
10. User optionally adds short description.
11. User optionally adds a before photo through the Photo Picker Component.
12. User sees a short safety notice.
13. User publishes.
14. App returns to Public Map with the new cleanup visible or selected.

## Required fields

- Route line.
- Title.
- Date and time.

## Optional fields

- Meeting point.
- Short description.
- Before photo.

## Status after creation

- New cleanups are created as **Planned**.

## Key UX constraints

- Route creation should be approximate and forgiving.
- The user should understand that a route line is not an official boundary.
- Road snapping, polygons, radius circles, and advanced GIS are not part of v1.
- The map should remain the main surface during route creation.

## 8.2 Join cleanup happy path

1. User taps a planned cleanup route line on the Public Map.
2. Cleanup Detail Sheet opens.
3. User reviews title, date/time, route, optional meeting point, organiser username, and participant count.
4. If logged out, user is asked to sign in before joining.
5. Signed-in user taps Join.
6. Participant count increases.
7. Cleanup appears in My Activity.

## Join rules

- Join is a lightweight RSVP.
- Joining does not create chat.
- Joining does not require organiser approval in v1.
- The app shows participant count, not public attendee lists.
- Users can leave a cleanup they have joined.

---

# 9. Before/after photo flow

## 9.1 Report photo flow

1. Report creator opens Report Creation Overlay.
2. Creator optionally adds a report photo through the Photo Picker Component.
3. Photo uploads during report submission or before final submit, depending on implementation.
4. Report appears with the photo if upload succeeds.
5. If upload fails, user can retry or submit without photo.

## 9.2 Cleanup before photo flow

1. Cleanup creator opens Cleanup Creation Overlay or Cleanup Detail Sheet for their planned cleanup.
2. Creator chooses to add a before photo.
3. Photo Picker Component opens.
4. Creator selects or captures photo.
5. Creator confirms/uploads.
6. Cleanup Detail Sheet shows the before photo.

## 9.3 Cleanup after photo and completion flow

1. Cleanup creator opens Cleanup Detail Sheet after the cleanup has happened.
2. Creator chooses to add an after photo.
3. Photo Picker Component opens.
4. Creator selects and uploads photo.
5. Creator taps Mark Completed.
6. Confirmation sheet appears.
7. Creator confirms.
8. Cleanup status changes to **Completed**.
9. Cleanup route changes to completed visual state on the map.

## Photo rules

- Report photos are optional.
- Cleanup before/after photos are optional but strongly support the success metric.
- Only the report creator can upload the report photo in v1.
- Only the cleanup creator can upload cleanup before/after photos in v1.
- Report photos and cleanup photos are separate in v1.
- A cleanup may visually cover reported areas, but cleanup photos do not automatically link, merge, or resolve reports.
- Photos can be flagged and hidden through moderation.

---

# 10. Status change flows

## 10.1 Resolve report

1. Report creator opens Report Detail Sheet.
2. Creator taps Mark Resolved.
3. App confirms or applies the action, depending on final UX.
4. Report status changes from **Open** to **Resolved**.
5. Map updates the report visual state.

Only the report creator or an admin can resolve a report.

## 10.2 Cancel cleanup

1. Cleanup creator opens Cleanup Detail Sheet.
2. Creator taps Cancel Cleanup.
3. App confirms the cancellation.
4. Cleanup status changes from **Planned** to **Cancelled**.
5. Cancelled cleanup becomes hidden or muted according to map display rules.

Only the cleanup creator or an admin can cancel a cleanup.

## 10.3 Complete cleanup

1. Cleanup creator opens Cleanup Detail Sheet.
2. Creator optionally uploads after photo.
3. Creator taps Mark Completed.
4. App confirms completion.
5. Cleanup status changes from **Planned** to **Completed**.
6. Cleanup appears as completed impact proof.

Only the cleanup creator or an admin can complete a cleanup.

---

# 11. Report-cleanup relationship in v1

Reports and cleanups are separate objects.

A cleanup route can pass near or through reported areas on the map, but the app should not automatically:

- Link the cleanup to those reports.
- Merge report photos and cleanup photos.
- Mark nearby reports as resolved.
- Notify report creators that their report has been addressed.

This avoids false assumptions and keeps v1 simple. Report-cleanup linking can be considered later after the core loop is proven.

---

# 12. Error and loading behaviour principles

## Loading

- Show progress close to the area that is loading.
- Avoid blocking the whole app unless required.
- Disable duplicate submit actions while requests are in progress.
- Preserve user input while loading.
- Do not show unnecessary loading for signed-in/signed-out checks during normal flows.

## Errors

- Use plain language.
- Preserve user input where possible.
- Offer retry for network or upload failures.
- Return users safely to the map if an item is unavailable.
- Do not expose technical error details to users.

## Empty states

- Keep empty states short and calm.
- Use them to explain what is missing and what the user can do next.
- Do not make an empty local map feel like failure.
- Detailed empty-state copy can be refined during visual design.

---

# 13. Out-of-scope UX for v1

The following screens or experiences should not be designed for v1 unless the product spec is deliberately changed:

- Chat inbox.
- Group chat.
- Direct messages.
- Comments.
- Likes/reactions.
- Followers or friends.
- Public attendee lists.
- Full user profiles.
- Profile photos.
- Social feeds.
- Council dashboards.
- Organisation dashboards.
- Area/polygon cleanup creation.
- Road-snapped route creation.
- Automatic report-cleanup linking.
- Automatic report resolution from cleanup completion.
- Heatmaps.
- Advanced search/filtering.
- Payment/rewards flows.
- Leaderboards.
- Risk assessment workflows.
- Equipment inventory.
