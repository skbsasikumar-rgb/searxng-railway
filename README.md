# OpenSERP Railway Service

This service is the public-search backend for RAYN workflow contact search.

It builds OpenSERP `v0.7.2` and exposes the dedicated engine routes used by the worker:

- `/duck/search?text=...&limit=10`
- `/google/search?text=...&limit=10`

The worker uses DuckDuckGo first, then Google. Bing is excluded from the active provider order because repeated live polls showed circuit-breaker and CAPTCHA-class failures.

Runtime policy:

- cache TTL is `604800` seconds.
- endpoint fallback is disabled.
- Google rate is kept lower than DuckDuckGo.
- circuit breaker opens after `3` failures and recovers after `180` seconds.
- no CAPTCHA-solving, stealth automation, fingerprint evasion, or proxy rotation is configured.

Railway healthchecks use `/health`.
