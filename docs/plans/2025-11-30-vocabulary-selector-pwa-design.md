# Vocabulary Selector + PWA Design

## Overview

Add vocabulary selection functionality and basic PWA support to the vocabulary trainer app.

## Goals

1. Allow users to choose between multiple vocabulary sets (themas)
2. Persist selection across sessions
3. Enable offline usage via PWA

## File Structure Changes

```
vocabulary-trailer/
├── manifest.json              # NEW - PWA manifest
├── sw.js                      # NEW - Service worker
├── icons/                     # NEW - PWA icons
│   ├── icon-192.png
│   └── icon-512.png
├── vocabularies/              # NEW - Vocabulary files folder
│   ├── taal_groep5_thema2.json   # MOVED from vocabulary.json
│   └── taal_groep5_thema3.json   # NEW
├── config.json                # MODIFIED
├── index.html                 # MODIFIED
└── translations/              # EXISTING
```

## Data Changes

### config.json

Remove `vocabularyFile` field, add `vocabularies` array:

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
  "goals": { ... },
  "similarity": { ... },
  "colors": { ... },
  "scoring": { ... }
}
```

### taal_groep5_thema3.json

New vocabulary file with structure:

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
      "vocabulary": [...]
    },
    "2": {
      "name": "Week 2: Reizen",
      "emoji": "✈️",
      "vocabulary": [...]
    },
    "3": {
      "name": "Week 3: Uitdrukkingen",
      "emoji": "💬",
      "vocabulary": [...]
    }
  }
}
```

### localStorage

- Key: `selectedVocabulary`
- Value: vocabulary `id` (e.g., `"thema3"`)

## UI Changes

### Selection Screen

Shown when:
- No vocabulary selected in localStorage
- User clicks "change vocabulary" button

Layout:
```
┌─────────────────────────────────────┐
│     🎓 Kies je woordenschat         │
│                                     │
│  ┌─────────────────────────────┐   │
│  │ Thema 2: Het menselijk...   │   │
│  │ 36 woorden                  │   │
│  └─────────────────────────────┘   │
│  ┌─────────────────────────────┐   │
│  │ Thema 3: Feest, reizen...   │   │
│  │ 34 woorden                  │   │
│  └─────────────────────────────┘   │
│                                     │
└─────────────────────────────────────┘
```

Style:
- Same background as app (`#e8f4f8`)
- Centered container with white background
- List items as clickable buttons
- Show word count per vocabulary

### Header Change Button

- Small icon (📚) in top-right corner of header
- On click: clear localStorage, reload page → shows selection screen

## PWA Implementation

### manifest.json

```json
{
  "name": "Woordenschat Oefening",
  "short_name": "Woordenschat",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#e8f4f8",
  "theme_color": "#7ba3d4",
  "icons": [
    { "src": "icons/icon-192.png", "sizes": "192x192", "type": "image/png" },
    { "src": "icons/icon-512.png", "sizes": "512x512", "type": "image/png" }
  ]
}
```

### Service Worker (sw.js)

Caching strategy:
1. **Static cache** (on install): `index.html`, `config.json`, fonts, icons, manifest
2. **Dynamic cache** (on demand): vocabulary files when selected

Strategy: Network first, fallback to cache for offline support.

### index.html additions

- `<link rel="manifest" href="manifest.json">`
- `<meta name="theme-color" content="#7ba3d4">`
- `<link rel="apple-touch-icon" href="icons/icon-192.png">`
- Service worker registration script

## App Flow

1. Load `config.json`
2. Check `localStorage.getItem('selectedVocabulary')`
3. If valid selection exists:
   - Load vocabulary file directly
   - Show main app
4. If no selection:
   - Show selection screen
   - On select: save to localStorage, load vocabulary, show main app

## Translations

Add to all translation files:
- `selectVocabulary`: "Kies je woordenschat" / "Choose your vocabulary" / etc.
- `words`: "woorden" / "words" / etc.
- `changeVocabulary`: "Verander woordenschat" / "Change vocabulary" / etc.
