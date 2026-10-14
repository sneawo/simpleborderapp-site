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

## HDR export example

The HDR and EXIF guide uses a lazy-loaded, 960 × 1200 HDR preview in a `<picture>` element. AVIF-capable browsers receive `i/examples/hdr-iphone-13-preview.avif` (138,406 bytes, BT.2020/PQ, 10-bit); `i/examples/hdr-iphone-13-preview.jpg` is a 349,694-byte Ultra HDR gain-map JPEG fallback with a Display P3 SDR base. Both were resized and re-encoded from the full export's base image and embedded gain map. Neither preview includes EXIF location metadata. The JPEG's SDR base remains usable when a decoder does not support its gain map. AVIF delivery is based on format support, allowing the browser to tone-map HDR for the current display rather than relying on an HDR media query.

The source's secondary JPEG was extracted with ExifTool. FFmpeg resized the SDR base to 960 × 1200 and the gain map to 480 × 600 with Lanczos filtering. Google's `libultrahdr` v2.0.2 (`e5f5a022fe96fc4dc2ee35c19f733a50df807abe`), built with ISO and XMP metadata enabled, repackaged those images using the source's gain-map values: log2 minimum/maximum gain 0 / 2.237210, gamma 1, SDR/HDR offsets 0.000010, and log2 display headroom 0 / 2.999080. The logarithmic gain and headroom values were converted to linear values for the codec API. The source's Display P3 ICC profile is retained in the base JPEG.

The HDR AVIF was encoded from the codec's linear half-float HDR decode, unpacked directly to planar 32-bit float to retain values above 1.0, then converted from Display P3 to BT.2020/PQ at 203 nits reference white using FFmpeg's zscale filter, with 10-bit 4:4:4 AV1 at CRF 24. The JPEG passes the codec's HDR probe and decodes to finite linear values above SDR white (peak 4.359375 in this decode). A round trip through AVIF gives a peak of about 4.54; a white-border sample remains about 2.00 in both files. Apple's Core Image reports HDR headroom 4.9261084 for the AVIF. These are file/decode checks, not a claim that the developer has visually verified the new web preview on every browser or display.

`i/examples/hdr-iphone-13-export.jpg` is the unchanged, full-size file supplied by the app developer on October 14, 2026: 3395 × 4244 pixels, 6,189,558 bytes. Its SHA-256 is `236698782968a30ba1768d556bcc11e91411cf1782ad6555da9a5b02b34ad3e9`. It retains the source metadata, including location and the embedded HDR gain map. It is linked with a `download` attribute and the `hdr-export-download` Umami event; it is not an inline image or preloaded resource. The page recommends opening the downloaded JPEG in Photos or another HDR-capable viewer, since browser rendering can show SDR.

The developer reported seeing HDR on a MacBook screen and an iPhone. The exact display models, viewer versions, and app build were not recorded. This is a single exported file with a visual check, not a controlled before/after HDR preservation test. The August Sony metadata measurements are a separate example.
