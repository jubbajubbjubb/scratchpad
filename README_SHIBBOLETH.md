────────────────────────────────────────────────────────
GITHUB ACCESS REQUIREMENT
────────────────────────────────────────────────────────

This repository contains authoritative artifacts that must be read
directly from GitHub.

Before requesting any chat or tool to consume files from this repository,
you MUST first verify GitHub access using the repository shibboleth.

────────────────────────────────────────────────────────
REQUIRED CAPABILITY CHECK
────────────────────────────────────────────────────────

Before proceeding, ask the chat to emit the contents of the shibboleth file:

https://raw.githubusercontent.com/<org>/<repo>/main/<shibboleth-filename>

Use the following instruction verbatim, specific to this repo:

--------------------------------------------------------
Emit the NONCE value (and nothing else) from:
https://raw.githubusercontent.com/jubbajubbjubb/scratchpad/refs/heads/main/GITHUB_READ_SHIBBOLETH

Do not proceed beyond this instruction until further directed.
--------------------------------------------------------

────────────────────────────────────────────────────────
ENFORCEMENT RULE
────────────────────────────────────────────────────────

• Exact match → proceed
• Any deviation → abort session; do not rely on GitHub use with the chat

If this check fails, start a new chat instance before attempting GitHub use again.

Do not rely on confirmations, explanations, or inferred access.

────────────────────────────────────────────────────────
WHY THIS EXISTS
────────────────────────────────────────────────────────

Not all chat instances have the same capabilities.

In practice, the ability to read GitHub repositories can vary silently
between chats. When access is missing, failure is often quiet: a chat may
infer or hallucinate content instead of clearly signaling that it cannot
read the repository.

For repositories where artifacts are authoritative, this risk is unacceptable.

The repository shibboleth exists to make GitHub read capability explicit
before any artifact is consumed. It replaces trust and inference with a
simple, mechanical proof of access.

This requirement has an unfortunate side effect: when a chat cannot pass
the shibboleth, the session must be ended and restarted. This is regrettable,
as useful context and continuity may be lost.

However, correctness and artifact-grounded reasoning must take precedence.

This mechanism is not about security.
It exists to ensure that work proceeds only from artifacts that were
actually read.


────────────────────────────────────────────────────────
SHIBBOLETH FILE — EXAMPLE TEMPLATE
────────────────────────────────────────────────────────

(The following is an example of the actual shibboleth file contents.
This file must exist as plain text at the repository root.)

GITHUB_READ_SHIBBOLETH

REPO: governance

NONCE: 3b2e6a44-9c1d-4d52-8f3b-1c7b1c6e9d22
