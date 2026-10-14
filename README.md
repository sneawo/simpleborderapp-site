# Simple Border

[SimpleBorder.app](https://simpleborder.app) helps creators add clean, no-crop borders to photos and videos for Instagram and beyond.

For the latest features, screenshots, and store links, visit **https://simpleborder.app**.

## App Store campaign attribution

App Store links use provider token `124097192`, taken from the campaign link generated in App Store Connect. The campaign token (`ct`) identifies the website page; buttons on the same page share a campaign. The media type is `mt=8`.

| Page | Campaign token |
| --- | --- |
| Homepage | `website-home` |
| iPhone border guide | `website-iphone-guide` |
| HDR and EXIF guide | `website-hdr-exif` |
| Black-border guide | `website-black-borders` |
| App comparison | `website-app-comparison` |
| Instagram format guide | `website-instagram-formats` |
| Instagram carousel guide | `website-carousel-guide` |
| Apple changelog | `website-changelog` |
| Android changelog | `website-android-changelog` |

The homepage's Safari Smart App Banner uses `website-home` through its `affiliate-data` field. In HTML attributes, write query separators as `&amp;`; the browser resolves them to `&` in the URL. Preserve any existing destination parameters, such as `see-all=reviews`.

When adding a page, choose a campaign name of at most 30 characters, reuse the provider token, and keep download links instrumented with `data-umami-event="app-store-download"` plus a meaningful `data-umami-event-location`. Campaigns identify the page containing the link; use Umami to inspect how visitors reached that page.

After deployment, view **Analytics → Metrics → Add Filter → Campaign** in App Store Connect. Reporting takes at least 24 hours and requires sufficient volume; Apple documents at least five first-time download users for a campaign to appear, with thresholds for individual metrics. A missing campaign is not evidence of zero downloads. See [Apple's campaign-link guidance](https://developer.apple.com/help/app-store-connect-analytics/acquisition/campaign-links).
