# 🎓 Vocabulary Trainer

An interactive, multilingual vocabulary training application designed for children. Features timed sessions, multiple exercise types, progress tracking, and customizable vocabulary sets.

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Languages](https://img.shields.io/badge/languages-NL%20%7C%20ES%20%7C%20EN-orange.svg)

## ✨ Features

- **🌍 Multilingual**: Full support for Dutch (NL), Spanish (ES), and English (EN)
- **🎯 Multiple Exercise Types**:
  - Multiple Choice
  - Fill in the Blank
  - Matching Pairs
  - True/False
- **⏱️ Flexible Goals**:
  - Time-based sessions (1-60 minutes)
  - Exercise-based sessions (10-100 questions)
- **📊 Progress Tracking**:
  - Real-time statistics
  - Score percentage
  - Timer display
- **🎨 Kid-Friendly Design**:
  - Clean, modern interface
  - Color-coded feedback
  - Emoji-based achievement levels
- **📝 Customizable**:
  - Easy-to-edit vocabulary JSON files
  - Configurable settings
  - Similarity matching for typos (80% threshold)

## 🚀 Quick Start

### Option 1: Direct Use
1. Download or clone this repository
2. Open `index.html` in your web browser
3. Click START and begin practicing!

### Option 2: GitHub Pages
Visit the live demo: `https://YOUR-USERNAME.github.io/vocabulary-trainer/`

## 📁 Project Structure

```
vocabulary-trainer/
├── index.html           # Main application file
├── vocabulary.json      # Vocabulary data (easily customizable)
├── translations.json    # UI translations (NL, ES, EN)
├── config.json         # App configuration
├── README.md           # This file
└── LICENSE             # MIT License
```

## 🔧 Customization

### Adding Your Own Vocabulary

Edit `vocabulary.json`:

```json
{
  "themes": {
    "1": {
      "name": "Theme Name",
      "emoji": "📚",
      "vocabulary": [
        {
          "word": "word or phrase",
          "definition": "definition or translation"
        }
      ]
    }
  }
}
```

### Changing the Language

Edit `config.json`:

```json
{
  "defaultLanguage": "nl"  // Change to "es" or "en"
}
```

Or add a language selector in the UI (see below for implementation).

### Adding New Languages

1. Add translations to `translations.json`
2. Update `config.json` to include the new language
3. Follow the existing translation structure

### Customizing Colors

Edit `config.json`:

```json
{
  "colors": {
    "primary": "#7ba3d4",
    "secondary": "#c9a5d4",
    "background": "#e8f4f8",
    "correct": "#4CAF50",
    "incorrect": "#f44336"
  }
}
```

### Adjusting Goals

Edit `config.json`:

```json
{
  "goals": {
    "time": {
      "min": 1,
      "max": 60,
      "default": 5
    },
    "exercises": {
      "min": 10,
      "max": 100,
      "default": 20
    }
  }
}
```

## 🎮 How to Use

1. **Start Session**: Click the START button
2. **Choose Goal**: Select time-based or exercise-based goal
3. **Select Theme**: Choose from available themes or "All Weeks"
4. **Pick Exercise Type**: Choose your preferred exercise format
5. **Practice**: Complete exercises and track your progress
6. **View Results**: See your final score and statistics

## 🏆 Scoring System

The app uses a 10-level scoring system based on percentage correct:

- 🌟 95-100%: Perfect!
- 🎉 85-94%: Excellent!
- 😊 75-84%: Very good!
- 👍 65-74%: Good!
- 🙂 55-64%: Pretty good!
- 😐 45-54%: Can do better!
- 😕 35-44%: Need more practice!
- 😞 25-34%: Keep practicing!
- 😢 15-24%: Don't give up!
- 💪 0-14%: Keep trying!

## 🛠️ Technical Details

- **Frontend**: Pure HTML5, CSS3, JavaScript (ES6+)
- **No Dependencies**: No frameworks or libraries required
- **No Build Process**: Just open and use
- **Offline Ready**: Works without internet connection
- **Mobile Friendly**: Responsive design

## 📝 Configuration Files

### vocabulary.json
Contains all vocabulary organized by themes. Each theme has:
- `name`: Theme display name
- `emoji`: Theme icon
- `vocabulary`: Array of word-definition pairs

### translations.json
Contains all UI text in multiple languages. Structure:
- Language code (nl, es, en)
  - `app`: App-level text
  - `stats`: Statistics labels
  - `themes`: Theme names
  - `exerciseTypes`: Exercise type names
  - `goals`: Goal selection text
  - `questions`: Question prompts
  - `feedback`: Response messages
  - `buttons`: Button labels
  - `results`: Results screen text

### config.json
Application configuration:
- Default language
- Available languages
- Goal ranges and defaults
- Similarity matching settings
- Color scheme
- Scoring levels

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. Areas for contribution:

- Additional language translations
- More vocabulary themes
- New exercise types
- UI improvements
- Bug fixes

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👨‍💻 Development

### Local Development
1. Clone the repository
2. Open `index.html` in your browser
3. Make changes to HTML, CSS, or JSON files
4. Refresh browser to see changes

### Testing
- Test in multiple browsers (Chrome, Firefox, Safari, Edge)
- Test on mobile devices
- Test with different vocabulary sets
- Test all language options

## 🐛 Known Issues

None currently. Please report any issues on GitHub.

## 🗺️ Roadmap

- [ ] Language selector in UI
- [ ] User authentication and progress saving
- [ ] Additional exercise types
- [ ] Audio pronunciation support
- [ ] Difficulty levels
- [ ] Achievement badges
- [ ] Export results to PDF
- [ ] Dark mode

## 📧 Contact

For questions, suggestions, or issues, please open a GitHub issue.

## 🙏 Acknowledgments

- Designed for children learning vocabulary
- Built with modern web standards
- Inspired by educational best practices

---

Made with ❤️ for language learners everywhere
