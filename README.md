---

# newgen-fca - Unofficial Facebook Chat API

This is a fork of the original [fca-unofficial](https://github.com/azlux/facebook-chat-api) repository. This version includes new features and updates that are bundled faster than the main repository. However, be aware that new features may also come with some bugs.

---

## Overview

This API allows you to automate Facebook chat functionalities by emulating the browser's GET/POST requests. It does not work with an auth token and requires a Facebook account's **AppState** (session information), which is obtained via third-party tools.

---

## Important Notes

**The `api.getAppState()` function no longer works!**

As of recent changes, Facebook no longer supports retrieving session information directly from the API using `api.getAppState()`. Instead, you must use a previously obtained **AppState** from external tools like **Kiwi Browser** and the **c3c-ufc-utility** extension.

We strongly recommend being responsible when using this API to avoid issues like account bans. Avoid spamming messages, sending large amounts of requests, or using excessive automation.

---

## How to Get AppState

1. **Kiwi Browser & c3c-ufc-utility Extension**
   - Install the **Kiwi Browser** and the **c3c-ufc-utility extension**.
   - Use the extension to extract your **AppState** (session cookies) from your Facebook login.
   - The **AppState** will be saved as a `appstate.json` file, which you will load for logging in.

For more details, refer to the official [c3c-ufc-utility GitHub release](https://github.com/c3cbot/c3c-ufc-utility/releases).

---

## Install

To install **newgen-fca**, use the following npm command:

```bash
npm install newgen-fca
```

To install the bleeding-edge version directly from GitHub:

```bash
npm install newgen-fca/newgen-fca
```

---

## Example Usage

Here’s how to log in using the **AppState**:

```javascript
const fs = require('fs');
const login = require('newgen-fca');

// Load your appState from the saved file
const appState = JSON.parse(fs.readFileSync('appstate.json', 'utf8'));

// Use the appState for login
login({ appState: appState }, (err, api) => {
    if (err) return console.error('Login failed:', err);

    console.log('Successfully logged in!');

    // Example of listening for new messages
    api.listen((err, message) => {
        if (err) return console.error(err);

        // Respond to the received message
        api.sendMessage(message.body, message.threadID);
    });
});
```

### Main Functionality

- **Sending Messages:**
    - Regular Text Messages
    - Sticker Messages
    - Image/File Attachments
    - URLs
    - Emojis

- **Listening to Messages:**
    - Listen to messages in real-time
    - Option to listen to events like user joining or leaving a chat

---

## Documentation

You can find the full documentation [here](DOCS.md).

---

## FAQ

1. **Why doesn’t `api.getAppState()` work anymore?**
   - The `api.getAppState()` function was deprecated. You now need to use the **AppState** from external tools, such as the **Kiwi Browser** and the **c3c-ufc-utility** extension.

2. **How can I log in without credentials?**
   - After logging in through a browser, extract your **AppState** using the **c3c-ufc-utility extension**. This is now the only way to authenticate.

3. **Can I listen to messages from the bot?**
   - Yes, by default, the bot listens to incoming messages and can respond automatically. You can configure it to respond with specific actions based on the message content.

4. **Is there a way to send media like images or files?**
   - Yes, you can send files or images by passing them as attachments. The example provided demonstrates how to send an image along with a text message.

5. **How do I keep my session alive?**
   - You do not need to log in repeatedly once you have your **AppState** saved. Simply load the **appState.json** each time you initialize the API.

6. **Can I send messages as a Facebook Page?**
   - Yes, you can configure the login to use a Facebook Page ID for sending messages as a Page. This is done during the login step.

---

## Projects Using This API

- [c3c](https://github.com/lequanglam/c3c) - A customizable bot with Facebook and Discord support.
- [Messenger-CLI](https://github.com/AstroCB/Messenger-CLI) - Command-line interface for Facebook Messenger.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Note:** This project is an unofficial Facebook chat API. Use it responsibly and follow Facebook’s terms of service.

---
