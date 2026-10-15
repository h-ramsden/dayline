# Dayline Web

Dayline Web is an installable, offline-first Progressive Web App. The stopwatch, entries, categories, class schedule, appearance, and data backups stay in this browser on this device using local storage. The service worker caches the app shell for offline use after the first successful visit.

## Run it on a computer

For a quick preview, serve this folder from a local web server. With Node installed, open Terminal in this folder and run:

```sh
npx --yes http-server . -p 8080
```

Then visit `http://localhost:8080` on that computer. This local address is only for preview; it cannot be used to install the app on an iPhone.

## Put an icon on your iPhone for free

iPhone requires a secure HTTPS site to install a real Home Screen web app. The app files here are static and can be hosted free, for example with GitHub Pages. Publishing requires a GitHub account and making the site repository/public files available on the web; this has not been done for you.

Once the site has an HTTPS URL:

1. Open that URL in Safari on the iPhone.
2. Tap Share, then **Add to Home Screen**. If offered, choose **Open as Web App**.
3. Tap Add. Dayline will appear as an icon and open without Safari's browser controls.

Home Screen web apps support Web Push on iOS/iPadOS 16.4 and later, but Web Push needs a server to send notifications. Apple says Apple Developer Program membership is not required for web push, but this project has no push server configured. As built, it cannot send the hourly reminder when iOS closes or suspends the app. Timer math remains correct because it saves the start timestamp. [Apple Web Push documentation](https://developer.apple.com/documentation/usernotifications/sending-web-push-notifications-in-web-apps-and-browsers?language=objc).

## Features

- Start, stop, or discard the stopwatch; entries split at local midnight.
- Manual entries by category, hours/minutes, end date/time, and note; delete entries from details.
- Default categories with stable colors, plus add/delete categories.
- Editable weekly school schedule with semester end date. Future class blocks are faded and not included in totals until the class ends.
- Log, day timeline, week summary with category percentages, and month calendar.
- Light/dark/system appearance, safe-area padding, reduced-motion CSS, and JSON import/export.

Data is stored per browser and device. It does not sync between Expo Go, this PWA, or other devices. Export a JSON backup before clearing browser data or changing browsers.

## Android

Once the site is hosted over HTTPS, open it in Chrome on Android, open the browser menu, and choose **Install app** or **Add to Home screen**. No Play Store account or listing is required for this install. The app shell works offline after the first successful load.

## iPhone reminder limitation

A PWA cannot create an iOS local notification for a future time and have iOS deliver it after the app is closed. For that, an iPhone PWA needs Web Push, which means a push server must store the subscription and enough active-timer metadata to send the reminder. This app keeps the actual log on-device and does not configure that server, so it does not claim to deliver closed-app hourly reminders. The timer itself continues from its saved timestamp.
