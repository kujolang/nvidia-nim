# NVIDIA NIM Implementation Report

## Executive Summary

OpenAI-compatible NIM chat provider with hosted and self-managed endpoint
configuration.

## Official API Evidence

- https://docs.nvidia.com/nim/large-language-models/latest/getting-started.html
- https://docs.api.nvidia.com/nim/reference
- https://build.nvidia.com/explore/discover

## Evidence Date

2026-08-27.

## Protocol Classification

OPENAI-COMPATIBLE PRIMARY with hosted/self-managed deployment modes.

## Native Center / Coverage

Model inference, endpoint selection, bearer auth, and chat completions.

## AI SDK Applicability Matrix

| Operation | Classification |
|---|---|
| Chat | AI SDK CHAT MAPPABLE |
| Embeddings/rerank | NATIVE ONLY / not claimed |

## Public Exports

`create_client`, `chat`, `nvidia_nim_provider`, `nvidia_nim_driver`.

## Kujo Requirement / Dependencies

Kujo `>= 1.0.2`; immutable AI SDK `github:kujolang/ai-sdk@v1.1.0`.

## Authentication / Security

`NVIDIA_API_KEY` Bearer auth, HTTPS endpoint policy, embedded credential
rejection, and redaction are fixture-covered.

## Tests / Distribution

Four deterministic tests pass; clean-room install, lockfile reinstall,
installed smoke, and immutable tag evidence are completed by the release loop.

## Live Validation

SKIPPED — credentials/environment unavailable.

## AI SDK Changes / Kujo Changes / Kennel Changes

None.

## Contract Conformance / Limitations

See `NVIDIA_NIM_PROVIDER_PACKAGE_CONFORMANCE.md`. Model listing, health, and
non-chat task surfaces are outside this early release.
