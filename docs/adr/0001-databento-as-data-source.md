# ADR 0001: Databento as the main data source

Status: Accepted · Date: 2026-11-26

## Context

- Need 1-minute NQ bars and several years of history
- Previous session must be available before 9:00 New York time
- yfinance: only 30 days of 1-minute data

## Decision

- Databento is the only source for all historical data and previous sessions, with the continuous contract `NQ.v.0`
- yfinance is only used for the pre-market price on the morning of the brief

## Alternatives rejected

- **yfinance only**: rejected because of its depth limits
- **yfinance every morning, replaced later by Databento**: not needed, a test showed Databento is available in time

## Consequences

- Cost: ~$27 for the full history since 2010 (covered by the free credits), then ~$2 a year
- Delay: ~8 hours, measured on 2026-11-26, so the previous session is ready well before the brief
- Pre-market price: comes from yfinance, not Databento, so the gap between both sources must be checked once
- Contract rolls: `NQ.v.0` is not back-adjusted, so prices jump on roll days