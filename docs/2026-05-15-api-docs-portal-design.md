# AI API Documentation Portal — Design Spec

## 1. Overview
A single-page AI API documentation portal for **Claude Code** and **Hermes Agent**, inspired by Stripe's documentation design. Hosted as the main entry point for the APIWebSite project.

## 2. Architecture

### 2.1 Layout (Three-Column)
```
┌──────────────────────────────────────────────────────────────┐
│  Nav Bar: Logo | Theme Toggle | Version          (sticky)    │
├──────────┬──────────────────────────┬────────────────────────┤
│  LEFT    │       MAIN CONTENT       │     RIGHT CODE         │
│  SIDEBAR │       (scrollable)       │     (scrollable)       │
│          │                          │                        │
│  ☰ Toggle│  • Introduction          │  • Syntax-highlighted  │
│          │    Platform overview     │    code examples       │
│  Intro   │                          │                        │
│          │  • Claude Code           │  • Curl examples       │
│  Claude  │    - Quickstart          │  • Python examples     │
│  Code    │    - Installation        │  • JavaScript examples │
│          │    - Configuration       │  • YAML/JSON configs   │
│  Hermes  │    - CLI Reference       │                        │
│          │    - API Reference       │                        │
│          │                          │                        │
│          │  • Hermes                │                        │
│          │    - Quickstart          │                        │
│          │    - Installation        │                        │
│          │    - Configuration       │                        │
│          │    - Providers           │                        │
│          │    - CLI Reference       │                        │
│          │                          │                        │
├──────────┴──────────────────────────┴────────────────────────┤
│  Footer                                           (static)   │
└──────────────────────────────────────────────────────────────┘
```

### 2.2 File Structure
- Single file: `index.html` (all CSS/JS inline)
- Deployed to root of GitHub Pages

## 3. Visual Design

### 3.1 Color System
| Token | Dark Mode | Light Mode | Usage |
|-------|-----------|------------|-------|
| `--bg-primary` | `#0a0a0b` | `#ffffff` | Page background |
| `--bg-secondary` | `#141416` | `#f6f6f7` | Sidebar / code bg |
| `--bg-tertiary` | `#1c1c1f` | `#eeeef0` | Code blocks |
| `--text-primary` | `#f3f4f6` | `#1a1a2e` | Body text |
| `--text-secondary` | `#9ca3af` | `#6b7280` | Muted text |
| `--accent` | `#635BFF` | `#635BFF` | Links, highlights |
| `--accent-hover` | `#7c75ff` | `#7c75ff` | Hover states |
| `--border` | `#2a2a2e` | `#e5e7eb` | Dividers |

### 3.2 Typography
- System font stack: `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif`
- Mono: `'SF Mono', 'Fira Code', 'Cascadia Code', Consolas, monospace`
- Scale: 12/14/16/20/24/32px

### 3.3 Spacing
- Sidebar: 260px width, collapsible to 60px (icon-only)
- Code panel: 340px width
- Content: fluid remaining width, max 720px

## 4. Content Structure

### 4.1 Introduction
- Platform overview
- Ecosystem diagram (text-based)
- Quick comparison: Claude Code vs Hermes

### 4.2 Claude Code Section
- **Quickstart**: Install → Authenticate → First session
- **Installation**: Native installer, npm, platform-specific
- **Configuration**: settings.json hierarchy, env vars
- **CLI Reference**: All commands, flags, slash commands
- **API Reference**: Messages API, Agent SDK
- **Code Examples**: curl, Python, Node.js

### 4.3 Hermes Section
- **Quickstart**: Install → Configure → First session
- **Installation**: curl install, pip, Docker
- **Configuration**: config.yaml, .env, setup wizard
- **Providers**: 20+ provider configurations
- **CLI Reference**: Commands, gateway, tools
- **Code Examples**: YAML configs, API calls

## 5. Technical Implementation

### 5.1 Navigation
- Fixed left sidebar with smooth scroll (`scroll-behavior: smooth`)
- Active section tracking via IntersectionObserver
- Collapsible subsections via CSS transitions
- Mobile: sidebar slides in as overlay

### 5.2 Theme Toggle
- CSS custom properties for all colors
- `data-theme="dark|light"` on `<html>`
- Persisted in `localStorage`
- Smooth transition (300ms)

### 5.3 Syntax Highlighting
- Custom JS regex-based highlighter
- Token types: keywords, strings, comments, numbers, functions, operators
- Language auto-detection or manual class
- Fallback: plain text if JS disabled

### 5.4 Responsive Breakpoints
- `>1200px`: Full three-column
- `768-1200px`: Two-column (code panel below content)
- `<768px`: Single column, sidebar overlay, code inline

### 5.5 Performance
- Zero external requests
- `content-visibility: auto` on sections
- Debounced scroll handler
- Passive event listeners

## 6. Interactive Features
- **Code copy button**: Click to copy code block content
- **Anchor links**: `#section-id` deep linking
- **Active nav highlighting**: Current section in viewport
- **Collapsible sidebar subsections**: Toggle sub-items

## 7. Accessibility
- Semantic HTML: `<nav>`, `<main>`, `<aside>`, `<section>`
- ARIA labels on interactive elements
- Focus management for sidebar toggle
- `prefers-reduced-motion` support
- Keyboard navigation (Tab, Enter, Escape)

## 8. Out of Scope (v1)
- Search functionality
- Multi-language i18n
- API playground / interactive console
- PDF export
- Versioned documentation

---

## Implementation Plan

1. Create `index.html` with full HTML structure
2. Implement CSS (variables, layout, theme, responsive)
3. Implement JS (navigation, theme toggle, syntax highlighting, copy)
4. Add documentation content for Introduction, Claude Code, Hermes
5. Test responsive behavior and cross-browser
6. Deploy to GitHub Pages
