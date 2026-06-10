# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository is a single static page: [index.html](index.html) — a one-page investment strategy/financial advisory landing page. There is no build system, package manager, or dependencies.

## Architecture

- Everything (HTML, CSS, JS) lives in the single `index.html` file:
  - `<style>` block: CSS custom properties defined in `:root` (`--primary`, `--secondary`, `--accent`, `--background`, `--text`, `--light-bg`, etc.) drive the color palette. Layout uses Flexbox/Grid with mobile-first breakpoints at `768px` and `992px`.
  - Body: sections in order — sticky nav, hero, "Why Choose Us" benefit cards, investment process timeline, testimonials, lead magnet, enquiry form, FAQ accordion, final CTA, footer.
  - `<script>` block (vanilla JS, no dependencies): sticky navbar on scroll, mobile menu toggle, `IntersectionObserver`-based scroll-reveal (`.fade-in` → `.visible`), FAQ accordion (single-open via `.faq-item.active` + `max-height` transition), and enquiry form validation/submission.

## Constraints

- No frameworks or libraries (no React/Vue/Angular/Bootstrap/Tailwind/jQuery) — keep all additions in vanilla HTML/CSS/JS within `index.html`.
- Hero/background imagery uses Unsplash URLs (`images.unsplash.com/...?auto=format&fit=crop&...`) — keep images optimized via Unsplash query params rather than adding local binary assets.
- Fonts are loaded from Google Fonts (`Playfair Display` for headings, `Inter` for body) via `<link>` tags in `<head>`.

## Enquiry Form (FormSubmit)

- The form posts to `https://formsubmit.co/<EMAIL>` (currently `tjr-84@hotmail.com`) with hidden fields `_subject`, `_captcha=false`, `_template=table`.
- Submission is intercepted via JS `fetch` (AJAX) with `Accept: application/json` so success/error messages render inline without a page redirect — do not remove `e.preventDefault()` or this AJAX handling when editing the form.
- Client-side validation regexes for email and phone live in the form-handling script; required fields are Name, Email, Phone.

## Testing/Running

There is no test suite or build step. To preview changes, open `index.html` directly in a browser (e.g. `Start-Process index.html` on Windows).
