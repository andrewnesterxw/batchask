# batchask

Run a JSONL of prompts through an LLM, results to JSONL

Built for my own use; public in case it helps someone.

## Getting started

```bash
pip install -r requirements.txt
export OPENAI_API_KEY=sk-...
```

## Examples

```bash
python batch.py prompts.jsonl -o answers.jsonl --workers 4 --rpm 300
```

## What it does

- JSONL in, JSONL out: the input is streamed line by line
- Failures go to a sidecar file with error type, message and status
- Real rate limiting: sliding windows on requests/min and tokens/min
- Idempotent: ids already in the output are skipped on a rerun
- Per-row overrides for model, system, temperature and max_tokens
- Progress, token counts and a cost estimate on stderr
- 4xx fails fast; 429 and 5xx retry with jittered backoff
- A bad input line is logged and skipped, never fatal

## Project structure

```text
├── .github/
│   ├── workflows/
│   │   └── ci.yml
│   └── dependabot.yml
├── docs/
│   ├── configuration.md
│   ├── faq.md
│   ├── tradeoffs.md
│   └── usage.md
├── examples/
│   └── quickstart.md
├── tests/
│   └── test_smoke.py
├── .gitignore
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
├── batch.py
├── prompts.sample.jsonl
└── requirements.txt
```

## Development

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python -m pytest -q
```

## License

MIT licensed, see LICENSE.
