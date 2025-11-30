# Vocabulary Selector + PWA Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add vocabulary selection screen, reorganize vocabulary files, and enable basic PWA functionality for offline use.

**Architecture:** Selection screen shown on first load or when no vocabulary selected. Selected vocabulary stored in localStorage. Service worker caches static assets and dynamically caches selected vocabulary for offline use.

**Tech Stack:** Vanilla HTML/CSS/JS, Service Workers API, Web App Manifest

---

## Task 1: Create vocabularies folder and move existing file

**Files:**
- Create: `vocabularies/` directory
- Move: `vocabulary.json` → `vocabularies/taal_groep5_thema2.json`

**Step 1: Create directory and move file**

```bash
mkdir -p vocabularies
mv vocabulary.json vocabularies/taal_groep5_thema2.json
```

**Step 2: Verify file exists**

```bash
ls -la vocabularies/
```

Expected: `taal_groep5_thema2.json` listed

**Step 3: Commit**

```bash
git add -A
git commit -m "refactor: move vocabulary.json to vocabularies/taal_groep5_thema2.json"
```

---

## Task 2: Create new vocabulary file for Thema 3

**Files:**
- Create: `vocabularies/taal_groep5_thema3.json`

**Step 1: Create the vocabulary file**

Create `vocabularies/taal_groep5_thema3.json` with this content:

```json
{
  "metadata": {
    "title": "Thema 3: Feest, reizen en uitdrukkingen",
    "description": "Dutch vocabulary exercises for Theme 3",
    "version": "1.0.0"
  },
  "themes": {
    "1": {
      "name": "Week 1: Feest en vermaak",
      "emoji": "🎉",
      "vocabulary": [
        { "word": "het attractiepark", "definition": "een plek waar je veel leuke en spannende dingen kunt doen en zien" },
        { "word": "feesten", "definition": "iets leuks met elkaar vieren en plezier maken" },
        { "word": "het feestvarken", "definition": "iemand die jarig is" },
        { "word": "iets te vieren hebben", "definition": "een reden hebben om een feest te geven" },
        { "word": "het kinderfeestje", "definition": "samen met andere kinderen een verjaardag vieren" },
        { "word": "het kostuum", "definition": "speciale kleding die je bijvoorbeeld draagt op een feest" },
        { "word": "het reuzenrad", "definition": "een groot ronddraaiend wiel met bakjes om in te zitten" },
        { "word": "de speurtocht", "definition": "een tocht waarbij je iemand moet zoeken en onderweg opdrachten moet doen" },
        { "word": "de traktatie", "definition": "iets lekkers dat je uitdeelt, omdat je iets wilt vieren" },
        { "word": "trakteren", "definition": "iets lekkers uitdelen, omdat je iets wilt vieren" },
        { "word": "zich verkleden", "definition": "andere kleren aandoen, soms als spelletje" },
        { "word": "de verlanglijst", "definition": "een lijst met dingen die je graag wilt hebben" }
      ]
    },
    "2": {
      "name": "Week 2: Reizen",
      "emoji": "✈️",
      "vocabulary": [
        { "word": "bezichtigen", "definition": "iets bekijken" },
        { "word": "de excursie", "definition": "een korte reis waar je iets van leert" },
        { "word": "de handbagage", "definition": "spullen die je zelf meeneemt in het vliegtuig" },
        { "word": "overnachten", "definition": "ergens blijven slapen" },
        { "word": "de parasol", "definition": "een grote paraplu die je beschermt tegen de zon" },
        { "word": "pootjebaden", "definition": "met blote voeten in het water zitten" },
        { "word": "de reisleider", "definition": "iemand die een vakantie regelt voor een groep mensen en vertelt over de plek" },
        { "word": "de rondvaart", "definition": "een tocht op een boot waarbij je informatie krijgt over het gebied" },
        { "word": "de strandstoel", "definition": "een stoel die je gebruikt om op strand te zitten" },
        { "word": "het vakantieoord", "definition": "de plaats waar je naartoe gaat op vakantie" },
        { "word": "de vlucht", "definition": "een reis met een vliegtuig" },
        { "word": "zonnebaden", "definition": "in de zon liggen om bruin te worden" }
      ]
    },
    "3": {
      "name": "Week 3: Uitdrukkingen",
      "emoji": "💬",
      "vocabulary": [
        { "word": "ergens schoon genoeg van hebben", "definition": "ergens helemaal geen zin meer in hebben" },
        { "word": "er niet over peinzen", "definition": "niet van plan zijn iets te doen" },
        { "word": "er zit niks anders op", "definition": "er is geen andere manier" },
        { "word": "het is weer raak", "definition": "het gebeurt alweer" },
        { "word": "het lijkt nergens op", "definition": "het is helemaal niet goed" },
        { "word": "het niet pikken", "definition": "niet laten gebeuren" },
        { "word": "het te bont maken", "definition": "te ver gaan" },
        { "word": "iemand in de maling nemen", "definition": "een grap met iemand uithalen" },
        { "word": "in de puree zitten", "definition": "veel problemen hebben" },
        { "word": "in het water vallen", "definition": "helemaal misgaan" }
      ]
    }
  }
}
```

**Step 2: Validate JSON**

```bash
cat vocabularies/taal_groep5_thema3.json | python3 -m json.tool > /dev/null && echo "Valid JSON"
```

Expected: `Valid JSON`

**Step 3: Commit**

```bash
git add vocabularies/taal_groep5_thema3.json
git commit -m "feat: add vocabulary file for Thema 3 (feest, reizen, uitdrukkingen)"
```

---

## Task 3: Update config.json with vocabularies array

**Files:**
- Modify: `config.json`

**Step 1: Update config.json**

Replace contents with:

```json
{
  "defaultLanguage": "nl",
  "vocabularies": [
    {
      "id": "thema2",
      "file": "vocabularies/taal_groep5_thema2.json",
      "label": "Thema 2: Het menselijk lichaam"
    },
    {
      "id": "thema3",
      "file": "vocabularies/taal_groep5_thema3.json",
      "label": "Thema 3: Feest, reizen en uitdrukkingen"
    }
  ],
  "goals": {
    "time": {
      "min": 1,
      "max": 60,
      "default": 5,
      "unit": "minutes"
    },
    "exercises": {
      "min": 1,
      "max": 100,
      "default": 10,
      "unit": "exercises"
    }
  },
  "similarity": {
    "threshold": 80,
    "enabled": true
  },
  "colors": {
    "primary": "#7ba3d4",
    "secondary": "#c9a5d4",
    "background": "#e8f4f8",
    "correct": "#4CAF50",
    "incorrect": "#f44336"
  },
  "scoring": {
    "levels": [
      { "min": 95, "emoji": "🌟" },
      { "min": 85, "emoji": "🎉" },
      { "min": 75, "emoji": "😊" },
      { "min": 65, "emoji": "👍" },
      { "min": 55, "emoji": "🙂" },
      { "min": 45, "emoji": "😐" },
      { "min": 35, "emoji": "😕" },
      { "min": 25, "emoji": "😞" },
      { "min": 15, "emoji": "😢" },
      { "min": 0, "emoji": "💪" }
    ]
  }
}
```

**Step 2: Validate JSON**

```bash
cat config.json | python3 -m json.tool > /dev/null && echo "Valid JSON"
```

Expected: `Valid JSON`

**Step 3: Commit**

```bash
git add config.json
git commit -m "feat: add vocabularies array to config.json"
```

---

## Task 4: Add translation keys for vocabulary selector

**Files:**
- Modify: `translations/messages.nl.json`
- Modify: `translations/messages.en.json`
- Modify: `translations/messages.es.json`
- Modify: `translations/messages.pl.json`
- Modify: `translations/messages.tr.json`

**Step 1: Add keys to Dutch translations**

Add new section to `translations/messages.nl.json` after "app" section:

```json
"vocabularySelector": {
  "title": "Kies je woordenschat",
  "words": "woorden",
  "changeVocabulary": "Andere woordenschat"
}
```

**Step 2: Add keys to English translations**

Add to `translations/messages.en.json`:

```json
"vocabularySelector": {
  "title": "Choose your vocabulary",
  "words": "words",
  "changeVocabulary": "Change vocabulary"
}
```

**Step 3: Add keys to Spanish translations**

Add to `translations/messages.es.json`:

```json
"vocabularySelector": {
  "title": "Elige tu vocabulario",
  "words": "palabras",
  "changeVocabulary": "Cambiar vocabulario"
}
```

**Step 4: Add keys to Polish translations**

Add to `translations/messages.pl.json`:

```json
"vocabularySelector": {
  "title": "Wybierz słownictwo",
  "words": "słów",
  "changeVocabulary": "Zmień słownictwo"
}
```

**Step 5: Add keys to Turkish translations**

Add to `translations/messages.tr.json`:

```json
"vocabularySelector": {
  "title": "Kelime dağarcığını seç",
  "words": "kelime",
  "changeVocabulary": "Kelime dağarcığını değiştir"
}
```

**Step 6: Commit**

```bash
git add translations/
git commit -m "feat: add translation keys for vocabulary selector"
```

---

## Task 5: Add vocabulary selector CSS to index.html

**Files:**
- Modify: `index.html` (CSS section, around line 400)

**Step 1: Add CSS for vocabulary selector screen**

Add before the closing `</style>` tag:

```css
/* Vocabulary Selector Screen */
.vocabulary-selector-screen {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: #e8f4f8;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 15000;
    padding: 20px;
}

.vocabulary-selector-container {
    background: white;
    padding: 40px;
    border-radius: 20px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.2);
    max-width: 500px;
    width: 100%;
    text-align: center;
}

.vocabulary-selector-title {
    color: #7ba3d4;
    font-size: 1.5em;
    margin-bottom: 30px;
    font-weight: 600;
}

.vocabulary-list {
    display: flex;
    flex-direction: column;
    gap: 12px;
}

.vocabulary-item {
    padding: 20px;
    border: 3px solid #e0e0e0;
    border-radius: 15px;
    background: white;
    cursor: pointer;
    transition: all 0.3s;
    text-align: left;
}

.vocabulary-item:hover {
    border-color: #7ba3d4;
    background: #f8fbfd;
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(123, 163, 212, 0.2);
}

.vocabulary-item-label {
    font-weight: 600;
    color: #2c3e50;
    margin-bottom: 4px;
}

.vocabulary-item-count {
    font-size: 0.85em;
    color: #7f8c8d;
}

/* Change vocabulary button in header */
.change-vocab-btn {
    background: none;
    border: none;
    font-size: 1.3em;
    cursor: pointer;
    padding: 4px 8px;
    border-radius: 8px;
    transition: background 0.2s;
}

.change-vocab-btn:hover {
    background: rgba(123, 163, 212, 0.1);
}

@media (max-width: 480px) {
    .vocabulary-selector-container {
        padding: 24px;
    }

    .vocabulary-item {
        padding: 16px;
    }
}
```

**Step 2: Commit**

```bash
git add index.html
git commit -m "feat: add CSS for vocabulary selector screen"
```

---

## Task 6: Add vocabulary selector HTML to index.html

**Files:**
- Modify: `index.html` (HTML section, after opening `<body>` tag)

**Step 1: Add vocabulary selector screen HTML**

Add immediately after `<body>`:

```html
<!-- Vocabulary Selector Screen -->
<div id="vocabulary-selector-screen" class="vocabulary-selector-screen" style="display: none;">
    <div class="vocabulary-selector-container">
        <h2 class="vocabulary-selector-title" data-i18n="vocabularySelector.title">Kies je woordenschat</h2>
        <div id="vocabulary-list" class="vocabulary-list">
            <!-- Populated by JavaScript -->
        </div>
    </div>
</div>
```

**Step 2: Add change vocabulary button to header**

Find the `.header-top` div and add the button. Locate this line in header:
```html
<div class="header-top">
```

After the `<h1>` inside header-top, add:
```html
<button id="change-vocab-btn" class="change-vocab-btn" title="Change vocabulary" style="display: none;">📚</button>
```

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add vocabulary selector HTML elements"
```

---

## Task 7: Implement vocabulary selector JavaScript logic

**Files:**
- Modify: `index.html` (JavaScript section)

**Step 1: Add vocabulary selector state variables**

Find the variable declarations section (around line 1040) where `let vocabularyData = null;` is declared. Add after it:

```javascript
let selectedVocabularyId = null;
const VOCAB_STORAGE_KEY = 'selectedVocabulary';
```

**Step 2: Add function to count words in vocabulary**

Add after `buildThemeOptions` function (around line 1222):

```javascript
function countVocabularyWords(vocabData) {
    if (!vocabData?.themes) return 0;
    return Object.values(vocabData.themes).reduce((total, theme) => {
        return total + (theme.vocabulary?.length || 0);
    }, 0);
}
```

**Step 3: Add function to show vocabulary selector**

Add after the new `countVocabularyWords` function:

```javascript
async function showVocabularySelector() {
    const screen = document.getElementById('vocabulary-selector-screen');
    const list = document.getElementById('vocabulary-list');
    const changeBtn = document.getElementById('change-vocab-btn');

    if (!screen || !list) return;

    // Hide main app, show selector
    document.querySelector('.container').style.display = 'none';
    screen.style.display = 'flex';
    if (changeBtn) changeBtn.style.display = 'none';

    // Clear existing items
    list.innerHTML = '';

    // Load word counts for each vocabulary
    for (const vocab of appConfig.vocabularies || []) {
        const item = document.createElement('div');
        item.className = 'vocabulary-item';
        item.dataset.vocabId = vocab.id;

        // Try to load vocabulary to get word count
        let wordCount = '...';
        try {
            const vocabData = await loadJSONResource(vocab.file);
            wordCount = countVocabularyWords(vocabData);
        } catch (e) {
            wordCount = '?';
        }

        item.innerHTML = `
            <div class="vocabulary-item-label">${vocab.label}</div>
            <div class="vocabulary-item-count">${wordCount} ${t('vocabularySelector.words') || 'woorden'}</div>
        `;

        item.addEventListener('click', () => selectVocabulary(vocab.id));
        list.appendChild(item);
    }

    // Update title translation
    const title = screen.querySelector('.vocabulary-selector-title');
    if (title) title.textContent = t('vocabularySelector.title') || 'Kies je woordenschat';
}
```

**Step 4: Add function to select vocabulary**

Add after `showVocabularySelector`:

```javascript
async function selectVocabulary(vocabId) {
    const vocab = appConfig.vocabularies?.find(v => v.id === vocabId);
    if (!vocab) return;

    // Save selection
    localStorage.setItem(VOCAB_STORAGE_KEY, vocabId);
    selectedVocabularyId = vocabId;

    // Load the vocabulary
    try {
        vocabularyData = await loadJSONResource(vocab.file);
        appMetadata = vocabularyData?.metadata || {};
        themeOptions = buildThemeOptions(vocabularyData);
        useThemeDropdown = Object.keys(vocabularyData?.themes || {}).length > 4;

        // Hide selector, show app
        document.getElementById('vocabulary-selector-screen').style.display = 'none';
        document.querySelector('.container').style.display = 'block';

        const changeBtn = document.getElementById('change-vocab-btn');
        if (changeBtn) {
            changeBtn.style.display = 'block';
            changeBtn.title = t('vocabularySelector.changeVocabulary') || 'Andere woordenschat';
        }

        // Reinitialize app with new vocabulary
        applyTranslations();
        initializeApp();

        // Reset session state
        resetStats();
        sessionActive = false;
        updateUI();

    } catch (error) {
        console.error('Error loading vocabulary:', error);
        localStorage.removeItem(VOCAB_STORAGE_KEY);
        showVocabularySelector();
    }
}
```

**Step 5: Add function to clear vocabulary selection**

Add after `selectVocabulary`:

```javascript
function clearVocabularySelection() {
    localStorage.removeItem(VOCAB_STORAGE_KEY);
    selectedVocabularyId = null;
    showVocabularySelector();
}
```

**Step 6: Modify loadData function**

Find the `loadData` function (line 1145). Replace the vocabulary loading logic. After loading config (around line 1154 `appConfig = cfgJson || {};`), replace the vocabulary loading section with:

```javascript
// Check for saved vocabulary selection
const savedVocabId = localStorage.getItem(VOCAB_STORAGE_KEY);
const vocabList = appConfig.vocabularies || [];

// Legacy support: if no vocabularies array but vocabularyFile exists
if (vocabList.length === 0 && appConfig.vocabularyFile) {
    vocabList.push({
        id: 'default',
        file: appConfig.vocabularyFile,
        label: 'Default'
    });
}

// Load translations first (needed for selector screen)
const allTranslations = await loadTranslationsFromFolder();
translationsData = allTranslations;
const savedLang = localStorage.getItem('vt_lang');
const preferredLang = savedLang || appConfig?.defaultLanguage || DEFAULT_LANGUAGE;
currentLanguage = translationsData[preferredLang] ? preferredLang : DEFAULT_LANGUAGE;
translation = translationsData[currentLanguage] || Object.values(translationsData)[0];

// Check if we need to show selector
const savedVocab = vocabList.find(v => v.id === savedVocabId);

if (!savedVocab && vocabList.length > 1) {
    // Show vocabulary selector
    initLanguageSwitcher();
    showVocabularySelector();
    dataReady = true;
    return;
}

// Load the vocabulary (saved or first available)
const vocabToLoad = savedVocab || vocabList[0];
if (!vocabToLoad) {
    throw new Error('No vocabulary configured');
}

selectedVocabularyId = vocabToLoad.id;
let vocabJson = null;

try {
    vocabJson = await loadJSONResource(vocabToLoad.file);
} catch (err) {
    console.error(`Error loading vocabulary '${vocabToLoad.file}':`, err);
    // If saved vocab failed, clear and show selector
    if (savedVocab && vocabList.length > 1) {
        localStorage.removeItem(VOCAB_STORAGE_KEY);
        showVocabularySelector();
        dataReady = true;
        return;
    }
    throw err;
}

vocabularyData = vocabJson;
appMetadata = vocabularyData?.metadata || {};
themeOptions = buildThemeOptions(vocabularyData);
useThemeDropdown = Object.keys(vocabularyData?.themes || {}).length > 4;

// Show change button if multiple vocabularies
const changeBtn = document.getElementById('change-vocab-btn');
if (changeBtn && vocabList.length > 1) {
    changeBtn.style.display = 'block';
    changeBtn.title = t('vocabularySelector.changeVocabulary') || 'Andere woordenschat';
}

applyTranslations();
initializeApp();
initLanguageSwitcher();
dataReady = true;
```

**Step 7: Add event listener for change vocabulary button**

Find where event listeners are added (around line 2035, after `initializeApp` function). Add:

```javascript
// Change vocabulary button
document.getElementById('change-vocab-btn')?.addEventListener('click', clearVocabularySelection);
```

**Step 8: Test the implementation**

Open the app in browser:
1. Should show vocabulary selector on first load
2. Select a vocabulary → app loads with that vocabulary
3. Refresh → app loads directly (remembers selection)
4. Click 📚 button → returns to selector
5. Select different vocabulary → loads correctly

**Step 9: Commit**

```bash
git add index.html
git commit -m "feat: implement vocabulary selector logic with localStorage persistence"
```

---

## Task 8: Create PWA manifest.json

**Files:**
- Create: `manifest.json`

**Step 1: Create manifest.json**

```json
{
  "name": "Woordenschat Oefening",
  "short_name": "Woordenschat",
  "description": "Practice Dutch vocabulary with interactive exercises",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#e8f4f8",
  "theme_color": "#7ba3d4",
  "orientation": "any",
  "icons": [
    {
      "src": "icons/icon-192.png",
      "sizes": "192x192",
      "type": "image/png",
      "purpose": "any maskable"
    },
    {
      "src": "icons/icon-512.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "any maskable"
    }
  ]
}
```

**Step 2: Commit**

```bash
git add manifest.json
git commit -m "feat: add PWA manifest.json"
```

---

## Task 9: Create PWA icons

**Files:**
- Create: `icons/` directory
- Create: `icons/icon-192.png`
- Create: `icons/icon-512.png`

**Step 1: Create icons directory**

```bash
mkdir -p icons
```

**Step 2: Create placeholder icons**

Create simple SVG-based icons using a tool or create placeholder PNGs. For now, create a simple HTML file to generate icons, or use an online tool.

Alternatively, create a simple icon using ImageMagick if available:

```bash
# Create a simple colored square as placeholder
convert -size 192x192 xc:#7ba3d4 -fill white -gravity center -pointsize 72 -annotate 0 'W' icons/icon-192.png
convert -size 512x512 xc:#7ba3d4 -fill white -gravity center -pointsize 200 -annotate 0 'W' icons/icon-512.png
```

If ImageMagick not available, manually create or download appropriate icons (192x192 and 512x512 PNG files with app branding).

**Step 3: Commit**

```bash
git add icons/
git commit -m "feat: add PWA icons"
```

---

## Task 10: Create service worker (sw.js)

**Files:**
- Create: `sw.js`

**Step 1: Create sw.js**

```javascript
const CACHE_NAME = 'woordenschat-v1';
const STATIC_ASSETS = [
    '/',
    '/index.html',
    '/config.json',
    '/manifest.json',
    '/icons/icon-192.png',
    '/icons/icon-512.png'
];

// Install: cache static assets
self.addEventListener('install', (event) => {
    event.waitUntil(
        caches.open(CACHE_NAME)
            .then((cache) => cache.addAll(STATIC_ASSETS))
            .then(() => self.skipWaiting())
    );
});

// Activate: clean old caches
self.addEventListener('activate', (event) => {
    event.waitUntil(
        caches.keys().then((cacheNames) => {
            return Promise.all(
                cacheNames
                    .filter((name) => name !== CACHE_NAME)
                    .map((name) => caches.delete(name))
            );
        }).then(() => self.clients.claim())
    );
});

// Fetch: network first, fallback to cache
self.addEventListener('fetch', (event) => {
    const { request } = event;
    const url = new URL(request.url);

    // Skip non-GET requests
    if (request.method !== 'GET') return;

    // Skip external requests
    if (url.origin !== location.origin) return;

    event.respondWith(
        fetch(request)
            .then((response) => {
                // Cache successful responses
                if (response.ok) {
                    const responseClone = response.clone();
                    caches.open(CACHE_NAME).then((cache) => {
                        cache.put(request, responseClone);
                    });
                }
                return response;
            })
            .catch(() => {
                // Fallback to cache
                return caches.match(request).then((cachedResponse) => {
                    if (cachedResponse) {
                        return cachedResponse;
                    }
                    // Return offline page for navigation requests
                    if (request.mode === 'navigate') {
                        return caches.match('/index.html');
                    }
                    return new Response('Offline', { status: 503 });
                });
            })
    );
});
```

**Step 2: Commit**

```bash
git add sw.js
git commit -m "feat: add service worker for offline support"
```

---

## Task 11: Register service worker and add PWA meta tags

**Files:**
- Modify: `index.html` (head section and end of body)

**Step 1: Add PWA meta tags to head**

Find the `<head>` section and add after existing meta tags:

```html
<link rel="manifest" href="manifest.json">
<meta name="theme-color" content="#7ba3d4">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="default">
<meta name="apple-mobile-web-app-title" content="Woordenschat">
<link rel="apple-touch-icon" href="icons/icon-192.png">
```

**Step 2: Add service worker registration**

Find the end of the JavaScript section (before `</script>`) and add:

```javascript
// Register service worker for PWA
if ('serviceWorker' in navigator) {
    window.addEventListener('load', () => {
        navigator.serviceWorker.register('/sw.js')
            .then((registration) => {
                console.log('SW registered:', registration.scope);
            })
            .catch((error) => {
                console.log('SW registration failed:', error);
            });
    });
}
```

**Step 3: Test PWA functionality**

1. Open app in Chrome
2. Open DevTools → Application → Service Workers
3. Verify service worker is registered
4. Check "Offline" in Network tab
5. Refresh → app should still work
6. Check Application → Manifest → verify manifest loads

**Step 4: Commit**

```bash
git add index.html
git commit -m "feat: register service worker and add PWA meta tags"
```

---

## Task 12: Final testing and cleanup

**Step 1: Full test checklist**

Test each scenario:

- [ ] First visit: vocabulary selector appears
- [ ] Select Thema 2: app loads with body/family/expressions vocabulary
- [ ] Refresh: app loads directly with Thema 2 (remembered)
- [ ] Click 📚: selector reappears
- [ ] Select Thema 3: app loads with feest/reizen/uitdrukkingen vocabulary
- [ ] Refresh: app loads directly with Thema 3
- [ ] All exercise types work (multiple choice, fill-in, matching, true/false)
- [ ] Language switcher works
- [ ] PWA: app works offline after first load
- [ ] PWA: app can be installed (shows install prompt on mobile/desktop)

**Step 2: Fix any issues found**

Address any bugs discovered during testing.

**Step 3: Final commit**

```bash
git add -A
git commit -m "test: verify vocabulary selector and PWA functionality"
```

---

## Summary

This plan implements:
1. Vocabulary file reorganization into `vocabularies/` folder
2. New vocabulary file for Thema 3
3. Updated config.json with vocabularies array
4. Vocabulary selector screen with localStorage persistence
5. Change vocabulary button in header
6. Basic PWA with manifest and service worker for offline use

Total estimated commits: 12
