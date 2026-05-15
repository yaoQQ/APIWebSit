# AI API Documentation Portal — Implementation Plan

> **For agentic workers:** Single-file implementation. All tasks modify `index.html` at project root.

**Goal:** Build a complete AI API documentation portal (index.html) with three-column layout, dark/light theme, responsive design, and inline syntax highlighting — inspired by Stripe's documentation style.

**Architecture:** Single HTML file with inline `<style>` and `<script>`. CSS uses custom properties for theming, CSS Grid for layout, and media queries for responsiveness. JS handles theme toggle, sidebar behavior, IntersectionObserver-based nav highlighting, regex syntax highlighting, and code copy.

**Tech Stack:** Vanilla HTML5, CSS3 (Grid, Custom Properties, Transitions), Vanilla JavaScript (ES6+), system font stack. Zero external dependencies.

---

### Task 1: Create HTML Skeleton and All Content

**Files:**
- Create: `D:\claude-code-pro\APIWebSite\index.html`

- [ ] **Step 1: Write the full HTML structure with all content sections**

Create the complete HTML file with:
- Semantic HTML5 structure: `<header>`, `<nav>`, `<main>`, `<aside>`, `<section>`, `<footer>`
- All documentation content for Introduction, Claude Code, and Hermes
- Placeholder `<style>` and `<script>` blocks
- Data attributes for theming and navigation

The HTML structure:

```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AI API Documentation</title>
</head>
<body>
  <!-- Top Navigation Bar -->
  <header class="top-nav">
    <button class="sidebar-toggle" aria-label="Toggle sidebar">☰</button>
    <span class="logo">APIWebSit</span>
    <div class="nav-right">
      <button id="themeToggle" class="theme-toggle" aria-label="Toggle theme">
        <span class="icon-light">☀</span><span class="icon-dark">☾</span>
      </button>
      <span class="version">v1.0.0</span>
    </div>
  </header>

  <div class="layout">
    <!-- Left Sidebar Navigation -->
    <nav class="sidebar" id="sidebar" aria-label="Documentation navigation">
      <ul class="nav-list">
        <li><a href="#introduction" class="nav-link active">Introduction</a>
          <ul class="sub-nav">
            <li><a href="#overview" class="nav-link">Overview</a></li>
            <li><a href="#ecosystem" class="nav-link">Ecosystem</a></li>
          </ul>
        </li>
        <li><a href="#claude-code" class="nav-link">Claude Code</a>
          <ul class="sub-nav">
            <li><a href="#cc-quickstart" class="nav-link">Quickstart</a></li>
            <li><a href="#cc-installation" class="nav-link">Installation</a></li>
            <li><a href="#cc-configuration" class="nav-link">Configuration</a></li>
            <li><a href="#cc-cli" class="nav-link">CLI Reference</a></li>
            <li><a href="#cc-api" class="nav-link">API Reference</a></li>
          </ul>
        </li>
        <li><a href="#hermes" class="nav-link">Hermes</a>
          <ul class="sub-nav">
            <li><a href="#hermes-quickstart" class="nav-link">Quickstart</a></li>
            <li><a href="#hermes-installation" class="nav-link">Installation</a></li>
            <li><a href="#hermes-configuration" class="nav-link">Configuration</a></li>
            <li><a href="#hermes-providers" class="nav-link">Providers</a></li>
            <li><a href="#hermes-cli" class="nav-link">CLI Reference</a></li>
          </ul>
        </li>
      </ul>
    </nav>

    <!-- Main Content Area -->
    <main class="content" id="mainContent">
      <!-- Introduction Section -->
      <section id="introduction" class="doc-section">
        <h1>Introduction</h1>
        <section id="overview">
          <h2>Platform Overview</h2>
          <p>...</p>
        </section>
        <section id="ecosystem">
          <h2>Ecosystem</h2>
          <p>...</p>
        </section>
      </section>

      <!-- Claude Code Section -->
      <section id="claude-code" class="doc-section">
        <h1>Claude Code</h1>
        <!-- Sub-sections with full content -->
      </section>

      <!-- Hermes Section -->
      <section id="hermes" class="doc-section">
        <h1>Hermes</h1>
        <!-- Sub-sections with full content -->
      </section>
    </main>

    <!-- Right Code Panel -->
    <aside class="code-panel" id="codePanel">
      <div class="code-panel-header">
        <h3>Code Examples</h3>
      </div>
      <div class="code-examples" id="codeExamples">
        <!-- Dynamically populated -->
      </div>
    </aside>
  </div>

  <footer class="footer">
    <p>© 2026 APIWebSit. All rights reserved.</p>
  </footer>

  <style>/* ... */</style>
  <script>/* ... */</script>
</body>
</html>
```

- [ ] **Step 2: Write all documentation content for Introduction**

Write the Introduction section content including platform overview explaining this is a documentation portal for AI developer tools, and an ecosystem overview comparing Claude Code (Anthropic's agentic CLI) and Hermes (Nous Research's open-source self-improving agent).

- [ ] **Step 3: Write Claude Code full documentation**

Write complete Claude Code section with:
- **Quickstart**: Install with curl, set ANTHROPIC_API_KEY, run `claude`
- **Installation**: Native installer (macOS/Linux/WSL), Homebrew, npm (legacy), Windows PowerShell
- **Configuration**: settings.json hierarchy (5 levels), global config commands, key env vars (ANTHROPIC_API_KEY, ANTHROPIC_BASE_URL, CLAUDE_CODE_USE_BEDROCK=1, etc.)
- **CLI Reference**: All commands (claude, claude -p, claude -c, claude doctor, claude update, claude mcp, claude config), flags (--model, --allowedTools, --max-turns, --output-format), slash commands (/help, /config, /model, /compact, /plan, /review, /cost, etc.)
- **API Reference**: Messages API overview — POST https://api.anthropic.com/v1/messages with model, messages, system params; Agent SDK for Python and TypeScript

- [ ] **Step 4: Write Hermes full documentation**

Write complete Hermes section with:
- **Quickstart**: Install with curl, run setup wizard, start chatting
- **Installation**: curl installer, pip install, Docker/Railway deployment
- **Configuration**: ~/.hermes/config.yaml structure, .env for API keys, setup wizard (hermes setup), config commands
- **Providers**: 20+ providers table — Anthropic, OpenAI, OpenRouter, DeepSeek, Google Gemini, Ollama, LM Studio, AWS Bedrock, etc. with config examples for each
- **CLI Reference**: All commands — hermes, hermes model, hermes tools, hermes setup, hermes gateway, hermes mcp, hermes doctor, hermes logs, hermes update

- [ ] **Step 5: Add code examples with proper class attributes**

For each code block in the content, use:
```html
<pre><code class="language-bash">curl -fsSL https://claude.ai/install.sh | bash</code></pre>
<pre><code class="language-json">{"model": "claude-sonnet-4-6"}</code></pre>
<pre><code class="language-yaml">model:
  provider: "openrouter"
  default: "anthropic/claude-opus-4.6"</code></pre>
<pre><code class="language-python">import anthropic
client = anthropic.Anthropic(api_key="sk-ant-...")</code></pre>
<pre><code class="language-javascript">import Anthropic from '@anthropic-ai/sdk';
const client = new Anthropic({ apiKey: 'sk-ant-...' });</code></pre>
```

---

### Task 2: Implement Complete CSS

**Files:**
- Modify: `D:\claude-code-pro\APIWebSite\index.html` (style block)

- [ ] **Step 1: Write CSS custom properties and base styles**

```css
:root, [data-theme="dark"] {
  --bg-primary: #0a0a0b;
  --bg-secondary: #141416;
  --bg-tertiary: #1c1c1f;
  --text-primary: #f3f4f6;
  --text-secondary: #9ca3af;
  --accent: #635BFF;
  --accent-hover: #7c75ff;
  --accent-subtle: rgba(99, 91, 255, 0.1);
  --border: #2a2a2e;
  --code-bg: #1c1c1f;
  --sidebar-width: 260px;
  --code-panel-width: 340px;
  --top-nav-height: 48px;
}

[data-theme="light"] {
  --bg-primary: #ffffff;
  --bg-secondary: #f6f6f7;
  --bg-tertiary: #eeeef0;
  --text-primary: #1a1a2e;
  --text-secondary: #6b7280;
  --accent: #635BFF;
  --accent-hover: #5551d9;
  --accent-subtle: rgba(99, 91, 255, 0.08);
  --border: #e5e7eb;
  --code-bg: #f6f6f7;
}

* { margin: 0; padding: 0; box-sizing: border-box; }

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  background: var(--bg-primary);
  color: var(--text-primary);
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
  transition: background 0.3s, color 0.3s;
}

pre, code {
  font-family: 'SF Mono', 'Fira Code', 'Cascadia Code', Consolas, monospace;
}
```

- [ ] **Step 2: Write layout CSS (three-column grid)**

```css
.layout {
  display: grid;
  grid-template-columns: var(--sidebar-width) 1fr var(--code-panel-width);
  min-height: calc(100vh - var(--top-nav-height));
  margin-top: var(--top-nav-height);
}

/* Top Navigation */
.top-nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  height: var(--top-nav-height);
  background: var(--bg-secondary);
  border-bottom: 1px solid var(--border);
  display: flex;
  align-items: center;
  padding: 0 16px;
  z-index: 100;
  gap: 12px;
}

.top-nav .logo {
  font-weight: 600;
  font-size: 15px;
  color: var(--accent);
  letter-spacing: -0.01em;
}

.nav-right {
  margin-left: auto;
  display: flex;
  align-items: center;
  gap: 12px;
}

.version {
  font-size: 12px;
  color: var(--text-secondary);
  padding: 2px 8px;
  border: 1px solid var(--border);
  border-radius: 4px;
}
```

- [ ] **Step 3: Write sidebar navigation CSS**

```css
.sidebar {
  position: fixed;
  top: var(--top-nav-height);
  left: 0;
  width: var(--sidebar-width);
  height: calc(100vh - var(--top-nav-height));
  overflow-y: auto;
  background: var(--bg-secondary);
  border-right: 1px solid var(--border);
  padding: 20px 0;
  z-index: 90;
  transition: transform 0.3s, width 0.3s;
}

.sidebar-toggle {
  background: none;
  border: none;
  color: var(--text-secondary);
  font-size: 20px;
  cursor: pointer;
  padding: 4px;
  line-height: 1;
}

.nav-list { list-style: none; padding: 0; margin: 0; }
.nav-list > li { margin-bottom: 4px; }
.nav-link {
  display: block;
  padding: 6px 20px;
  color: var(--text-secondary);
  text-decoration: none;
  font-size: 13px;
  transition: all 0.15s;
  border-left: 2px solid transparent;
}
.nav-link:hover { color: var(--text-primary); }
.nav-link.active {
  color: var(--accent);
  border-left-color: var(--accent);
  background: var(--accent-subtle);
}

.sub-nav { list-style: none; padding-left: 0; margin: 0; display: none; }
.sub-nav.open { display: block; }
.sub-nav .nav-link {
  padding: 4px 20px 4px 32px;
  font-size: 12px;
}
```

- [ ] **Step 4: Write main content area CSS**

```css
.content {
  grid-column: 2;
  padding: 40px 48px;
  max-width: 720px;
  width: 100%;
}

.content h1 {
  font-size: 32px;
  font-weight: 700;
  margin-bottom: 24px;
  letter-spacing: -0.02em;
}
.content h2 {
  font-size: 24px;
  font-weight: 600;
  margin: 32px 0 12px;
  letter-spacing: -0.01em;
}
.content h3 {
  font-size: 18px;
  font-weight: 600;
  margin: 24px 0 8px;
}
.content p { margin-bottom: 16px; color: var(--text-secondary); }
.content ul, .content ol { margin: 8px 0 16px 20px; color: var(--text-secondary); }
.content li { margin-bottom: 4px; }

.content table {
  width: 100%;
  border-collapse: collapse;
  margin: 16px 0;
  font-size: 13px;
}
.content th, .content td {
  padding: 8px 12px;
  border: 1px solid var(--border);
  text-align: left;
}
.content th {
  background: var(--bg-secondary);
  font-weight: 600;
  color: var(--text-primary);
}
.content td { color: var(--text-secondary); }

.content a {
  color: var(--accent);
  text-decoration: none;
}
.content a:hover { text-decoration: underline; }

.doc-section {
  scroll-margin-top: calc(var(--top-nav-height) + 16px);
}
```

- [ ] **Step 5: Write code blocks CSS**

```css
.content pre {
  background: var(--code-bg);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 16px;
  margin: 16px 0;
  overflow-x: auto;
  font-size: 13px;
  line-height: 1.5;
  position: relative;
}

.content code {
  font-size: 0.9em;
  padding: 2px 6px;
  background: var(--bg-tertiary);
  border-radius: 4px;
}
.content pre code {
  background: none;
  padding: 0;
  border-radius: 0;
}

.code-panel {
  position: fixed;
  top: var(--top-nav-height);
  right: 0;
  width: var(--code-panel-width);
  height: calc(100vh - var(--top-nav-height));
  overflow-y: auto;
  background: var(--bg-secondary);
  border-left: 1px solid var(--border);
  padding: 20px;
}

.code-panel-header h3 {
  font-size: 13px;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--text-secondary);
  margin-bottom: 16px;
}

.code-panel pre {
  background: var(--code-bg);
  border: 1px solid var(--border);
  border-radius: 6px;
  padding: 12px;
  margin-bottom: 16px;
  font-size: 12px;
  overflow-x: auto;
  position: relative;
}

.copy-btn {
  position: absolute;
  top: 6px; right: 6px;
  background: var(--bg-tertiary);
  border: 1px solid var(--border);
  color: var(--text-secondary);
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 11px;
  cursor: pointer;
  opacity: 0;
  transition: opacity 0.15s;
}
pre:hover .copy-btn { opacity: 1; }
```

- [ ] **Step 6: Write syntax highlighting CSS classes**

```css
.hl-keyword { color: #ff79c6; }
.hl-string { color: #f1fa8c; }
.hl-number { color: #bd93f9; }
.hl-comment { color: #6272a4; font-style: italic; }
.hl-function { color: #50fa7b; }
.hl-operator { color: #ff79c6; }
.hl-builtin { color: #8be9fd; }
.hl-property { color: #66d9ef; }
.hl-punctuation { color: #f8f8f2; }

[data-theme="light"] .hl-keyword { color: #d63384; }
[data-theme="light"] .hl-string { color: #198038; }
[data-theme="light"] .hl-number { color: #7c3aed; }
[data-theme="light"] .hl-comment { color: #a0a0a0; }
[data-theme="light"] .hl-function { color: #0066cc; }
[data-theme="light"] .hl-operator { color: #d63384; }
[data-theme="light"] .hl-builtin { color: #0099b3; }
[data-theme="light"] .hl-property { color: #0099b3; }
[data-theme="light"] .hl-punctuation { color: #333333; }
```

- [ ] **Step 7: Write responsive CSS**

```css
/* Tablet: hide code panel, show inline */
@media (max-width: 1200px) {
  .layout {
    grid-template-columns: var(--sidebar-width) 1fr;
  }
  .code-panel {
    display: none;
  }
  .content {
    max-width: 100%;
  }
  .code-examples-inline {
    display: block;
  }
}

/* Mobile: single column, overlay sidebar */
@media (max-width: 768px) {
  .layout {
    grid-template-columns: 1fr;
  }
  .sidebar {
    transform: translateX(-100%);
  }
  .sidebar.open {
    transform: translateX(0);
  }
  .content {
    padding: 24px 16px;
  }
  .content h1 { font-size: 26px; }
  .content h2 { font-size: 20px; }
}

@media (min-width: 1201px) {
  .code-examples-inline { display: none; }
}
```

---

### Task 3: Implement Complete JavaScript

**Files:**
- Modify: `D:\claude-code-pro\APIWebSite\index.html` (script block)

- [ ] **Step 1: Write theme toggle JS**

```javascript
(function() {
  'use strict';

  // Theme toggle
  const themeToggle = document.getElementById('themeToggle');
  const html = document.documentElement;
  const savedTheme = localStorage.getItem('theme') || 'dark';
  html.setAttribute('data-theme', savedTheme);

  themeToggle.addEventListener('click', () => {
    const current = html.getAttribute('data-theme');
    const next = current === 'dark' ? 'light' : 'dark';
    html.setAttribute('data-theme', next);
    localStorage.setItem('theme', next);
  });
})();
```

- [ ] **Step 2: Write sidebar toggle and navigation JS**

```javascript
  // Sidebar toggle
  const sidebarToggle = document.querySelector('.sidebar-toggle');
  const sidebar = document.getElementById('sidebar');
  let sidebarOpen = true;

  sidebarToggle.addEventListener('click', () => {
    if (window.innerWidth > 768) {
      sidebarOpen = !sidebarOpen;
      sidebar.style.width = sidebarOpen ? 'var(--sidebar-width)' : '0';
      sidebar.style.overflow = sidebarOpen ? 'auto' : 'hidden';
      sidebar.style.padding = sidebarOpen ? '20px 0' : '0';
    } else {
      sidebar.classList.toggle('open');
    }
  });

  // Collapsible sub-nav
  document.querySelectorAll('.nav-list > li > a').forEach(link => {
    const sub = link.nextElementSibling;
    if (sub && sub.classList.contains('sub-nav')) {
      link.addEventListener('click', (e) => {
        e.preventDefault();
        sub.classList.toggle('open');
        const href = link.getAttribute('href');
        if (href && sub.classList.contains('open')) {
          document.querySelector(href)?.scrollIntoView({ behavior: 'smooth' });
        }
      });
      // Auto-open if hash matches
      if (window.location.hash && link.getAttribute('href') === window.location.hash.split('-')[0]) {
        sub.classList.add('open');
      }
    }
  });
```

- [ ] **Step 3: Write IntersectionObserver for active nav**

```javascript
  // Active section tracking
  const sections = document.querySelectorAll('.doc-section');
  const navLinks = document.querySelectorAll('.nav-link');

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const id = entry.target.id;
        navLinks.forEach(link => {
          link.classList.toggle('active', link.getAttribute('href') === '#' + id);
        });
      }
    });
  }, { rootMargin: '-80px 0px -60% 0px' });

  sections.forEach(s => observer.observe(s));
```

- [ ] **Step 4: Write syntax highlighter JS**

```javascript
  // Regex-based syntax highlighter
  function highlightCode(code, lang) {
    const patterns = {
      bash: [
        { pattern: /(# .*)/g, class: 'hl-comment' },
        { pattern: /(\b(export|echo|cd|curl|npm|brew|pip|docker|git|source|alias|sudo|yay)\b)/g, class: 'hl-builtin' },
        { pattern: /("(?:[^"\\]|\\.)*"|'(?:[^'\\]|\\.)*')/g, class: 'hl-string' },
        { pattern: /(\$[A-Z_]+)/g, class: 'hl-keyword' },
      ],
      json: [
        { pattern: /("(?:[^"\\]|\\.)*")\s*:/g, class: 'hl-property' },
        { pattern: /("(?:[^"\\]|\\.)*")/g, class: 'hl-string' },
        { pattern: /\b(-?\d+(?:\.\d+)?)\b/g, class: 'hl-number' },
        { pattern: /\b(true|false|null)\b/g, class: 'hl-keyword' },
      ],
      yaml: [
        { pattern: /(# .*)/g, class: 'hl-comment' },
        { pattern: /^(\s*[\w-]+)(?=:)/gm, class: 'hl-property' },
        { pattern: /("(?:[^"\\]|\\.)*"|'(?:[^'\\]|\\.)*')/g, class: 'hl-string' },
        { pattern: /\b(true|false|null)\b/g, class: 'hl-keyword' },
      ],
      python: [
        { pattern: /(# .*|"""(?:[^"]|"(?!""))*(?:"""|$))/g, class: 'hl-comment' },
        { pattern: /\b(import|from|def|class|return|if|elif|else|for|while|in|not|and|or|as|with|try|except|raise|print|async|await|True|False|None)\b/g, class: 'hl-keyword' },
        { pattern: /("(?:[^"\\]|\\.)*"|'(?:[^'\\]|\\.)*')/g, class: 'hl-string' },
        { pattern: /\b(-?\d+(?:\.\d+)?)\b/g, class: 'hl-number' },
        { pattern: /(\b[A-Za-z_]\w*)\s*\(/g, class: 'hl-function' },
      ],
      javascript: [
        { pattern: /(\/\/.*|\/\*[\s\S]*?\*\/)/g, class: 'hl-comment' },
        { pattern: /\b(import|from|export|const|let|var|function|return|if|else|for|of|in|async|await|new|try|catch|throw|class|extends|true|false|null|undefined)\b/g, class: 'hl-keyword' },
        { pattern: /("(?:[^"\\]|\\.)*"|'(?:[^'\\]|\\.)*'|`(?:[^`\\]|\\.)*`)/g, class: 'hl-string' },
        { pattern: /\b(-?\d+(?:\.\d+)?)\b/g, class: 'hl-number' },
        { pattern: /(\b[A-Za-z_]\w*)\s*\(/g, class: 'hl-function' },
      ],
    };

    const rules = patterns[lang] || patterns.bash;
    let result = code;
    for (const rule of rules) {
      result = result.replace(rule.pattern, (match, ...args) => {
        return `<span class="${rule.class}">${match}</span>`;
      });
    }
    return result;
  }

  // Apply highlighting to all code blocks
  document.querySelectorAll('pre code[class*="language-"]').forEach(block => {
    const lang = block.className.replace('language-', '');
    const code = block.textContent;
    block.innerHTML = highlightCode(code, lang);
  });
```

- [ ] **Step 5: Write copy button JS**

```javascript
  // Copy buttons
  document.querySelectorAll('.content pre').forEach(pre => {
    const btn = document.createElement('button');
    btn.className = 'copy-btn';
    btn.textContent = 'Copy';
    btn.addEventListener('click', async () => {
      const code = pre.querySelector('code')?.textContent || pre.textContent;
      try {
        await navigator.clipboard.writeText(code);
        btn.textContent = 'Copied!';
        setTimeout(() => { btn.textContent = 'Copy'; }, 2000);
      } catch {
        btn.textContent = 'Failed';
      }
    });
    pre.appendChild(btn);
  });
```

- [ ] **Step 6: Write smooth scroll and hash handling**

```javascript
  // Smooth scroll for nav links
  document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function(e) {
      const href = this.getAttribute('href');
      const target = document.querySelector(href);
      if (target) {
        e.preventDefault();
        target.scrollIntoView({ behavior: 'smooth' });
        history.pushState(null, '', href);
      }
    });
  });
})();
```

---

### Task 4: Testing and Deployment

**Files:**
- Test: `D:\claude-code-pro\APIWebSite\index.html`

- [ ] **Step 1: Open index.html in browser and verify layout**

Open file:///D:/claude-code-pro/APIWebSite/index.html and check:
- Three-column layout renders correctly
- Sidebar navigation displays all sections
- Main content area shows documentation text
- Code panel shows code examples

- [ ] **Step 2: Test dark/light theme toggle**

- Click theme toggle button
- Verify dark → light → dark transition works
- Verify color changes are smooth
- Refresh page and verify theme persists from localStorage

- [ ] **Step 3: Test sidebar navigation**

- Click navigation items and verify smooth scroll
- Verify active state highlights correctly
- Test collapsible subsections
- Test sidebar toggle (collapse/expand)

- [ ] **Step 4: Test responsive layout**

- Resize browser to < 1200px: verify code panel disappears, inline code examples appear
- Resize to < 768px: verify sidebar becomes overlay, single column layout
- Verify no horizontal scrollbars at any breakpoint

- [ ] **Step 5: Test syntax highlighting and copy**

- Verify all code blocks have colored syntax tokens
- Click copy button on any code block
- Verify "Copied!" feedback appears
- Paste clipboard to verify correct content was copied

- [ ] **Step 6: Commit and deploy**

```bash
git add index.html
git commit -m "feat: add AI API documentation portal page

- Three-column Stripe-inspired layout with collapsible sidebar
- Dark/light theme toggle with localStorage persistence
- Responsive design (desktop/tablet/mobile breakpoints)
- Regex-based inline syntax highlighting (bash, json, yaml, python, javascript)
- Real documentation content for Claude Code and Hermes Agent
- Zero external dependencies, single HTML file"
git push
```
