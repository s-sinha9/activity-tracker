# Activity Tracker

A single-page web app for tracking time spent on an activity. Press **Start** when you begin and **Stop** when you finish. Every action is logged with its time, and a small dashboard shows how much time you were active over the last 1, 3, 6 or 24 hours.

It is one HTML file with plain JavaScript and CSS. There are no dependencies, no build step and no server.

## Features

- **Start and Stop buttons.** Only the button that makes sense is enabled: Start while stopped, Stop while running.
- **Activity log.** Each action is listed with its date, time and type, newest first. The log scrolls on its own so the rest of the page stays in place.
- **Analytics dashboard.** Shows the total active time and the number of sessions within the selected time range (last 1, 3, 6 or 24 hours). It updates every second.
- **Saved data.** Everything is stored in the browser's `localStorage`, so it is kept after reloading or restarting the browser.
- **Multi-tab sync.** Actions taken in one tab appear in other open tabs of the app.
- **Light and dark mode.** Uses your operating system's setting by default. The toggle in the top-right corner switches modes, and your choice is remembered.
- **Responsive layout.** Two columns on wide screens (actions and analytics on the left, log on the right), one column on screens narrower than 768px.

## Usage

The app is available at https://s-sinha9.github.io/activity-tracker/.

### Track an activity

1. Click **Start** when you begin. The status line shows when the session started.
2. Click **Stop** when you finish.
3. Pick a range under **Analytics** to see your total active time and session count for that period.

## How durations are calculated

A session is a Start followed by the next Stop. A session that hasn't been stopped yet counts up to the current time.

For the selected range, only the part of each session that falls inside the range is counted. For example, with the range set to **Last 3 hrs**, a session that ran from 5 hours ago to 2 hours ago contributes 1 hour. The session count includes every session that overlaps the range, even partially.

## Data and privacy

All data stays in your browser. Nothing is sent to a server.

- Data is per browser and per device. It is not shared between browsers or computers.
- Clearing your browser's site data deletes the history.
- Pages opened from `file://` may share storage with other local files in some browsers. Serve the app over HTTP if that matters to you.

Stored keys:

| Key | Contents |
| --- | --- |
| `activityTracker.events` | JSON array of `{ "action": "start" \| "stop", "time": <milliseconds since epoch> }` |
| `activityTracker.theme` | `"light"` or `"dark"`, only set after you use the toggle |

To clear all tracked activity, open the browser's developer tools console on the app page and run:

```js
localStorage.removeItem("activityTracker.events");
```

Then reload the page.

## Project structure

```
activity-tracker/
├── index.html   # The whole app: markup, styles and script
├── LICENSE      # MIT License
└── README.md
```

## License

Released under the [MIT License](LICENSE).
