# LangTek Wiki

LangTek is a media immersion app for learning English or Spanish. Instead of lessons and drills, you read, watch, and listen to real content in the language you are learning, with translation and study tools built in. No games, no lessons, no tracking.

- **Get the app:** [LangTek on Google Play](https://play.google.com/store/apps/details?id=com.decyphertek.langtek)
- **Pricing:** Free during beta testing. A single $3/month subscription is planned after beta.
- **Privacy:** See the [LangTek Privacy Policy](/products/langtek/privacy/)

## RSS Reader

The RSS reader is the core of the app. Bring the feeds you already follow, or start with preset feeds covering news, technology, sports, and finance.

### Add a Feed

1. Open LangTek and go to the RSS Reader section
2. Tap **Add Feed**
3. Enter the RSS feed URL
4. Save and start reading

Popular Spanish sources include El País, BBC Mundo, CNN en Español, Xataka, Genbeta, El Cultural, and Jot Down.

### Read with Translation

1. Open any article
2. Tap any word for a quick word-by-word translation
3. Tap a sentence for the full contextual translation
4. Long-press for extra context and usage examples

## Videos

Watch Spanish or English videos on the topics you already follow. When a sentence goes by too fast, use the same translation tools you use for articles to pick it apart. Seeing and hearing a word together anchors the sound to the meaning.

## Podcasts

Podcast feeds live next to your articles and videos, not in a separate app. Listen while driving, walking, or doing chores, and tap the translation tools when a fast segment needs a second look. Listening at native speed is the fastest way to make fast speech stop sounding like noise.

## EPUB Books

Load your own EPUB books, or browse the built-in **Public Domain Library**, a free collection of classic English and Spanish books (Cervantes, Twain, Verne, and more). The same translation tools follow you into every book.

## Translations

LangTek gives you two translations at once, and they teach you different things:

- **Word-for-word** - the literal structure of the sentence, which teaches you how the language works
- **Contextual** - what the sentence actually means, the way a native would say it
- **Grammar analysis** - tap the grammar icon on a sentence for tense, conjugation, and structure breakdowns
- **Wiktionary** - while reading articles or books, tap a word for definitions, parts of speech, and word forms without leaving the page

Comparing the two translations trains you to stop translating in your head. Translations are cached, and common translations work from a built-in offline database, so reading does not always depend on a network connection. Language support is bidirectional, with automatic detection.

## AI Conversation Assistant

Practice conversations with an optional AI tutor powered by the OpenRouter API. It replies like a normal chat with translations alongside, and it answers grammar questions on demand.

### Setup

1. Create a free account at [OpenRouter.ai](https://openrouter.ai) and generate an API key
2. Open **Settings → AI Settings** in LangTek
3. Paste your API key and pick a model (Llama 3.3 70B Instruct is the default; DeepSeek R1 0528 and Gemma 3 27B IT are also available)
4. Choose whether responses arrive in Spanish or English
5. Tap **Test Connection** to verify

The assistant remembers your last few messages for context. Your API key is stored locally on your device, and LangTek never stores your conversations.

## Anki Flash Cards

Anki flash cards with spaced repetition are built into the app. Words you meet while reading become cards, and each card comes back right before you would have forgotten it. You are reviewing your own reading history, not a list someone else wrote. Manage your decks as your collection grows, with AnkiWeb sync available.

## Text-to-Speech

Text-to-speech reads content aloud so you can hear the words while your eyes follow them.

- Works on article titles, article content, AI responses, and single words
- Natural es-US and en-US voices
- Adjustable speech rate from 0.5x to 2.0x, set separately per language in **Settings → TTS Settings**

Tip: start at 0.7x - 0.8x while learning, and practice shadowing by repeating what you hear.

## Saved Items

Bookmark articles and phrases to build a personal learning library.

- **Save an article:** tap the bookmark icon at the top of any article
- **Save a phrase:** long-press any sentence and select **Save**
- **Manage:** go to **Settings → Saved Items** to browse, search, and delete (swipe left)

Saved items are stored locally on your device, work offline, and have no limit. There is no cloud sync, which keeps your data private.

## Reading Timer and Notifications

A reading timer tracks your sessions, and scheduled notifications put the app in front of you at the times you actually have a spare minute. Fifteen honest minutes with a timer on beats a vague intention to read more.

## Settings

Access via the hamburger menu → **Settings**.

- **Theme and fonts** - text size, light or dark theme, font family
- **AI Settings** - OpenRouter API key, model, response language
- **TTS Settings** - speech rates per language
- **Saved Items** - your bookmarks

All settings are stored locally on your device.

## Learning Tips

1. Start with topics you already know to make comprehension easier
2. Use word-by-word translation first, then compare with the contextual translation
3. Read at least one article a day; consistency beats marathons
4. Turn new words into flash cards and let spaced repetition do the review
5. Use TTS to connect sound and meaning while you read
6. Practice conversations with the AI to reinforce what you read

## Troubleshooting

- **Feed not loading:** check the feed URL and your connection; some sites block RSS access, so try another source
- **Translation not appearing:** new translations need an internet connection the first time; restart the app if it seems stuck
- **TTS silent:** check device volume and confirm TTS language packs are installed under device **Settings → Language & Input → Text-to-Speech**
- **AI not responding:** run **Test Connection** in AI Settings and verify your OpenRouter key

## Support

- [GitHub Issues](https://github.com/decyphertek/langtek-app/issues)
- [LangTek product page](https://langtek.decyphertek.io/)
- [Deep dive](https://decyphertek.io/products/deepdive/langtek/)
