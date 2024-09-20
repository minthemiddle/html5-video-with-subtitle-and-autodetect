# Video Player with Automated Subtitle Language Detection

## Introduction

This project provides a video player with automated subtitle language detection. The player dynamically loads the appropriate subtitle track based on the user's browser language settings. If the browser language is not supported, it falls back to English subtitles.

It uses a video from B2B Platform europages.com as an example.  

## Features

- **Automated Subtitle Language Detection**: The player automatically selects the subtitle track based on the user's browser language.
- **Fallback to English**: If the browser language is not in the list of supported languages, the player defaults to English subtitles.
- **Supported Languages**: The player supports German, French, Turkish, Spanish, Greek, and English subtitles.

## For End Users

### How to Use

1. **Open the Video Player**: Start a web browser (e.g. `php -S localhost:8003`, needed due to CORS) and open the `index.html` file in your web browser.
2. **Play the Video**: The video will start playing automatically.
3. **Subtitles**: The appropriate subtitle track will be displayed based on your browser's language settings. If your language is not supported, English subtitles will be shown.

### Supported Languages

The video player supports the following languages for subtitles:
- **German**: `de`
- **French**: `fr`
- **Turkish**: `tr`
- **Spanish**: `es`
- **Greek**: `el`
- **English**: `en` (fallback)

## For Developers

### Project Structure

```
/
├── index.html
├── subtitles/
│   ├── subtitles-de.vtt
│   ├── subtitles-el.vtt
│   ├── subtitles-en.vtt
│   ├── subtitles-es.vtt
│   ├── subtitles-fr.vtt
│   └── subtitles-tr.vtt
├── video.mp4
└── README.md
```

### How It Works

1. **Language Detection**:
   - The script detects the user's browser language using `navigator.language` or `navigator.userLanguage`.
   - It then splits the language code to get the primary language (e.g., `en-US` becomes `en`).

2. **Subtitle Selection**:
   - The script iterates over all text tracks associated with the video element.
   - It checks if the track's language matches the user's browser language.
   - If a match is found, the track's mode is set to `'showing'`, making it visible.
   - If no match is found, the track's mode is set to `'hidden'`.

3. **Fallback to English**:
   - If the user's browser language is not in the list of supported languages, the script defaults to English subtitles.

### Customization

- **Adding New Languages**:
  - To add support for a new language, create a new `.vtt` subtitle file in the `subtitles/` directory.
  - Update the `index.html` file to include the new track:
    ```html
    <track label="New Language" kind="subtitles" srclang="new-lang" src="subtitles/subtitles-new-lang.vtt">
    ```
  - Update the `availableLanguages` array in the JavaScript to include the new language code.

- **Modifying the Fallback Language**:
  - To change the fallback language, modify the `userLangPrefix` assignment in the JavaScript:
    ```javascript
    if (!availableLanguages.includes(userLangPrefix)) {
        userLangPrefix = 'new-fallback-lang';
    }
    ```

### Thanks

Learned mainly from [HTML video with subtitles](https://til.simonwillison.net/html/video-with-subtitles) by Simon Willison.
