# Product Requirements Document
**Working Title:** GameVault
**Hackathon:** RevenueCat Shipaton 2026
**Category:** Gaming / Gaming Bucket List
**Document Status:** Initial MVP PRD
**Primary Goal:** Build a mobile-first application that turns game discoveries from social media and the web into an intelligent, organized gaming wishlist/backlog.

---

# 1. Product Vision
Gamers discover interesting games everywhere:

- TikTok
- Instagram / Reels
- YouTube / Shorts
- Reddit
- X
- Twitch
- Discord
- Steam
- PlayStation / Xbox / Nintendo content
- Gaming websites and blogs
- Friends sharing links
The problem is that **discovery happens in one place, but gaming happens somewhere else and often much later**.

A user may see an interesting game during a work break, think:

> "That looks cool. I should play it sometime."
They save the post, bookmark it, send it to themselves, take a screenshot, or simply forget about it.

The application should solve this by becoming the user's **universal gaming inbox + intelligent backlog**.

The fundamental product loop is:

**Discover → Share → Identify → Save → Prioritize → Play → Rate**

The application should make saving a game require as little effort as possible.

---

# 2. Core User Story
Consider the following example.

It is a Tuesday afternoon.

A user is at work and takes a short break.

They open TikTok and see a video showing gameplay from an interesting game.

Instead of:

1. remembering the game's name,
2. opening another application,
3. searching for it,
4. manually creating a wishlist entry,
the user simply taps:

**Share → GameVault**

GameVault receives the shared URL/content.

The backend attempts to determine which game the social-media post is referring to.

For example:

```
TikTok Post
      ↓
Share
      ↓
GameVault
      ↓
Game Identification
      ↓
Cyberpunk 2077
      ↓
Game metadata lookup
      ↓
Add to user's wishlist
```
Later that evening, the user opens GameVault.

They see:

```
Your Gaming Backlog

1. Cyberpunk 2077
2. Clair Obscur: Expedition 33
3. Elden Ring
4. Hades II
5. Hollow Knight: Silksong
...
```
Rather than displaying hundreds of saved games with no structure, the application should eventually help surface a **Top 10 / priority backlog** based on the user's interests and behavior.

---

# 3. Product Value Proposition

## Primary value proposition

> **Never lose a game discovery again.**
GameVault becomes the place where games discovered anywhere on the internet are converted into an actionable gaming backlog.

## Secondary value proposition
Instead of merely maintaining a wishlist, GameVault helps answer:

> **"What should I play next?"**
This distinction is important.

A simple wishlist competes with Steam, PlayStation, Xbox, IGN, Backloggd, etc.

An **intelligent discovery-to-backlog system** provides a stronger product identity.

---

# 4. MVP Goals
The MVP should prove four things.

### Goal 1 — Capture
Users can quickly save a game they discover.

### Goal 2 — Identify
The system can determine which game the shared content refers to.

### Goal 3 — Organize
Users can maintain a useful personal gaming backlog.

### Goal 4 — Engage
Users can return to the application to:

- browse their games,
- change statuses,
- prioritize games,
- inspect game information,
- rate games,
- write reviews/notes.

---

# 5. MVP Scope

## P0 — Required for Hackathon MVP
The following should be considered core functionality.

### Authentication
User can:

- sign up,
- log in,
- log out,
- maintain a basic profile.
Authentication implementation should remain simple for the hackathon.

---

## Wishlist / Backlog
Users can:

- add a game,
- remove a game,
- view saved games,
- search their saved games,
- change game status,
- rate a game,
- write a review/note,
- open the game's detail page.

---

## Share-to-App
The desired experience is:

```
Social Media App
      ↓
Share
      ↓
GameVault
      ↓
Process URL
      ↓
Identify Game
      ↓
Confirm
      ↓
Wishlist
```
Example:

```
User watches TikTok about "Hades II"

Share
  ↓
GameVault
  ↓
"Looks like Hades II"
  ↓
[Add to Wishlist]
```
The user should ideally not need to manually type the game's name.

---

# 6. Game Identification Pipeline
This is one of the most important technical/product differentiators.

When content is shared, the backend should create a **Game Discovery Pipeline**.

Conceptually:

```
Shared URL
    ↓
URL Resolver
    ↓
Extract available metadata
    ↓
Game Candidate Detection
    ↓
Game Search
    ↓
Confidence Score
    ↓
Match Game
    ↓
Enrich Metadata
    ↓
Wishlist
```

## Stage 1 — Receive shared content
Example:

```
{
  "url": "https://...",
  "source": "tiktok"
}
```
Potential sources:

```
TIKTOK
INSTAGRAM
YOUTUBE
REDDIT
TWITCH
X
WEB
MANUAL
OTHER
```

---

# 7. Game Recognition Strategy
The recognition system should use multiple strategies rather than depending entirely on AI.

Recommended order:

### Strategy A — Direct metadata extraction
Attempt to extract:

- page title,
- OpenGraph metadata,
- description,
- hashtags,
- URL information,
- structured metadata.
This is inexpensive and deterministic.

---

### Strategy B — Search against Global Game Catalog
Search the extracted terms against the internal games database.

Example:

```
"Why Clair Obscur is my GOTY"

→ search catalog

→ Clair Obscur: Expedition 33
```

---

### Strategy C — External Game Metadata Provider
If the game does not exist locally, query an external gaming database/API.

Potential providers to evaluate:

- IGDB
- RAWG
- Giant Bomb or alternatives
- Steam APIs where applicable
**The exact provider should be evaluated before implementation based on API restrictions, rate limits, licensing, metadata quality, image availability, and hackathon constraints.**

---

### Strategy D — AI-assisted identification
If deterministic methods fail, use an LLM to infer possible game names from available metadata.

Example input:

```
Post title:
"This new soulslike is absolutely insane"

Description:
"Can't stop playing Lies of P..."

Hashtags:
#liesofp #soulslike #gaming
```
Expected structured output:

```
{
  "game": "Lies of P",
  "confidence": 0.96
}
```
AI should assist with **identification**, not become the source of truth for game metadata.

---

# 8. Important Area to Rethink — Social Media Restrictions

> **⚠️ REQUIRES VALIDATION BEFORE IMPLEMENTATION**
Do not assume that TikTok, Instagram, X, etc. will allow the backend to freely scrape the contents of every shared URL.

Platforms may restrict:

- scraping,
- metadata access,
- APIs,
- video downloads,
- captions,
- authentication,
- automated requests.
Therefore, Share-to-App should be designed as a pipeline where different sources can have different extraction strategies.

For the hackathon, supporting **one or two sources extremely well** is preferable to pretending to support every social network.

Suggested first targets:

```
1. YouTube
2. Generic web URLs
3. Manual game search
```
Then experiment with TikTok/Instagram depending on technical feasibility.

---

# 9. Global Game Catalog
The backend maintains a global normalized catalog.

Example:

```
GAME

id
externalGameId
title
slug
description
releaseDate
coverImageUrl
backgroundImageUrl
developer
publisher
genres
platforms
trailerUrl
createdAt
updatedAt
```
This is shared across users.

Do **not** duplicate the complete game metadata for every wishlist.

---

# 10. User Game / Wishlist Model
The relationship between a user and game should be stored separately.

Conceptually:

```
USER
  |
  |
  +------ USER_GAME ------ GAME
```
Example:

```
USER_GAME

id
userId
gameId

status
priority
rating
review
notes

sourceUrl
sourcePlatform

createdAt
updatedAt
completedAt
```
This model makes it possible for 100,000 users to save the same global game while maintaining independent:

- statuses,
- ratings,
- reviews,
- priorities,
- notes.

---

# 11. Game Statuses
Recommended statuses:

```
SAVED
WANT_TO_PLAY
PLAYING
COMPLETED
ON_HOLD
DROPPED
WAITING_FOR_SALE
```
For the initial MVP, this can be simplified to:

```
WANT_TO_PLAY
PLAYING
COMPLETED
DROPPED
```
`SAVED` may also be useful as the default state for newly discovered games.

---

# 12. Wishlist UI
The main screen should **not feel like a database table**.

It should feel like a visual gaming collection.

Possible layout:

```
┌──────────────────────────────────┐
│ Good evening 👋                  │
│                                  │
│ What should you play next?       │
│                                  │
│ YOUR TOP PICKS                   │
│                                  │
│ ┌────────────┐ ┌────────────┐    │
│ │ Game Art   │ │ Game Art   │    │
│ │            │ │            │    │
│ │ Elden Ring │ │ Hades II   │    │
│ └────────────┘ └────────────┘    │
│                                  │
│ YOUR BACKLOG                     │
│                                  │
│ Cyberpunk 2077       Want to Play│
│ Hollow Knight        Playing     │
│ Balatro              Completed   │
│                                  │
└──────────────────────────────────┘
```
Game artwork should be a major part of the experience.

---

# 13. Top 10 / Priority System
Eventually, users may have dozens or hundreds of games.

The system should produce a smaller:

> **"Play Next" / Top 10**
Initially, avoid building an overly complex AI recommendation engine.

The MVP ranking can use a deterministic scoring system.

Example conceptual factors:

```
priorityScore =
    recency
  + userInterest
  + manualPriority
  + repeatedDiscovery
  + ratingSignals
  + platformPreference
```
Later versions can introduce recommendation models.

---

# 14. Important Area to Rethink — Recommendation Algorithm

> **⚠️ DO NOT OVERENGINEER FOR MVP**
A recommendation engine could consume the entire hackathon.

For V1:

Allow users to manually prioritize games and combine that with simple heuristics.

For example:

```
40% explicit user priority
25% recently saved
20% game interest signals
15% other signals
```
The exact formula is not important initially.

The experience is.

---

# 15. Game Detail Screen
Selecting a game opens an immersive game detail page.

Recommended hierarchy:

```
Hero Artwork

GAME TITLE

Trailer / Gameplay

[Want to Play ▼]

Platforms
PS5 • Xbox • PC

Release Date
Genre
Developer

ABOUT
Game description...

YOUR ACTIVITY

Your Rating
★★★★★★★★★☆

Your Review
"This combat system is..."

COMMUNITY

GameVault Rating
8.7 / 10

Community Reviews
...
```
The game page should visually emphasize:

1. artwork,
2. trailer/gameplay,
3. status,
4. user's relationship with the game.

---

# 16. Ratings
GameVault should maintain **its own rating system**.

This is important.

External ratings such as IGN should not become the application's primary rating.

Example:

```
GameVault Rating

8.7

Based on 1,248 players
```
The aggregate rating is calculated from GameVault users.

---

# 17. Reviews
Users can write reviews after or while playing.

Suggested review fields:

```
rating
reviewText
spoiler
createdAt
updatedAt
```
Later:

- likes,
- comments,
- reviewer profiles,
- spoiler filtering,
- review ranking.
These social capabilities are **post-MVP** unless time permits.

---

# 18. External Reviews

> **⚠️ OPTIONAL / REQUIRES API & LICENSING VALIDATION**
The initial idea includes displaying reviews from other platforms.

This should **not block the MVP**.

There may be:

- licensing restrictions,
- API limitations,
- attribution requirements,
- scraping restrictions.
Prioritize:

```
Game metadata
↓
GameVault user ratings
↓
GameVault user reviews
↓
External reviews (optional)
```

---

# 19. Global Catalog Synchronization
The global games list does not necessarily need to be completely populated beforehand.

Recommended architecture:

```
External Game API
        ↓
Scheduled Sync
        ↓
Global Game Catalog

AND

User shares unknown game
        ↓
On-demand Lookup
        ↓
Game API
        ↓
Create Game
        ↓
Global Catalog
```
Use both strategies.

### Scheduled jobs
A background scheduled job can periodically discover:

- new releases,
- upcoming games,
- trending games,
- metadata changes.
Example:

```
Every 6–24 hours
      ↓
Fetch recent/upcoming games
      ↓
Upsert catalog
```

### On-demand enrichment
Do not wait for the cron job when a user discovers something.

```
User saves unknown game
      ↓
Immediate lookup
      ↓
Populate catalog
```
This creates a **lazy-loading catalog** that improves naturally as users use the application.

---

# 20. Recommended Backend Architecture
For the hackathon, avoid unnecessary microservices.

Recommended:

```
Mobile Application
        ↓
REST API
        ↓
Spring Boot Backend
        ↓
PostgreSQL
```
Additional integrations:

```
                ┌─ Game Metadata API
                │
Spring Boot ────┼─ AI/LLM
                │
                ├─ RevenueCat
                │
                └─ Object/CDN URLs
```
Background processing:

```
Shared URL
     ↓
API
     ↓
Discovery Job
     ↓
Metadata Extraction
     ↓
Game Identification
     ↓
Game Enrichment
     ↓
Database
```
For MVP, asynchronous work can initially use Spring background jobs / scheduled jobs rather than introducing Kafka or a complicated distributed architecture.

---

# 21. Proposed Backend Modules
Keep a modular monolith.

```
com.gamevault

auth/
user/
game/
wishlist/
discovery/
review/
rating/
recommendation/
integration/
    gameprovider/
    ai/
    revenuecat/
cheduler/
```
This preserves clear boundaries without slowing development with microservices.

---

# 22. Suggested API Surface
Example REST APIs:

```
POST   /auth/login
POST   /auth/register

GET    /games
GET    /games/{id}
GET    /games/search?q=

POST   /discover
GET    /discover/{jobId}

GET    /wishlist
POST   /wishlist
PATCH  /wishlist/{id}
DELETE /wishlist/{id}

PATCH  /wishlist/{id}/status
PATCH  /wishlist/{id}/priority

POST   /games/{id}/rating
POST   /games/{id}/reviews

GET    /games/{id}/reviews

GET    /recommendations
GET    /recommendations/top
```
Do not treat these paths as final contracts. Generate an OpenAPI specification once the domain model is finalized.

---

# 23. Frontend Recommendation
Recommended stack:

**React Native + TypeScript**

Potentially Expo if it does not interfere with required native Share Extension functionality.

The major technical requirement to investigate early is:

> **Receiving shared URLs from other mobile applications.**
This functionality can require native iOS/Android integration, so it should be prototyped **before spending significant time polishing UI**.

---

# 24. Recommended App Navigation
Bottom navigation:

```
Home
Discover
Wishlist
Profile
```
Potential home experience:

```
HOME

Continue Playing
      ↓

Your Top 10
      ↓

Recently Saved
      ↓

Trending / Recommended
```
For MVP, `Discover` can primarily provide manual game search.

---

# 25. UI Design Direction
The application should feel closer to:

**Netflix + Spotify + gaming library**

rather than:

**CRUD application + database dashboard.**

Use:

- large game artwork,
- immersive hero sections,
- horizontal carousels,
- subtle gradients,
- dark theme,
- strong typography,
- game cover cards,
- smooth transitions,
- status chips,
- minimal text on browsing screens.
Avoid clutter.

---

# 26. AI-Assisted UI Development
Suggested workflow:

### Step 1 — Generate concepts
Use a UI-generation/design tool to rapidly explore:

- Home
- Wishlist
- Game Detail
- Share Confirmation
- Search
- Profile
- Paywall
Possible tools include Figma's AI features and UI-generation tools such as v0.

### Step 2 — Select one design system
Do **not** independently generate every screen.

That usually produces inconsistent designs.

First establish:

```
Typography
Spacing
Card style
Corner radius
Background
Buttons
Navigation
Game cards
Status chips
```
Then generate screens from that system.

### Step 3 — Implement in Cursor
Give Cursor:

1. this PRD,
2. chosen screenshots/design,
3. frontend architecture rules,
4. API specification.
Then implement feature-by-feature.

---

# 27. RevenueCat / Monetization
RevenueCat integration will be added to satisfy the hackathon requirement and demonstrate a real monetization model.

The exact monetization model is **not yet finalized**.

Potential premium capabilities:

```
FREE

Basic wishlist
Manual game search
Game statuses
Limited discovery saves

PREMIUM

Unlimited wishlist/discovery
AI-powered game identification
Advanced backlog ranking
Personalized recommendations
Advanced statistics
Additional collection features
```

> **⚠️ REQUIRES PRODUCT DECISION**
Do not immediately paywall the application's core magic.

If Share → Identify → Save is the primary reason users love the product, making it completely unavailable without payment could damage onboarding.

A better approach may be a generous free allowance followed by premium power-user functionality.

Revenue model should be finalized separately.

---

# 28. MVP Data Model
High-level entities:

```
USER
 ├── USER_GAME
 │       │
 │       └── GAME
 │
 ├── REVIEW
 │
 └── RATING

GAME
 ├── GAME_PLATFORM
 ├── GAME_GENRE
 ├── MEDIA
 └── EXTERNAL_REFERENCE

DISCOVERY
 ├── userId
 ├── sourceUrl
 ├── sourcePlatform
 ├── detectedGameId
 ├── confidence
 └── status
```

---

# 29. Discovery States
A discovery request should have an explicit lifecycle.

```
RECEIVED
PROCESSING
MATCHED
NEEDS_CONFIRMATION
FAILED
```
Example:

```
Instagram URL
      ↓
PROCESSING
      ↓
Candidate:
"Black Myth: Wukong"

Confidence: 97%
      ↓
MATCHED
```
For uncertain results:

```
We aren't completely sure.

Did you mean?

○ Hades
○ Hades II
○ None of these
```
Never silently save an incorrect game when confidence is low.

---

# 30. Duplicate Handling
If the user shares the same game repeatedly:

**Do not create duplicate wishlist entries.**

Instead, this can become a useful signal.

Example:

```
Hades II

Discovered 4 times

TikTok ×2
YouTube ×1
Reddit ×1
```
Repeated discovery could eventually increase the game's recommendation score.

This creates a powerful implicit-interest signal.

---

# 31. Analytics
Track key product events:

```
app_opened

share_received
discovery_started
game_detected
game_detection_failed
game_confirmed

game_added
game_removed

game_status_changed
game_completed

game_rated
review_created

game_detail_viewed

paywall_viewed
subscription_started
subscription_cancelled
```
These events will help demonstrate product thinking during hackathon judging.

---

# 32. Success Metrics
Primary MVP metric:

> **Games successfully captured from discovery → wishlist**
Supporting metrics:

```
Discovery identification success rate
Time from share → saved game
Games saved per user
Wishlist return rate
Status updates per user
Games completed
Ratings submitted
Reviews submitted
Top-10 interactions
Premium conversion
```

---

# 33. Out of Scope for Initial MVP
Do not attempt all of these during the first implementation:

- full social network,
- following users,
- messaging,
- multiplayer matchmaking,
- achievements,
- game launcher integration,
- Steam library synchronization,
- PlayStation library synchronization,
- Xbox library synchronization,
- sophisticated ML recommendation engine,
- universal scraping of every social platform,
- complex microservices,
- Kafka/event-streaming infrastructure,
- extensive external-review aggregation.
These can be future roadmap items.

---

# 34. Key Technical Risks

## ⚠️ Risk 1 — Social Media Content Extraction
TikTok/Instagram/etc. may restrict automated content retrieval.

**Action:** Prototype this immediately.

---

## ⚠️ Risk 2 — Game Identification Accuracy
A social-media post may not explicitly mention the game.

**Action:** Build confidence-based matching and user confirmation rather than assuming AI is always correct.

---

## ⚠️ Risk 3 — Game Metadata Provider
The application depends heavily on good game metadata.

**Action:** Evaluate IGDB vs RAWG or another provider before locking the backend integration.

---

## ⚠️ Risk 4 — Mobile Share Extension
Share-to-App is central to the product but involves native mobile behavior.

**Action:** Build a tiny proof of concept early:

```
TikTok/Browser
    ↓
Share
    ↓
GameVault
    ↓
Receive URL
```
Do this before building the polished application.

---

## ⚠️ Risk 5 — Scope Creep
Ratings + reviews + AI + recommendations + social + external APIs + subscriptions can quickly become too much for a hackathon.

Protect the core demo:

```
Discover
   ↓
Share
   ↓
Identify
   ↓
Save
   ↓
Beautiful Wishlist
   ↓
Game Details
   ↓
Status / Rating
```
Everything else is secondary.

---

# 35. Recommended MVP Demo
The hackathon demo should tell a story rather than demonstrate API endpoints.

### Scene 1 — Discovery
User is scrolling social media.

They discover an interesting game.

### Scene 2 — Capture

```
Share → GameVault
```

### Scene 3 — Intelligence
GameVault displays:

```
Game detected ✨

Clair Obscur:
Expedition 33

[Add to Wishlist]
```

### Scene 4 — Backlog
The game immediately appears in the user's visually rich gaming collection.

### Scene 5 — Decision
GameVault surfaces:

```
YOUR TOP 10

#1 Clair Obscur
```

### Scene 6 — Gaming lifecycle
The user changes:

```
Want to Play
      ↓
Playing
      ↓
Completed
```
Then rates the game.

### Scene 7 — Monetization
Show the RevenueCat-powered premium experience.

This creates a coherent demo narrative:

> **I discovered it. GameVault remembered it. GameVault helped me decide to play it. And eventually I completed and rated it.**

---

# 36. Recommended Build Order
Do not build the application screen-by-screen.

Build one **vertical slice** first:

```
1. Create database schema
           ↓
2. Game catalog/search API
           ↓
3. Wishlist API
           ↓
4. Basic mobile wishlist
           ↓
5. Game details
           ↓
6. Receive shared URL
           ↓
7. Identify game
           ↓
8. Add detected game
           ↓
9. Status/rating/review
           ↓
10. Top-10 ranking
           ↓
11. RevenueCat
           ↓
12. UI polish
```
The first milestone should therefore be:

> **A user can search for a game, add it to their wishlist, view its details, and update its status.**
Once that works end-to-end, add the more technically risky **Share → Identify → Save** experience.

---

# 37. Architecture Principle
Keep the hackathon architecture deliberately boring where possible.

```
React Native
      ↓
Spring Boot
      ↓
PostgreSQL
```
Then isolate external complexity behind interfaces:

```
GameMetadataProvider
GameDiscoveryService
AIIdentificationService
SubscriptionService
```
This allows APIs/providers to change without rewriting the core application.

---

# 38. Product Principle
Every engineering decision should reinforce the core promise:

> **A gamer should be able to discover a game anywhere and save it with almost zero effort.**
The project's differentiator is **not the wishlist itself**.

The differentiator is:

```
Internet Discovery
        ↓
One-tap Capture
        ↓
Intelligent Identification
        ↓
Personal Gaming Backlog
        ↓
"What should I play next?"
```
That should remain the center of the product throughout the hackathon.

---

# 39. Open Decisions
The following questions should deliberately remain open until validated:

1. Final product name.
2. IGDB vs RAWG vs another game-data provider.
3. Which social platforms can realistically support URL extraction.
4. React Native/Expo versus native functionality required for Share Extensions.
5. Exact Top-10 ranking algorithm.
6. RevenueCat subscription structure and pricing.
7. Which functionality should be premium.
8. Whether external reviews can legally/technically be displayed.
9. Whether AI recognition should happen synchronously or asynchronously.
10. Whether community/social functionality belongs in the hackathon MVP.
These should **not be silently decided by Cursor or another coding agent**.

---

# 40. Instructions for AI Coding Assistants
When this PRD is provided to Cursor, Copilot, ChatGPT, Claude, or another coding agent:

**Do not attempt to implement the entire PRD at once.**

First:

1. Read and understand the complete PRD.
2. Identify ambiguities before making major architectural decisions.
3. Treat sections marked **⚠️ REQUIRES VALIDATION / RETHINK** as unresolved.
4. Preserve MVP scope.
5. Prefer a modular monolith over microservices.
6. Do not introduce infrastructure unless required.
7. Keep game metadata separate from user-specific game state.
8. Keep external APIs behind provider interfaces.
9. Design the Share → Identify → Save flow as the application's central experience.
10. Build the application in vertical slices.
11. Keep RevenueCat integration modular until the revenue model is finalized.
12. Do not fabricate API capabilities for TikTok, Instagram, IGDB, RAWG, or other providers.
13. Ask before making a product decision that materially changes this PRD.

## Immediate implementation objective
The first development milestone is:

> **Build the frontend foundation and backend foundation necessary for a user to search for a game, save it to their wishlist, view its details, and update its status.**
After that works, implement:

> **Share URL → Detect Game → Confirm → Add to Wishlist.**
That sequence gives the team a functioning product early while preserving the feature that makes the hackathon project distinctive.
