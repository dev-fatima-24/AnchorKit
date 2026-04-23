# Pull Request Descriptions

This document contains the descriptions for the pull requests related to the AnchorKit platform updates.

---

## PR 1: Validate toml_url in cache_capabilities
**Branch**: `fix/validate-toml-url-280`

### Description
This PR addresses a bug where `cache_capabilities` stored `toml_url` without validation. Storing an invalid URL in the cache would cause all subsequent fetches to fail. This update ensures that the URL is a valid HTTPS endpoint before caching.

### Changes
- Added call to `validate_anchor_domain` within `cache_capabilities` in `src/contract.rs`.
- Returns `ErrorCode::InvalidEndpointFormat` on invalid URL rejection.
- Added unit test `test_cache_capabilities_invalid_url` in `src/metadata_cache_tests.rs`.

**Closes #280**

---

## PR 2: Add Force Refresh to refresh_anchor_info
**Branch**: `feat/force-refresh-279`

### Description
Currently, `refresh_anchor_info` respects TTL and may return cached data even if a fresh fetch is desired. This PR adds a `force: bool` parameter to allow bypassing the TTL check and forcing a fresh fetch.

### Changes
- Updated `refresh_anchor_info` signature in `src/contract.rs` to include `force: bool`.
- Implemented logic to bypass TTL check when `force` is true.
- Updated `src/anchor_info_discovery_tests.rs` with new test cases for both force and non-force refresh scenarios.

**Closes #279**

---

## PR 3: Add ETA Countdown to TransactionTimeline
**Branch**: `feat/transaction-eta-286`

### Description
Enhances the `TransactionTimeline` component by providing users with an Estimated Time of Arrival (ETA) for their transaction completion.

### Changes
- Added `estimatedCompletionAt` (timestamp in ms) to `TransactionTimelineProps`.
- Implemented a real-time countdown timer that updates every second.
- The countdown is automatically hidden if the prop is not provided or if the transaction is finished.
- Updated `TransactionTimeline.test.tsx` and demo scenarios in the component file.

**Closes #286**

---

## PR 4: Enforce DNS Length Boundaries in Domain Validator
**Branch**: `test/length-boundaries-278`

### Description
Strengthens the domain validation logic by enforcing strict DNS-standard length boundaries: 253 characters for the full domain and 63 characters per label.

### Changes
- Updated `validate_host` in `src/domain_validator.rs` to check for these specific length limits.
- Expanded `test_length_boundaries` to include edge-case tests for 253/254 character domains and 63/64 character labels.

**Closes #278**
