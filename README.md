# Ticket App (Offline Ticket Generator)

Standalone UI to generate and send offline tickets.

## Features
- Manual participant entry
- Registration ID generation
- QR ticket generation
- Email sending support
- Printable/downloadable ticket output

## Setup
1. Ensure backend ticket routes are enabled.
2. Configure backend URL in `index.html`.

## Local Run
```bash
python -m http.server 8080
```
Open:
- `http://localhost:8080/index.html`

## Backend Requirements
Expected endpoints:
- `POST /api/ticket/generate`
- `POST /api/ticket/send-email`

## Notes
- Keep API credentials server-side only.
- Validate email + mobile before generating tickets.
