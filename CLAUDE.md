# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with this repository.

## Repository Purpose

This repo implements the paper "De-anthropomorphizing 'AI': From wishful mnemonics to accurate nomenclature" (Inie, Zukerman, Bender) as a practical text-transformation framework. The goal is providing instructions that LLMs can follow to generate de-anthropomorphized outputs.

## Key Files

- `.claude/skills/deanthro/SKILL.md` — The Claude Code skill version of the framework. Wrapped with YAML frontmatter for automatic activation. When editing the framework, keep this and `deanthropomorphize.md` in sync.
- `deanthropomorphize.md` — The core framework. This is the "product." It contains the instructions injected into LLM prompts to enforce functionality-first language. Edit this file carefully — it's consumed as prompt text, so clarity and conciseness matter (token budget is a constraint).
- `README.md` — Usage guide with implementation methods (prompt inclusion, system prompts, API integration) and verification strategies.
- `longer_example.md` — Side-by-side comparison of model output with and without the framework for the prompt "How can AI help with research?"
- `paper_examples_converted.csv` / `.xlsx` — Substitution examples from the paper, converted by various models (claude-4-5-sonnet, gpt-5.2, deepseek-v3). Columns: Category, Input, model outputs.
- `.gitignore` — Standard macOS/Windows/Linux/Office ignores.

## Workflow

This is a content repo with no build system, tests, or linting. Development consists of editing the markdown framework and data files. When changing `deanthropomorphize.md`, verify the framework still aligns with the 8 prohibited language categories from the paper and the substitution table.
