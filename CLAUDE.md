# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static HTML project that displays Matthew McConaughey's 2014 Oscar acceptance speech with phonetic annotations and Chinese translations. The project focuses on visual presentation and educational value for English learners.

**Key Features:**
- Color-coded parts of speech (nouns, adjectives, verbs, names)
- Phonetic transcriptions for each word using IPA notation
- Chinese translations for each paragraph
- Responsive design with gradient backgrounds
- Jieti alignment system for English text and phonetics

## Project Structure

- `index.html` - Single HTML file containing all content, styles, and JavaScript
- Test files (demo-*.html, test-*.html) - Alignment test pages (can be ignored)

**No build process required** - This is a static HTML project that can be opened directly in a browser.

## Architecture

### CSS Architecture
The project uses CSS custom properties (variables) for theming:
- `--noun-color: #e74c3c` - Red for nouns
- `--adj-color: #27ae60` - Green for adjectives
- `--verb-color: #3498db` - Blue for verbs
- `--name-color: #9b59b6` - Purple for names
- `--gold: #D4AF37` - Accent color for Oscar theme

### Word Alignment System
The critical feature is vertical alignment of all English words regardless of phonetic annotations:

1. **Manual word spans**: Words with phonetics use this structure:
   ```html
   <span class="word verb">
       <span class="word-text">Thank</span>
       <span class="word-phonetic">/θæŋk/</span>
   </span>
   ```

2. **JavaScript auto-wrapping**: Plain text words are automatically wrapped with `.word-plain` class on DOM load using a TreeWalker that processes text nodes in `.english-text` containers.

The alignment uses `display: inline-block` with `vertical-align: bottom` and fixed heights to ensure all word text appears on the same baseline.

### Content Sections
- **Header**: Oscar branding with gradient background
- **Legend**: Color key for parts of speech
- **Speech Content**: 8 paragraphs with English text and Chinese translations
- **Styling**: Dark theme with gold accents, gradient backgrounds, and card-based layout

## Development Commands

**Viewing the project:**
```bash
# Start a local server (recommended)
python3 -m http.server 8000
# Then open http://localhost:8000/index.html

# Or simply open index.html in a browser
open index.html
```

**No other commands needed** - There are no tests, linters, or build processes for this static project.

## Content Maintenance

### Adding New Speech Content
1. Follow the existing paragraph structure:
   ```html
   <div class="paragraph-block">
       <div class="para-number">#</div>
       <div class="english-text">
           <!-- Words with phonetics here -->
       </div>
       <div class="translation">
           <!-- Chinese translation -->
       </div>
   </div>
   ```

2. Always wrap words in `<span class="word [class]">` with proper part-of-speech class (noun, adj, verb, name, pron, adv, etc.)

3. Include empty phonetic spans for words without pronunciation:
   ```html
   <span class="word pron">
       <span class="word-text">you</span>
       <span class="word-phonetic"></span>
   </span>
   ```

4. Add corresponding Chinese translation

### CSS Classes Reference
- `.word` - Base container for each word
- `.word-text` - The visible English word
- `.word-phonetic` - IPA phonetic transcription (empty if none)
- `.word-plain` - Applied by JavaScript to unwrapped text nodes
- `.noun`, `.adj`, `.verb`, `.name` - Part of speech coloring

## Key Technical Details

- **Responsive**: Mobile styles in `@media (max-width: 768px)` queries
- **Self-contained**: All styles and scripts are inline, no external dependencies
- **Accessibility**: Uses semantic HTML structure with proper heading hierarchy
- **Performance**: Minimal JavaScript, single DOM pass for text wrapping
