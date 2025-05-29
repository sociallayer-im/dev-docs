# Social Layer API Documentation

**Base Path:** `https://api.sola.day/api`  
**Format:** JSON  
**Versioning:** via header, vendor: `sola`

---

## Authentication

Most endpoints require authentication via an `auth_token` parameter or a Bearer token in the `Authorization` header.

---

## Endpoints

### Profile

#### Get Current Profile

- **GET** `/profile/me`
- **Description:** Get the current authenticated user's profile.
- **Auth:** Required

#### Get Profile by Email

- **GET** `/profile/get_by_email`
- **Params:**
  - `email` (string, required)
- **Description:** Get a profile by email.

#### Get Profile by Handle

- **GET** `/profile/get_by_handle`
- **Params:**
  - `handle` (string, required)
- **Description:** Get a profile by handle.

#### Get Profile by ID or Handle

- **GET** `/profile/get`
- **Params:**
  - `id` (string, required) — profile ID or handle
- **Description:** Get a profile by ID or handle.

---

### Event

#### Get Event by ID

- **GET** `/event/get`
- **Params:**
  - `id` (integer, required)
- **Description:** Get event details by ID.

#### Discover Events

- **GET** `/event/discover`
- **Description:** Get featured, popup, and top group events.

#### My Starred Events

- **GET** `/event/my_starred`
- **Params:**
  - `limit` (integer, optional, default: 40, max: 1000)
  - `page` (integer, optional)
  - `with_attending` (boolean, optional)
- **Auth:** Required
- **Description:** Get events starred by the current user.

#### Events Attending (by Profile)

- **GET** `/event/attending`
- **Params:**
  - `profile_id` (string, required: id or handle)
  - `collection` (string, optional: `upcoming`, `past`)
  - `limit` (integer, optional, default: 40, max: 1000)
  - `page` (integer, optional)
  - `with_stars` (boolean, optional)
  - `with_attending` (boolean, optional)
- **Description:** Get events a profile is attending.

#### My Attending Events

- **GET** `/event/my_attending`
- **Params:**
  - `collection` (string, optional: `upcoming`, `past`)
  - `limit` (integer, optional, default: 40, max: 1000)
  - `page` (integer, optional)
  - `with_stars` (boolean, optional)
  - `with_attending` (boolean, optional)
- **Auth:** Required
- **Description:** Get events the current user is attending.

#### My Created Events

- **GET** `/event/my_created`
- **Params:**
  - `limit` (integer, optional, default: 40, max: 1000)
  - `page` (integer, optional)
  - `with_stars` (boolean, optional)
  - `with_attending` (boolean, optional)
- **Auth:** Required
- **Description:** Get events created by the current user.

#### List Events in a Group

- **GET** `/event/list`
- **Params:**
  - `group_id` (string, required: id or handle)
  - `track_id` (integer, optional)
  - `tags` (string, optional, comma-separated)
  - `search_title` (string, optional)
  - `venue_id` (integer, optional)
  - `theme` (string, optional)
  - `pinned` (boolean, optional)
  - `skip_multiday` (boolean, optional)
  - `skip_recurring` (boolean, optional)
  - `start_date` (date, optional)
  - `end_date` (date, optional)
  - `start_time` (datetime, optional)
  - `end_time` (datetime, optional)
  - `collection` (string, optional: `upcoming`, `past`, `pinned`)
  - `private_event` (boolean, optional)
  - `limit` (integer, optional, default: 40, max: 1000)
  - `page` (integer, optional)
  - `with_stars` (boolean, optional)
  - `with_attending` (boolean, optional)
- **Auth:** Optional, but required for private/manager views
- **Description:** List events in a group with various filters.

## Error Handling

- **403 Forbidden:** Invalid or missing authentication token.
- **400 Bad Request:** Application errors, missing or invalid parameters, or business logic errors (e.g., group is freezed).

---

## Notes

- Pagination is supported via `limit` and `page` parameters on most list endpoints.
- Some endpoints require the user to be authenticated; others are public.
- Filtering and search parameters are available for event listing endpoints.
- Entities are returned in a structured format as described above.


