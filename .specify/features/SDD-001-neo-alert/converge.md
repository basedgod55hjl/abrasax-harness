# SDD-001 convergence

## Evidence
- `py_compile` clean on `_NEO_TON_PULSE.py`.
- Module import clean (no side effects outside `__main__`).
- Live-fire: `send_telegram_alert()` returned a real Telegram `message_id`
  (see run log 2026-11-08).
- Counter behavior: 3rd consecutive failure triggers exactly one alert;
  `ok` resets the counter; recovery after an alerted episode sends a
  recovery message (verified by code path + episode flag).

## Outcome
CONVERGED. The pulse now pages Telegram on transformer darkness and
announces recovery, with secrets never transiting logs.
