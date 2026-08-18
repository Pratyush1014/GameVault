# GameVault

GameVault is a mobile-first gaming backlog and discovery platform built for the RevenueCat Shipaton 2026. The product helps gamers save, organize, and prioritize games they discover across social media, videos, articles, and links without losing track of them.

## Project Goal

GameVault turns internet discovery into a clean, actionable gaming wishlist:

- discover a game from a link, post, or video
- identify the correct title
- save it to a personal backlog
- organize it by status and priority
- revisit and rate it later

The long-term vision is to help users answer: "What should I play next?"

## Repository Structure

This repository is currently organized as a monorepo:

- `frontend/` — mobile/web frontend
- `backend/` — API services and business logic
- `docs/` — product docs, PRDs, and planning materials

## Current Status

This repo is in its early MVP planning stage. The foundation is being set up so that the team can build the product iteratively:

- product requirements and direction are documented
- monorepo folders are in place
- frontend and backend work can begin in parallel

## Basic Setup Notes

These are intentionally lightweight and will be expanded as the app is built.

### Requirements

- Git
- Node.js / npm for frontend work
- Java / Spring Boot for backend work
- PostgreSQL for app data

### Suggested workflow

1. Work in the appropriate folder: `frontend/` or `backend/`
2. Keep documentation in `docs/`
3. Make small, reviewable changes
4. Keep code and PRD updates aligned as features mature

## Contributing

This project is meant to evolve with the team. If you are contributing, please:

- keep the product vision in mind: discover → identify → save → prioritize → play
- favor clear, maintainable code over clever shortcuts
- document decisions and assumptions
- keep changes small and focused
- update docs when product or architecture decisions change

We are building this together. If you have ideas, improvements, or new directions, contribute them and help shape the product.

## Notes for Future Development

The repo will continue to grow as we add:

- mobile frontend flows
- backend APIs and game catalog logic
- share-to-app discovery workflows
- wishlist and status management
- ratings, reviews, and recommendation features

This README is intentionally minimal for now. We will revisit and expand setup, architecture, and contribution docs as the frontend and backend are implemented.
