---
name: pinterest-board-ideas
description: Suggest searchable Pinterest board names and board descriptions for a niche, brand or blog. Use when the user asks for Pinterest board ideas, board names, how to organize their Pinterest boards, or board descriptions.
metadata:
  author: PostOnce
  version: "0.1.0"
---

# Pinterest board ideas

Boards tell Pinterest what your pins are about. A board named for a real search phrase helps every pin on it. Suggest board names and descriptions; the user creates the boards in Pinterest themselves. This server can't create, rename or delete boards.

## Inputs to get first

- The niche, the audience, and what the pins link to (blog, shop, videos).
- Existing boards, if any, so you don't duplicate them.
- Keywords, if the user ran the `pinterest-seo-keywords` skill.
- Whether this is a personal or business account. For a business, boards should map to what it sells or teaches.

## Rules for board names

- Use the phrase a person would search: "Small Balcony Garden Ideas", not "My Green Corner".
- Keep names short and clear. Pinterest allows long names, but 2–6 words reads best on profiles and in search.
- One topic per board. "Home Decor" is too broad for a new account; "Boho Bedroom Decor" or "Small Living Room Ideas" is focused.
- Cover the user's main topics first (5–10 boards), then add narrower boards as content grows.
- Avoid inside jokes, puns and brand names alone as board names, unless it's a board for the brand's own products.
- Seasonal boards ("Fall Table Decor", "Christmas Cookie Recipes") are worth adding if the user has seasonal content.

## Board descriptions

- 1–3 sentences. Open with the board's keyword phrase and say what the reader finds there.
- Add 2–3 related phrases naturally. No hashtags, no keyword lists.
- Example: "Small balcony garden ideas for renters: container plants, vertical planters and layouts that fit tight spaces. Easy projects for city apartments."

## Output

Return a table: board name, description, and 3 example pin topics for each board. Mark which boards to create first. Tell the user to create the boards in the Pinterest app or website and paste in each name and description. Once the boards exist, the user can give their agent a board's ID to pass as `boardId` when publishing with the `postonce` skill. Without a `boardId`, PostOnce puts pins on the account's default board or a board named "PostOnce".
