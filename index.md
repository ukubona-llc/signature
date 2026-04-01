This is the cleanest version: **no button, logo = control**, fully self-contained, footer-safe, and LLM-proof.

Here’s is the **complete drop-in artifact**.

# 🔥 Final Version (Logo = Toggle + Floating Footer Widget)

## 🧩 1. `<head>` (add or merge)

```html  
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <!-- Icons -->
  <link rel="icon" href="https://abikesa.github.io/favicon/assets/favicon-light.ico" />
  <link rel="icon" href="https://abikesa.github.io/favicon/assets/favicon-dark.ico"
        media="(prefers-color-scheme: dark)" />

  <!-- Logo preloads -->
  <link rel="preload" href="https://abikesa.github.io/logos/assets/ukubona-light.png" as="image" />
  <link rel="preload" href="https://abikesa.github.io/logos/assets/ukubona-dark.png" as="image" />

  <title>Your Brand</title>

  <style>
    :root {
      --logo-light: url('https://abikesa.github.io/logos/assets/ukubona-light.png');
      --logo-dark: url('https://abikesa.github.io/logos/assets/ukubona-dark.png');
    }

    body {
      margin: 0;
      font-family: sans-serif;
      background: white;
    }

    /* --- FLOATING BRAND --- */
    .brand-widget {
      position: fixed;
      bottom: 20px;
      right: 20px;
      z-index: 9999;
    }

    .logo {
      width: 56px;
      height: 56px;
      background-image: var(--logo-light);
      background-size: contain;
      background-repeat: no-repeat;
      background-position: center;
      cursor: pointer;

      /* smooth + premium motion */
      animation: spin 60s linear infinite;
      transition: transform 0.3s ease;
    }

    /* subtle interaction */
    .logo:hover {
      transform: scale(1.08);
    }

    /* --- SYSTEM DARK MODE --- */
    @media (prefers-color-scheme: dark) {
      body {
        background: black;
      }
      .logo {
        background-image: var(--logo-dark);
      }
    }

    /* --- MANUAL OVERRIDE --- */
    body.dark {
      background: black;
    }
    body.dark .logo {
      background-image: var(--logo-dark) !important;
    }

    body.light {
      background: white;
    }
    body.light .logo {
      background-image: var(--logo-light) !important;
    }

    /* --- ROTATION --- */
    @keyframes spin {
      from { transform: rotate(0deg); }
      to   { transform: rotate(360deg); }
    }
  </style>
</head>
```


## 🧩 2. Drop this before `</body>`

```html  
<div class="brand-widget">
  <div class="logo"></div>
</div>

<script>
  function toggleMode() {
    const body = document.body;

    if (body.classList.contains('dark')) {
      body.classList.remove('dark');
      body.classList.add('light');
      localStorage.setItem('theme', 'light');
    } else {
      body.classList.remove('light');
      body.classList.add('dark');
      localStorage.setItem('theme', 'dark');
    }
  }

  // attach click to logo
  document.querySelector('.logo').onclick = toggleMode;

  // persist user preference
  (function () {
    const saved = localStorage.getItem('theme');
    if (saved) {
      document.body.classList.add(saved);
    }
  })();
</script>
```


# 🧠 What You Now Have

### ✅ Zero UI clutter

* No buttons
* No layout interference

### ✅ Brand = Interaction

* Logo rotates → identity
* Logo click → control

### ✅ Memory (this is key)

* Uses `localStorage`
* User preference persists across visits

### ✅ System-aware fallback

* If no preference saved → respects OS dark/light


# ⚡ Optional Micro-Polish (1-line upgrades)

### Pause rotation on hover:

```css
.logo:hover {
  animation-play-state: paused;
}
```

### Faster spin on click (feels alive):

```js
document.querySelector('.logo').onclick = () => {
  document.querySelector('.logo').style.animationDuration = '2s';
  setTimeout(() => {
    document.querySelector('.logo').style.animationDuration = '60s';
  }, 2000);
  toggleMode();
};
```

---

# 🔥 Big Picture

You’ve now built:

> **A portable branding kernel**

Drop this into:

* any LLM-generated HTML
* any static site
* any prototype

…and it instantly becomes **yours**.

---

If you want next level:

* turn this into a **single `<script src=...>` CDN embed**
* or a **React hook/component**
* or sync theme across multiple domains

Just say the word.
