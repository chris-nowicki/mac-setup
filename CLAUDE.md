# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a personal Mac setup guide repository (not a software project). It documents apps, tools, settings, and configurations for a new Mac. The README.md is the primary artifact — it's a living document that gets updated as the setup evolves.

## Commands

- `npm run toc` — regenerates the README table of contents using doctoc
- `npm install` — install dev dependencies (doctoc, husky)
- `brew bundle --file=Brewfile` — install all Homebrew packages, casks, fonts, and Mac App Store apps

## Pre-commit Hook

Husky runs `npm run toc && git add README.md` on every commit, automatically updating the doctoc-generated table of contents in README.md. Do not manually edit the TOC section between the `<!-- START doctoc -->` and `<!-- END doctoc -->` comments.

## Repository Structure

- `README.md` — the main setup guide with OS settings, app lists, CLI tools, and configuration steps
- `Brewfile` — single file containing all Homebrew formulae, casks, fonts, and Mac App Store apps

## Key Conventions

- The `Brewfile` should stay in sync with what's documented in the README
- macOS settings are documented as `defaults write` commands (scriptable, not screenshots)
- Dotfiles are maintained in a separate repo: https://github.com/chris-nowicki/dotfiles
