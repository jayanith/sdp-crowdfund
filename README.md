# HopeRaise: Crowdfunding Platform

A full stack crowdfunding web app where **creators** launch campaigns, **donors** browse and contribute, and **admins** manage users, campaigns and funds.

**Stack:** React 19 (Vite, MUI, Axios, React Router) · Spring Boot (Spring Data JPA, REST) · MySQL 8 · Docker Compose

## Features

- **Creator portal:** register/login, create campaigns with goal, dates, category and image, view own campaigns and donor lists
- **Donor portal:** register/login, browse campaigns, donate with an optional message, view donation and transaction history, update profile
- **Admin portal:** manage creators, donors and campaigns, fund tracking, counts for reports and analytics
- Campaign progress tracked through `goalAmount` vs `collectedAmount`, with active/closed status

## Architecture

```
React (Vite) ──Axios──▶ Spring Boot REST API (:1947) ──JPA──▶ MySQL (hoperaisedb)
```

| Module | Base path | Example endpoints |
|---|---|---|
| Admin | `/admin` | `POST /checklogin`, `GET /allcreators`, `GET /alldonors`, `GET /campaigncount` |
| Creator | `/creator` | `POST /registration`, `POST /checklogin`, `PUT /updateprofile` |
| Donor | `/donor` | `POST /registration`, `POST /checklogin`, `GET /profile/{id}` |
| Campaign | `/campaign` | `POST /add`, `GET /all`, `GET /by-creator/{creatorId}`, `GET /image/{id}` |

Entities: `Admin`, `Creator`, `Donor`, `Campaign`, `Donation`.

## Run with Docker

```bash
docker compose up -d
# frontend  http://localhost:3000
# backend   http://localhost:2025
# mysql     localhost:3307
```

## Run locally

```bash
# backend
cd BACKEND/CFP-SDP-BACKEND && ./mvnw spring-boot:run   # set datasource url to localhost in application.properties

# frontend
cd FRONTEND/sdp-frontend && npm install && npm run dev
```

## Project structure

```
BACKEND/CFP-SDP-BACKEND   Spring Boot: controller / service / repository / model / dto
FRONTEND/sdp-frontend     React: admin / creator / donor / main pages
docker-compose.yml        MySQL + backend + frontend images
```
