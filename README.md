# Google Forms → Discord Webhook Integration

Automatically send Google Form submissions to a Discord channel using **Google Apps Script** and **Discord Webhooks**.  
Each form submission is formatted into a Discord embed with fields matching the form questions and responses.

---

## Features

- Sends every Google Form submission to Discord
- Formats responses into a clean Discord embed
- Automatically splits long responses to meet Discord limits
- Skips empty responses
- Uses native Google Apps Script (no external services required)
- Easy webhook-based setup

---

## How It Works

1. A user submits a Google Form
2. Google Apps Script triggers on form submission
3. The script:
   - Collects the latest form response
   - Formats each question and answer
   - Splits long answers (Discord limit: 1024 characters per field)
   - Sends the data to a Discord webhook as an embed

---

## Prerequisites

- A Google Form
- A Discord server with permission to create webhooks
- Access to Google Apps Script

---

## Setup Instructions

### 1. Create a Discord Webhook

1. Open **Discord**
2. Go to **Server Settings → Integrations → Webhooks**
3. Click **New Webhook**
4. Choose a channel and copy the **Webhook URL**

---

### 2. Open Google Apps Script (Important)

Google Forms **do not** have an obvious script editor button.

To open Apps Script:

1. Open your **Google Form**
2. Click the **three dots (⋮)** in the top-right corner
3. Select **“Apps Script”**

This opens the Google Apps Script editor attached to your form.

---

### 3. Reference the Script from GitHub

This project already includes the script logic.

- Use the `google.js` file from the repository
- Replace the placeholder webhook URL with your own:

```js
var POST_URL = "DISCORD_WEBHOOK_URL";
```

---

## 4. Create the Form Submit Trigger

The script must be triggered automatically when a form is submitted.

1. Open **Apps Script** from your Google Form  
   (Three dots ⋮ → **Apps Script**)
2. In the Apps Script editor, click the **Triggers** icon (⏱️) in the left sidebar
3. Click **Add Trigger**
4. Configure the trigger:
   - **Choose which function to run**: `onSubmit`
   - **Choose which deployment should run**: `Head`
   - **Select event source**: `From form`
   - **Select event type**: `On form submit`
5. Click **Save**

This ensures the script runs automatically whenever a new response is submitted.

---

## 5. Authorize the Script

Google requires explicit authorization before the script can access form data and send web requests.

1. Submit a **test response** in your Google Form
2. A Google authorization prompt will appear
3. Select your Google account
4. Click **Advanced**
5. Click **Go to {Your Project Name}**
6. Click **Allow**

Authorization only needs to be completed once.

---

## 6. Test the Integration

To confirm everything is working:

1. Submit another response in the Google Form
2. Open the configured Discord channel
3. Verify that:
   - A Discord embed is created
   - Each question appears as a field
   - Long responses are split correctly
   - Empty fields are ignored

---

## 7. Discord Embed Behavior

### Embed Structure

- **Title**: `Staff Apps`
- **Color**: `3553599`
- **Fields**:
  - Each form question becomes a field
  - Responses over 1024 characters are split into continuation fields

### Discord Limits Handled

- 1024 characters per field
- Automatic chunking prevents webhook failures
- Compatible with large application forms

---

## 8. Customization

You can customize the embed directly in `google.js`.

### Change Embed Title
```js
"title": "Staff Apps"
```

### Changed Embed Color
```js
"color": 3553599
```
