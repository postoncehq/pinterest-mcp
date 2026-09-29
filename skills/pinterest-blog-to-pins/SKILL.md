---
name: pinterest-blog-to-pins
description: Turn one blog post URL into 5–10 fresh Pinterest pins, each with its own image, title and description, linked to the post and scheduled over several weeks with the PostOnce Pinterest MCP. Use when the user asks to promote a blog post on Pinterest, turn an article into pins, repurpose a blog for Pinterest, or drive blog traffic from Pinterest.
metadata:
  author: PostOnce
  version: "0.1.0"
---

# Pinterest blog to pins

One good article can carry many pins. Each pin is a different way into the same post: a different angle, image and title, all with the same destination link. Spread them out over weeks instead of posting them all at once.

## Inputs to get first

- The blog post URL. Read the page if your environment can fetch it; otherwise ask the user to paste the text.
- Photos from the post or the user's library. Pins need an image or video; text-only pins aren't possible.
- The Pinterest account and, optionally, the board ID for these pins.
- How many pins (default 6) and over how long (default 3–4 weeks).
- The user's timezone and preferred posting times.

## Find the angles

Read the post and pull 5–10 distinct angles. Each must be true to the post:

| Angle | Example for "How to start a sourdough starter" |
| --- | --- |
| The main promise | Easy Sourdough Starter for Beginners |
| A specific audience | Sourdough Starter Without a Kitchen Scale |
| A list inside the post | 5 Signs Your Sourdough Starter Is Ready |
| A problem it solves | Why Your Sourdough Starter Isn't Rising |
| A step or timeline | Day-by-Day Sourdough Starter Schedule |
| A checklist or printable | Sourdough Starter Supplies Checklist |

Skip angles the post doesn't actually cover. Never invent results, stats or quotes.

## Build each pin

- **Image:** a different photo or layout for every pin. Use the `pinterest-pin-maker` skill for 1000×1500 images with a text overlay. Don't reuse one image with a new title; Pinterest treats new images as fresh pins.
- **Title (up to 100 characters):** the angle's search phrase first. Use the `pinterest-pin-description-generator` rules.
- **Description (up to 500 characters):** the phrase in the first sentence, related phrases after, a reason to click at the end. No hashtags.
- **Link:** the blog post URL, set as `link` in `platform_options`. Every pin in the set uses the same link.

## Schedule

- Space pins out: one or two per week per post works well, and alternating angles keeps the set from looking repetitive.
- Put the strongest angle first.
- Use the user's times; if they have none, suggest evenings and weekends, when many people browse Pinterest, and say it's a starting point.

## Output

Return a table: date and time, title, description, image note, link, board. Then the rendered images or design notes. On approval, upload each image with `create_upload_url` and call `create_post` once per pin with `publish_at`, the image as `media`, and `title`, `link` and optional `boardId` in `platform_options` (see the `postonce` skill). Confirm the account, board and schedule before the first `create_post`. Report each post ID and scheduled time, and check one with `get_post`.
