# SDD-001: NEO pulse Telegram alerting

## Spec (what and why)
The NEO/TON pulse is the ecosystem's heartbeat. Today a transformer outage
only darkens `node_neo` in the entanglement state; nobody is told. Kairos
should page the creator on Telegram when the resident model fails
consecutively, and again when it recovers.

- Trigger: `ALERT_THRESHOLD = 3` consecutive `lm_pulse` failures.
- Channel: Telegram bot, chat from `.env` (`ABRASAX_TELEGRAM_CHAT_ID`).
- Message: compact, with the last error and a note that TON is still checked.
- Secrets: token read from environment/.env only; never logged, never in argv.
- Recovery alert: a second alert when `ok` returns after an alert was sent.

## Plan
1. Extend `_NEO_TON_PULSE.py` with an `.env` loader (stdlib, setdefault).
2. Add `send_telegram_alert(text)` -> message_id or None (never raises).
3. Track consecutive failures in `main()`; alert on threshold; re-alert on
   recovery (send once per episode).
4. Verify: module compiles/imports, alert send returns a real message_id
   (live-fire), counter logic exercised by unit check.

## Tasks
- [x] .env loader in pulse
- [x] send_telegram_alert
- [x] failure counter + threshold alert + recovery alert
- [x] live-fire test (real message_id)
- [x] converge report

## Risk notes
- Sending requires the bot token valid; failure is silent (returns None).
- One alert per episode, not per failure: no spam.
