# Nextcloud Forms Export / Import
Exports forms and the submissions of form into an json file and allows to import it into another nextcloud server

A single-page browser tool to export Nextcloud Forms (with all questions and options) from one server and import them into another.

## Usage

1. Open `index.html` in your browser
2. **Export**: Enter the source server URL, credentials, and form ID, then click "Export Form as JSON"
3. **Import**: Enter the target server URL, credentials, select the exported JSON file, then click "Import Form from JSON"

## Finding the Form ID or Hash

You can use either the **numeric Form ID** or the **hash** from the form URL.

The hash is the string visible in your Nextcloud URL, e.g.:
`https://cloud.example.com/apps/forms/rPXD5oJeNjJozgn6` — here `rPXD5oJeNjJozgn6` is the hash.

Simply paste the hash into the "Form ID or Hash" field. The tool will automatically resolve it to the correct form.

## CORS Setup

Since this tool runs in the browser, requests to a different domain may be blocked by CORS policy. Four solutions:

### Option 1: Browser Extension

Install a CORS-unblocking extension:

- **Chrome / Edge / Brave**: [CORS Unblock](https://chromewebstore.google.com/detail/cors-unblock/lfhmikememgdcahcdlaciloancbhjino)
- **Firefox**: [CORS Unblock](https://addons.mozilla.org/firefox/addon/cors-unblock/)

Enable it, reload the page, and requests should go through.

### Option 2: Chrome / Chromium with disabled CORS

Launch Chrome with `--disable-web-security` and a separate user-data directory:

**macOS:**
```bash
open -n "/Applications/Google Chrome.app" --args --user-data-dir="$HOME/chrome-cors-dev" --disable-web-security
```

**Windows (PowerShell):**
```powershell
& "${env:PROGRAMFILES}\Google\Chrome\Application\chrome.exe" --user-data-dir="$env:USERPROFILE\chrome-cors-dev" --disable-web-security
```

**Windows (Command Prompt):**
```cmd
"%PROGRAMFILES%\Google\Chrome\Application\chrome.exe" --user-data-dir="%USERPROFILE%\chrome-cors-dev" --disable-web-security
```

**Linux:**
```bash
google-chrome --user-data-dir="$HOME/chrome-cors-dev" --disable-web-security
```

### Option 3: Brave Browser with disabled CORS

Same flags, different executable:

**macOS:**
```bash
open -n "/Applications/Brave Browser.app" --args --user-data-dir="$HOME/brave-cors-dev" --disable-web-security
```

**Windows (PowerShell):**
```powershell
& "${env:LOCALAPPDATA}\BraveSoftware\Brave-Browser\Application\brave.exe" --user-data-dir="$env:USERPROFILE\brave-cors-dev" --disable-web-security
```

**Windows (Command Prompt):**
```cmd
"%LOCALAPPDATA%\BraveSoftware\Brave-Browser\Application\brave.exe" --user-data-dir="%USERPROFILE%\brave-cors-dev" --disable-web-security
```

**Linux:**
```bash
brave-browser --user-data-dir="$HOME/brave-cors-dev" --disable-web-security
```

> **Warning:** `--disable-web-security` disables browser security entirely. Only use this dedicated instance for this tool, not for general browsing. Close it when done.

### Option 4: Same-Origin Deployment

Place the `index.html` file on your Nextcloud server's web directory so it is served from the same domain. No extension or flags needed.

## Requirements

- A modern browser (Chrome, Firefox, Edge, Safari)
- Nextcloud server with the Forms app installed (API v3)
- Valid credentials with permission to read/create forms
