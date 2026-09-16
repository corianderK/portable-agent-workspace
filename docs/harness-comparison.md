# Harness comparison

This document records one hands-on portability experiment performed in September 2026. It is not a permanent compatibility matrix. Versions, providers, parsers, and model behavior change quickly.

## What was held constant

The experiment kept the following as constant as possible:

- same local repository;
- same repository-owned handoff protocol;
- same OpenRouter account/key family;
- same DeepSeek V4.1 Flash model when comparing Cline vs Kilo;
- same read-only recovery goal before execution.

## Roo Code

Observed during setup:

- the extension displayed a notice that active Roo Code development had ended;
- its model catalog was already behind newer models needed for the test;
- the project was therefore not used as the long-term fallback harness.

Takeaway: a portable repository should not depend on one extension remaining actively maintained.

## Cline + OpenRouter + GPT-5.6 Sol

Observed result: **successful repository recovery and tool use**.

The agent recovered project state from repository files, inspected Git metadata, and reconstructed the current task and verification state.

This validated the repository-owned state pattern independently of the original Codex session.

## Cline + OpenRouter + DeepSeek V4.1 Flash

Observed result: **reasoning succeeded, tool execution was unreliable in this test**.

The model correctly understood the resume protocol and identified which files/tools it needed next. However, repeated tool calls appeared as raw DSML-like invocation text instead of being executed by Cline, eventually triggering repeated tool-call failures.

Important: this does **not** mean DeepSeek cannot use tools or that Cline will always fail with this model. It is an observation from this specific model/provider/harness/version combination.

## Kilo Code + OpenRouter + DeepSeek V4.1 Flash

Observed result: **successful file tool use and full repository-state recovery**.

A minimal test successfully used file-reading tools to read `AGENTS.md` and `ORCHESTRATOR.md`. A subsequent full read-only handoff recovered milestone/task state, safety gates, verification status, and the exact next authorized action.

The same model that failed tool execution in the Cline test therefore succeeded when the harness changed.

## Key lesson

> Model capability ≠ harness compatibility.

Benchmarks alone are not enough for agentic development. A useful evaluation matrix includes:

- reasoning quality;
- coding quality;
- tool-call protocol compatibility;
- command/edit reliability;
- context management;
- approval controls;
- cost transparency;
- provider reliability.

## Recommended testing order

For any new model + harness pair:

1. minimal `read_file` test;
2. full read-only repository recovery;
3. one small controlled execution step;
4. full milestone/batch execution only after the first three pass.
