# NVIDIA NIM Provider for Kujo

[![Version](https://img.shields.io/badge/version-0.1.0-black)](https://github.com/kujolang/nvidia-nim/releases/tag/v0.1.0)
[![License](https://img.shields.io/badge/license-MIT-black)](LICENSE)
[![built with Kujo](https://img.shields.io/badge/built%20with-Kujo-black)](https://github.com/kujolang/kujo)

NVIDIA NIM provider for Kujo with OpenAI-compatible chat inference and explicit
host/model configuration for hosted or self-managed NIM endpoints.

## Install

```bash
kujo kennel add github:kujolang/nvidia-nim@v0.1.0
kujo kennel install
```

## 30-second quick start

```kujo
from nvidia_nim import create_client, chat

client := create_client({
    "api_key": env("NVIDIA_API_KEY"),
    "model": "meta/llama-3.1-8b-instruct",
})

result := chat(client, {
    "messages": [{"role": "user", "content": "Say hello."}],
})
print(result["data"])
```

## Native Provider API

The default hosted endpoint is `https://integrate.api.nvidia.com/v1`; self-hosted
NIM deployments may provide another approved HTTPS endpoint. Model IDs and
OpenAI-compatible request fields remain visible.

```kujo
from nvidia_nim import create_client, chat

client := create_client({
    "base_url": "https://integrate.api.nvidia.com/v1",
    "api_key": env("NVIDIA_API_KEY"),
    "model": "meta/llama-3.1-70b-instruct",
})

result := chat(client, {
    "messages": [
        {"role": "user", "content": "Explain NIM deployment."},
    ],
    "temperature": 0.2,
})
```

## AI SDK integration

NVIDIA NIM chat uses the public OpenAI-compatible driver shape. The native
client retains endpoint and model configuration.

```kujo
from nvidia_nim import nvidia_nim_provider
from ai_sdk import generate_text

provider := nvidia_nim_provider({"model": "meta/llama-3.1-8b-instruct"})
result := generate_text(provider, {"messages": [{"role": "user", "content": "Hello."}]})
print(result["text"])
```

## Authentication and security

Set `NVIDIA_API_KEY`. Authorization is sent only to approved HTTPS hosts;
embedded credentials and secret leakage are rejected or redacted.

## Testing and docs

```bash
bash scripts/release_quality_gate.sh
```

See [`docs/`](docs/) for implementation and conformance evidence.
