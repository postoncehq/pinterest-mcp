---
name: pinterest-pin-maker
description: Design Pinterest pin images at 1000×1500 (2:3) with a readable text overlay, render them from HTML to PNG, and publish them with the PostOnce Pinterest MCP. Use when the user asks for a Pinterest pin maker, pin template, pin image, pin graphics, or wants to turn a photo, product or blog post into a pin.
metadata:
  author: PostOnce
  version: "0.1.0"
---

# Pinterest pin maker

Make vertical pin images that read clearly as a small thumbnail in the Pinterest feed, then upload and publish them.

## Specs

- **Size:** 1000×1500 px (2:3). This is the standard pin shape. Pinterest accepts aspect ratios from 2:3 to 3:2 through this server; taller images risk being cropped in the feed.
- **Format:** PNG or JPEG (WebP also works). Up to 32 MB per image. GIFs can't be uploaded through `create_upload_url`.
- **Carousel:** up to 5 images, all the same size. **Video pin:** one MP4 or MOV, 4 seconds to 5 minutes. Don't mix images and video in one pin.

## Inputs to get first

The topic or page the pin links to, the headline (use the `pinterest-pin-description-generator` skill if there isn't one), a photo or product image if the user has one, and brand colors and fonts. Never add claims, prices or ratings the user didn't give you.

## Layout that works

- **Headline:** 3–8 words, large (roughly 70–110 px), high contrast. It should be readable when the pin is a small thumbnail in a phone feed.
- **Photo:** real photos of the result, product or process beat stock images. Fill at least half the pin.
- **Text block:** a solid or semi-opaque band behind the text so it stays readable over any photo.
- **Brand:** a small logo or URL at the bottom, not over the main image.
- **Safe area:** keep text at least 60 px from every edge. Keep the bottom-right corner clear, where Pinterest's own buttons can overlap.
- One idea per pin. Several short lines, not a paragraph.

Common templates: photo on top with headline band below; full-bleed photo with a centered text band; split "before / after"; numbered list ("5 Small Balcony Plants") for a list post; step preview for a tutorial.

## Making the images

If the environment can render HTML to PNG (for example headless Chrome or Playwright), build each pin as a fixed-size 1000×1500 HTML page with inline CSS and the image as a local or public URL, then screenshot it at exactly 1000×1500. Check the result at thumbnail size before uploading. Otherwise, hand the user the headline, layout notes, colors and image choice for their design tool.

For several pins linking to the same page, vary the photo, headline and layout on each one. Pinterest favors fresh images over the same image pinned again.

## Upload and publish

Upload each PNG with `create_upload_url`, PUT the bytes, and get the public URL with `get_media` (see the `postonce` skill). Pass the URLs in order as `media` in `create_post`. Set `title` (up to 100 characters) and `link` in `platform_options`, and optionally `boardId`; the post `content` becomes the description (up to 500 characters).

## Output

Return the pin plan (headline, image, layout, colors) and the rendered files or design notes, plus the title, description and link. Offer to publish or schedule with the `postonce` skill; confirm the Pinterest account, board and time before calling `create_post`.
