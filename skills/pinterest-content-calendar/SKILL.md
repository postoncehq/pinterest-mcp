---
name: pinterest-content-calendar
description: Plan 1–4 weeks of Pinterest pins from the user's goals, content pillars or a source to repurpose (blog URL, video, transcript), draft every pin, and schedule them with the PostOnce Pinterest MCP. Use when the user asks for a Pinterest content calendar, a Pinterest posting schedule, Pinterest pin ideas for the month, or a plan to keep pinning consistently.
metadata:
  author: PostOnce
  version: "0.1.0"
---

# Pinterest content calendar

Plan a steady run of pins, draft each one fully, and schedule the set once the user approves it. Pinterest rewards consistency and fresh pins over bursts, so a calendar is a good fit.

## Inputs to get first

- Goal: traffic to a blog, sales from a shop, email sign-ups, or awareness.
- Pillars (2–5 topics) or a source to repurpose: blog URLs, a video, a transcript, a product list.
- How many weeks (1–4) and pins per week. A small account can start with 3–7 pins a week; more only if the user has the images.
- Pinterest account, board IDs if they want specific boards, timezone and preferred times.
- What images exist. Every pin needs an image or a video.

## Pin types to mix

| Type | Media | Good for |
| --- | --- | --- |
| Image pin | 1 image, 1000×1500 (2:3) | Most pins: recipes, tutorials, products, list posts |
| Carousel | 2–5 images, same size | Steps, before/after, a product in several colors |
| Video pin | 1 video, 4 seconds to 5 minutes | How-to clips, process, quick demos |

Rules:

- Each pin has its own image and title, even when several link to the same page. Use `pinterest-blog-to-pins` for one article and `pinterest-pin-maker` for images.
- Plan seasonal topics ahead; people search for holidays and seasons weeks before they arrive.
- Titles up to 100 characters, descriptions up to 500, keyword first, no hashtags (see `pinterest-pin-description-generator`).
- Set `link` to the page the pin promotes. Links are optional but most Pinterest goals need one.
- Don't repeat the same pin on the same board in the same week.

## Build the calendar

1. Spread pillars evenly across the weeks.
2. Give each slot: date and time, pillar, pin type, title, description, link, board, image note.
3. Flag slots that still need an image from the user.

## Output

Return the calendar as a table, then the full text of every pin. Ask for approval and edits. On approval, for each pin: upload images with `create_upload_url`, then call `create_post` with `publish_at`, `media`, and `title`, `link` and optional `boardId` in `platform_options`. Pins without images yet go in as `create_draft`. Confirm the account, boards and timezone before the first `create_post` (see the `postonce` skill), then report each post ID and time.
