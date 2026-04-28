# OpenSERP Railway Service

This service is the public-search backend for RAYN workflow contact search.

It builds OpenSERP `v0.7.2` and exposes the dedicated engine routes used by the worker:

- `/bing/search?text=...&limit=10`
- `/duck/search?text=...&limit=10`
- `/google/search?text=...&limit=10`

The worker should prefer DuckDuckGo first when Bing is unhealthy, then Google, then Bing after its circuit breaker recovers.

Runtime policy:

- cache TTL is `604800` seconds.
- endpoint fallback is disabled.
- Google rate is kept lower than Bing and DuckDuckGo.
- circuit breaker opens after `3` failures and recovers after `180` seconds.
- no CAPTCHA-solving, stealth automation, fingerprint evasion, or proxy rotation is configured.

Railway healthchecks use `/health`.
