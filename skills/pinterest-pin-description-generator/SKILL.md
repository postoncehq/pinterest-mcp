---
name: pinterest-pin-description-generator
description: Write keyword-led Pinterest pin titles and descriptions that match what people search, ready to publish with the PostOnce Pinterest MCP. Use when the user asks for a pin description, pin title, Pinterest description generator, Pinterest caption, or wants to write or improve the text on a pin.
metadata:
  author: PostOnce
  version: "0.1.0"
---

# Pinterest pin description generator

Pinterest works like a search engine. People type what they want ("easy weeknight pasta", "small balcony garden ideas") and pins with matching words in the title and description get found. Write the text so the pin answers a search, then hand it to the `postonce` skill if the user wants it published.

## Before writing

Get or infer: what the pin shows, where it links (blog post, product page, video), who it's for, and 1–3 search phrases the user wants to rank for. If the user has no keywords, use the `pinterest-seo-keywords` skill first or pick the plain phrase a person would type to find this pin. Never invent prices, results, ratings or claims about the product.

## Title (up to 100 characters)

- Lead with the main keyword phrase, in plain words. "Easy Sourdough Starter for Beginners" beats "My Starter Journey".
- Add the benefit or angle after it: "…in 7 Days", "…(No Scale Needed)", "…for Small Kitchens". Only use a number if it's true.
- Keep the useful words in the first 40 or so characters; many surfaces cut long titles.
- The server sends the title as `title` in `platform_options`. If no title is set, Pinterest gets the first 100 characters of the description, which usually reads badly. Always write one.

## Description (up to 500 characters)

- First sentence: the main keyword and what the reader gets. It's the part people see first.
- Then 1–2 sentences with related phrases people also search (ingredients, style, season, room, audience). Write them as sentences, not a list of tags.
- End with a reason to tap: what's on the other side of the link ("Full recipe and printable timeline on the blog.").
- Stay under 500 characters. Text over the limit is cut off, not rejected.
- The post `content` becomes the pin description.

## What to avoid

- Hashtags. Pinterest no longer leans on them for discovery. Put the words in the sentence instead.
- Keyword stuffing ("pasta recipe easy pasta quick pasta dinner pasta"). Write for a person first.
- Vague titles with no search words ("Love this!", "New post").
- Clickbait that the linked page doesn't deliver.

## Alt text

Pinterest supports alt text, but this server doesn't send it. If the user wants alt text, write one plain sentence describing the image and tell them to add it in Pinterest after the pin is live.

## Output

For each pin, return:

- **Title** (with character count)
- **Description** (with character count)
- **Link** (if any)
- **Board** (name or ID, if the user gave one)

Offer 2–3 title variants when the angle isn't obvious. Then offer to publish or schedule it with the `postonce` skill: confirm the Pinterest account, the board (`boardId`, optional; without it the pin goes to the account's default board or a board named "PostOnce"), the `link`, and the time before calling `create_post`. A pin needs an image or video.
