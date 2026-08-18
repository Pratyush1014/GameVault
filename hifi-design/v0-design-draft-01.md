# GameVault — V0 Design Draft 01

## Design Objective
GameVault is a premium mobile gaming discovery and backlog product. The app helps gamers save games they discover across TikTok, YouTube, Reddit, Twitch, Instagram, X, gaming websites, and friends into a beautiful personal gaming library that answers one fundamental question: "What should I play next?"

The design goal is to feel like a premium combination of:
- streaming platform visual polish
- console UI elegance
- a personal gaming library
- a discovery-first recommendation product

This is not a CRUD app, not a database dashboard, and not a generic checklist. It should feel cinematic, immersive, and rich.

---

# Design Direction Overview

## Concept A — Cinematic
Large, dramatic artwork. Minimal text. Premium console-like presence. Best for the "wow" factor and hackathon demo.

## Concept B — Modern Gaming Library
Strong grid, backlog management, and discoverability. Best for utility + long-term product value.

## Concept C — Social Discovery
High-energy, discovery-first, community-driven. Best for the "share from social media" emotional hook.

---

# Shared Product Design System

## Core Visual Principles
- Dark luxury gaming palette
- Layered depth on dark surfaces
- Strong game artwork with dark gradients
- Minimal clutter
- Fast scanning and premium motion language
- Touch-first spacing for mobile
- Highly visual game cards and status cues

## Typography
- Display: bold condensed or high-contrast sans for titles
- Heading: strong medium-weight titles
- Body: clean readable text with slightly elevated letter spacing
- Metadata: compact uppercase labels

## Spacing System
- 4px base unit
- 8, 12, 16, 20, 24, 32, 40, 48, 64
- Comfortable breathing room for mobile content

## Border Radius
- Small cards: 12–16px
- Large hero panels: 24–32px
- Buttons: 14–18px
- Pill chips: 999px

## Navigation Treatment
- Bottom nav with 4 items: Home, Discover, Wishlist, Profile
- Icon + label
- Active item uses luminous accent and stronger contrast

## Status Chips
- Want to Play
- Playing
- Completed
- On Hold
- Dropped
- Saved
Colors should be subtle but distinguishable:
- blue for backlog
- green for completed
- amber for playing
- violet for premium/high priority

## Game Card Treatment
- Image-first card layout
- Strong gradient overlays for readability
- Minimal metadata with clear hierarchy
- Hover/tap states should feel tactile

## Empty State Style
- Cinematic and aspirational
- Use emotional product storytelling
- Avoid generic “no records found” UI

---

# Concept A — Cinematic

## Design Intent
This direction is built to feel premium, cinematic, and engineered for a flashy hackathon demo. The product should feel like a luxury gaming app where the artwork is the hero, not the interface chrome.

## Mood and Visual Language
- dramatic lighting
- strong asymmetry
- atmospheric gradients
- dark mode with cool accent lighting
- large featured art for the “what should I play next?” moment
- almost no unnecessary UI clutter

## Screen 1 — Home / Play Next

### Layout
Top bar:
- “Good evening, Alex”
- avatar on right
- notification icon

Hero recommendation card:
- huge background image of Clair Obscur: Expedition 33
- soft vignette with dark overlay
- title in high-contrast typography
- chips: “RPG”, “PC / PS5 / Xbox”, “Your #1 pick”
- CTA: View Game
- secondary: + Add

Below hero:
- “Your Top 10”
- horizontal ranked game strip with large numbers layered behind cover art

Then:
- “Continue Playing” with 2–3 active cards
- “Recently Saved” with tiny content-source tags for TikTok/Reddit/YouTube

### Composition
The hero should occupy around 35–40% of the viewport height. The rest flows below with clean scrolling rhythm.

### Emotional tone
Feels like a premium game launcher mixed with streaming UX.

### Example card hierarchy
- large featured card
- medium rank cards
- compact metadata chips
- minimal text labels

---

## Screen 2 — Wishlist / Backlog

### Layout
Top section:
- “My Backlog”
- search icon
- filter chips: All / Want to Play / Playing / Completed / On Hold

Grid:
- 2-column card grid
- cover art with overlay metadata on bottom-left
- status chip placed top-right
- title and small “9/10” rating in bottom text area

### Interaction
Cards feel like collectible objects; selecting a game opens a premium detail view.

### Example content
- Elden Ring
- Cyberpunk 2077
- Hades II
- Baldur's Gate 3
- Hollow Knight: Silksong
- Black Myth: Wukong

---

## Screen 3 — Game Detail

### Layout
Full-bleed hero image at top with overlay gradient. Title displayed highly legibly over image. Trailer play button floating over art.

Metadata row beneath:
- release year
- genre
- platforms
- developer
- status control

Primary section hierarchy:
1. About
2. Media
3. My Activity
4. GameVault Community Rating
5. Reviews

Status selector uses anchored pill buttons or a bottom sheet with clear state changes.

### My Activity
- personal rating: 9 / 10
- review summary card
- “Write Review” CTA

### Community Score
- 8.9 / 10
- “1.2K GameVault players”
- rating bar or mini histogram

### Review cards
Large cards with soft shadows, subtle borders, rating and spoiler indicator.

---

## Screen 4 — Share-to-GameVault Recognition

### Layout
Full-screen bottom sheet or confirmation card that feels like a successful product moment.

Visual breakdown:
- background blur
- cover art large
- “Game detected ✨”
- “Hades II”
- source type: TikTok icon + label
- subtle confidence bar or “Matched from your shared post” text
- primary CTA: Add to Wishlist
- secondary: Not the right game?

### UI intent
This screen should feel magical; the user is immediately reassured that the app understood the discovery.

---

## Screen 5 — Discover / Search

### Layout
Search field large and round.

Sections:
- Trending Now
- New Releases
- For You
- Upcoming

Cards use big artwork and minimal text. The app remains aspirational and visually rich.

---

## Design System Notes for Concept A
- Strong use of oversized imagery
- Premium dark UI with cyan/violet accents
- Minimalistic typography, almost editorial
- Buttons are bold and deliberate
- Status chips are reduced to minimal pills

---

# Concept B — Modern Gaming Library

## Design Intent
This direction prioritizes backlog management, organization, and visible utility. It still feels luxurious, but the product is more like a personal gaming archive and library. This is the strongest option for long-term engagement and user retention.

## Mood and Visual Language
- stronger card grid and dense metadata
- more practical information density
- easier scanning and filtering
- premium but efficient
- cover art remains central, but UI is more structured and list-like

## Screen 1 — Home / Play Next

### Layout
Header with greeting and avatar.

Top section: “What should I play next?”

Featured recommendation card is still large, but more structured:
- game title on left
- cover art on right or full-width over a dark overlay
- reason indicator: “Top recommendation based on your backlog”
- CTA: View Game

Below that:
- “Your Top 10” in a ranked carousel or compact horizontal list
- “Continue Playing” as narrow cards with status and progress
- “Recently Saved” as a compact set of source-aware cards

### Distinction from Concept A
This design uses more visible info density without feeling cluttered.

---

## Screen 2 — Wishlist / Backlog

### Layout
This is the strongest screen in this concept.

Header:
- “My Backlog”
- count
- search
- filter row

The core layout is a vertical list with cover thumbnails and metadata blocks, plus a grid toggle.

Each item shows:
- cover art
- title
- platform(s)
- status pill
- personal rating
- small priority dot or indicator
- quick actions: menu, status edit, review

### Filtering
- All
- Want to Play
- Playing
- Completed
- On Hold
- PC / PS5 / Switch / Xbox toggles

### Visual treatment
The list stays elegant, not spreadsheet-like. It reads like a curated library.

---

## Screen 3 — Game Detail

### Layout
Hero image with a media preview row beneath. Instead of a very minimal layout, this one includes more structured info and strong data modules.

Sections:
- Overview
- Platforms and release info
- My Activity
- Community Score
- Reviews

A bottom action bar remains pinned to the lower area for quick status changes.

### Personal activity section
- status selector dropped into a segmented control
- rating row with 10-star-like design or score chips
- review note preview

### Distinction
This concept makes game tracking and management feel like a real, useful personal library, not just a visual showcase.

---

## Screen 4 — Share-to-GameVault Recognition

### Layout
A compact confirmation sheet overlaid on the current screen. It should feel efficient and fast.

Visual stack:
- source chip: TikTok
- title + cover art
- confidence line: “Matched from shared content”
- action row with Add to Wishlist and Search Manually
- status selector: Want to Play / Saved / Playing

### UX value
This interaction is highly practical and reduces friction.

---

## Screen 5 — Discover / Search

### Layout
Search field with filters and trending chips.

Sections:
- Trending
- New Releases
- For You
- Upcoming

Cards are more consistent than Concept A and read like a strong discovery catalog.

### Visual formula
Artwork + metadata + red dot or tag + quick add control.

---

## Design System Notes for Concept B
- More information density
- Better backlog operations
- Clean horizontal chips and segmented controls
- Game cards have equal weight and need consistent spacing
- The UI still feels premium because of strong visual rhythm and dark elegant surfaces

---

# Concept C — Social Discovery

## Design Intent
This direction emphasizes the social nature of discovery: users see games in TikTok, YouTube, Reddit, and friends’ posts, and GameVault should make discovery feel immediate, social, emotional, and exciting. This concept is the most “community and discovery-first.”

## Mood and Visual Language
- energetic composition
- stronger card stacking and layered media
- discovery feeds, hashtags, source chips, trending indicators
- more movement and visual excitement
- still premium, but more active and alive

## Screen 1 — Home / Play Next

### Layout
Header:
- “Good evening, Alex”
- discover/search button
- avatar

Hero section:
- large feature card with game art + social reason tag
- subtitle like “Based on your recent discoveries”

Below the hero:
- “Trending in your orbit”
- stacked horizontal cards with narrower art
- small source labels: TikTok, Reddit, YouTube

Then:
- “Your Top 10” with less formality and more energy
- cards with rank number plus cover image

### UX feeling
This design makes the app feel like a living discovery feed, not a static library.

---

## Screen 2 — Wishlist / Backlog

### Layout
Instead of a strict list or grid, this version uses a more editorial mixed layout:
- first row: featured backlog highlight
- stacked cards below with status recency and platform tags
- some cards in a two-column masonry-like composition

This approach reads more like a game magazine + library blend.

### Information approach
Lots of metadata is still present, but organized to feel more social and less spreadsheet-like.

---

## Screen 3 — Game Detail

### Layout
The detail screen is rich in community energy:
- hero art
- gameplay/media row
- “Status” section with one-tap controls
- “Why it was saved” contextual card: discovered from TikTok / YouTube / Reddit
- community rating cards
- review cards with social proof and user reactions

### Personality
This version feels like a “game social graph” more than a standard product detail page.

---

## Screen 4 — Share-to-GameVault Recognition

### Layout
A highly polished bottom sheet with a sleek “discovery card” feel.

Content:
- top source chip
- small preview panel of the shared content or link source
- detected title with cover art
- “Confidence match” indicator
- “Save to Wishlist” and “Choose another” CTA

### Emotional goal
The user should feel the app instantly understood the discovery and turned it into something actionable.

---

## Screen 5 — Discover / Search

### Layout
This screen feels like a content feed for games, not just a search page.

Sections:
- Trending
- Recently discovered by community
- Editors’ picks
- Your saved genres

Large cards with community metadata and social signals.

The app feels lively, contextual, and discovery-rich.

---

## Design System Notes for Concept C
- Social proof emphasized visually
- Discovery-driven cards and source metadata
- More playful and active energy
- Great for the crucial “Share → Detect → Save” hook

---

# Comparison Summary

## Concept A — Cinematic
Best for:
- hackathon pitch
- emotional wow factor
- premium first impression
- hero-art-driven interface

Weaknesses:
- less information density
- less obvious backlog management power

## Concept B — Modern Gaming Library
Best for:
- real usability
- long-term product value
- backlog management
- organized backlog growth

Weaknesses:
- less emotionally dramatic
- not quite as “wow” in a live demo

## Concept C — Social Discovery
Best for:
- product uniqueness
- social discovery and source-driven concept
- the share-to-app core loop
- community feel

Weaknesses:
- a little less structured for long-term storage and management

---

# Best Direction Recommendation

If the team wants a visually striking product for a hackathon, the strongest immediate candidate is:

## Concept A with elements of Concept B
- Cinematic hero and premium visual treatment
- but with enough structure from Concept B to make the backlog practical and maintainable

If the team wants a more product-usable long-term product, the strongest is:

## Concept B

If the team wants the most distinctive social-discovery feel, the strongest is:

## Concept C

---

# Design Recommendation for the Next Iteration
The next round should combine the strongest pieces of each concept:

- Concept A’s cinematic hero and premium emotional polish
- Concept B’s structured backlog and collection management
- Concept C’s discovery-first social framing

This will likely produce a final direction that feels premium, usable, and highly differentiated for the hackathon.

---

# Immediate Next Step
The next design pass should refine one direction into a full mobile set with:
- exact spacing tokens
- final typography scale
- selected accent palette
- one final icon language
- a clean 4–5 screen flow shown as a full hi-fi prototype

At that stage, the product will feel ready for demo presentation and engineering handoff.
