# Stream Tools

A collection of customizable web widgets for live streaming overlays.

## Current Price Widget

A real-time cryptocurrency price tracker designed for OBS Browser Sources. Displays token symbol, market cap, and 24-hour percentage change with auto-refresh every 5 seconds.

![Demo](demo.png)

### Why Use This?

- **Customizable**: Adjust font size, colors, transparency, and coin tracking via a simple settings interface
- **OBS-Ready**: Works as a Browser Source in OBS with transparent backgrounds
- **Live Updates**: Automatically fetches and displays real-time market data
- **Shareable**: Generate custom widget URLs to reuse across streams or share with others

### How to Use

#### 1. Configure Your Widget

1. Open `current-price.html` in your browser
2. The settings modal will appear automatically on first load
3. Customize your widget:
   - **Font Size**: Adjust text size in pixels
   - **Foreground Color**: Set the text color
   - **Background Color**: Choose background color
   - **Background Opacity**: Control transparency (0-100%)
   - **Coin Address**: Enter the token contract address to track
   - **Chain ID**: Specify the blockchain network (e.g., 8453 for Base)
4. Click **"Copy Widget URL"** to copy the configured URL
5. Click **"Preview"** to see your widget in action

#### 2. Add to OBS

1. In OBS, click **"+"** in the Sources panel
2. Select **"Browser"**
3. Give it a name (e.g., "Crypto Price Ticker")
4. Paste your copied widget URL into the **URL** field
5. Set dimensions:
   - Width: 1920 (or your stream width)
   - Height: 200 (adjust as needed)
6. Check **"Shutdown source when not visible"** (optional, saves resources)
7. Click **OK**

#### 3. Position and Style

- Drag the browser source to position it on your stream
- Resize using the red bounding box handles
- Click anywhere on the widget in your browser to reopen settings and adjust colors/transparency
- Use background opacity at 0% for a fully transparent background in OBS

### Technical Details

- **Data Source**: Zora API (https://api-sdk.zora.engineering)
- **Update Frequency**: Every 5 seconds
- **Default Token**: $propaganda on Base (Chain ID: 8453)

### Tips

- For transparent overlays, set Background Opacity to 0%
- Test your widget in a browser before adding to OBS
- Save multiple widget URLs for different coins
- Click anywhere on the widget to edit settings on the fly

## Chat Overlay Widget

A real-time Zora livestream chat overlay that displays viewer messages with usernames and avatars. Messages automatically fade out after a configurable duration, creating a clean and dynamic chat display perfect for streaming.

### Why Use This?

- **Real-Time Chat**: Live WebSocket connection to Zora livestream chat via GraphQL
- **Easy Setup**: Enter your Zora username (auto-lookup) or livestream ID (manual entry)
- **Customizable**: Adjust colors, font size, message count, and fade duration
- **Smooth Animations**: Messages fade in and out smoothly with configurable timing
- **Avatar Support**: Optional user avatars displayed alongside messages
- **OBS-Ready**: Transparent background support and optimized for browser sources
- **Auto-Reconnect**: Handles connection drops and reconnects automatically

### How to Use

#### 1. Configure Your Widget

1. Open `chat.html` in your browser
2. The settings modal will appear automatically on first load
3. Enter your settings:
   - **Zora Username**: Enter your username (e.g., "carter") - automatically fetches your livestream ID
   - **OR Livestream ID**: Enter your livestream ID manually (if username lookup doesn't work)
   - **Font Size**: Adjust text size (12-32px)
   - **Max Messages Displayed**: How many messages to show at once (5-50)
   - **Fade Duration**: How long before messages fade out (20s - 10 minutes)
   - **Show Avatars**: Toggle to show/hide user avatars
4. Click **"Apply Settings"** to save and start the chat connection
5. Click **"Copy Widget URL"** to copy the configured URL

#### 2. Add to OBS

1. In OBS, click **"+"** in the Sources panel
2. Select **"Browser"**
3. Give it a name (e.g., "Zora Chat Overlay")
4. Paste your copied widget URL into the **URL** field
5. Set dimensions:
   - Width: 400-600 (adjust based on your layout)
   - Height: 600-1080 (adjust based on your layout)
6. Check **"Shutdown source when not visible"** (optional, saves resources)
7. Click **OK**

#### 3. Position and Customize

- Drag the browser source to position it on your stream (usually left or right side)
- Resize using the red bounding box handles
- Click anywhere on empty space in the widget to reopen settings and adjust:
  - Font size for readability
  - Max messages to control density
  - Fade duration based on chat activity
  - Show/hide avatars based on your preference

### Features

**Auto-Reconnect**
- Automatically reconnects if connection drops
- Handles Zora's backend timeout pattern (resubscribes after inactivity)
- Keeps chat overlay running reliably during long streams

**Message Management**
- Messages automatically fade out after the configured duration
- Oldest messages are removed when max count is reached
- Smooth scroll to newest messages
- Word wrapping for long messages

### Technical Details

- **Data Source**: Zora GraphQL API (wss://api.zora.co/universal/graphql)
- **Connection Type**: WebSocket (GraphQL subscriptions)
- **Username Lookup**: HTTP GraphQL query to fetch stream ID from username
- **Custom WebSocket Client**: Vanilla JavaScript implementation (no external dependencies)
- **Auto-Reconnect**: Immediate on timeout, 5 seconds on error
- **Keep-Alive**: Pings every 10 seconds

### Tips

- **Two ways to connect**: Use your username for automatic lookup, or enter livestream ID manually
- Username lookup works when served via web server (like GitHub Pages)
- For local testing, enter your livestream ID directly to avoid CORS issues
- Test the widget URL in your browser before adding to OBS
- Adjust fade duration based on chat activity (longer for slow chats, shorter for busy ones)
- Position the overlay where it won't cover important stream content
- Click on empty space (not messages) to reopen settings anytime
- Save the widget URL to quickly switch between different stream configurations

### Troubleshooting

**Chat not connecting:**
- If username lookup fails, try entering your livestream ID manually
- Verify your username is spelled correctly or livestream ID is correct
- Make sure you have an active livestream on Zora
- Check browser console for error messages

**"Cannot fetch stream ID" error:**
- This happens when testing locally (CORS restriction)
- Solution: Enter your livestream ID manually instead of username
- When deployed (GitHub Pages), username lookup will work fine

**Messages not appearing:**
- Refresh the page to reconnect
- Verify there are active messages in your Zora livestream chat
- Make sure your livestream is currently active

**Messages fading too quickly/slowly:**
- Click on empty space to reopen settings
- Adjust the Fade Duration slider (20s - 10 minutes)
- Apply changes and test with new messages

**Performance issues:**
- Reduce max messages displayed
- Disable avatars if not needed
- Lower fade duration to clear messages faster
