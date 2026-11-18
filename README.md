# SANA Omi Mentor

A conversational mentor backend for Omi. This repository contains a starter API, not an installed Omi integration.

## Features
- Natural conversational responses with contextual suggestions
- Optional recent conversation context
- No database or persistent conversation storage
- Health-check endpoint

## Local setup
1. Install Python 3.11+.
2. Run `pip install -r requirements.txt`.
3. Set the `OPENAI_API_KEY` environment variable (never commit your real key).
4. Start with `uvicorn app:app --host 127.0.0.1 --port 8000`.
5. POST JSON to `http://127.0.0.1:8000/mentor`:

```json
{"message":"What should I follow up on after that conversation?","context":["We agreed to confirm the appointment by Friday."]}
```

## Omi integration
The Omi event-to-API adapter is not yet implemented. Confirm Omi's current developer webhook/event format, authentication, and reply mechanism before wiring it to this backend. Do not assume Omi supplies continuous real-time audio or can proactively display every reply.

## Privacy and deployment
This starter stores no messages, but sends supplied text to the configured model API.
Before public deployment add authentication, HTTPS, rate limits, access controls,
and consent safeguards for recorded conversations. Avoid submitting sensitive workplace
or third-party recordings without authorization.

## Private access
Set `SANA_PRIVATE_TOKEN` to a long random secret in the deployment environment. Every `/mentor` request must include `Authorization: Bearer <your-secret>`. Do not commit or share either secret. This protects the endpoint from unauthenticated use, but the deployed service is still reachable on the public internet. Add rate limits and operational controls before continuous use.
