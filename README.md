# National Global Academy website

This is the existing NGA Node static-site generator, updated in place. The user chose to retain this stack rather than migrate to Next.js. Node 18 or newer is required.

```sh
npm run build
npm run check
npm start
```

The static output is generated in `dist/`. The only public pages generated are Home, `/courses/all/`, six course detail pages, Contact, About, the Guides index and three existing guide articles. `/admin/` is unlinked and is a separate staff setup screen. Old industry and career URLs redirect to corresponding course sections. Old admissions and legal pages were removed. The prior DCHM and blog URLs retain redirects where configured. Do not treat the preview or an unverified URL as a production deployment.

## Important: claims and decisions to verify

The announcement's 12-seat figure and the nine Why Choose statements, including earnings and the licence guarantee, were supplied in the 17 November request. They are not independently verified by this build. NGA must substantiate them and ensure they remain accurate before publication. Likewise confirm the listed extra industry-card courses, the first two Professional Program certifications, the accommodation/lunch inclusions, and the admissions response-time statement. The extra card names do not have newly invented detail pages. Hours are deliberately omitted at the user's direction. Course certificate names remain blank until supplied. The exact supplied cost FAQ is a user-approved exception to the general prohibition on fee and medical wording.

The confirmed displayed address is `Bhutani Alphathum, Sector 90, Noida, Uttar Pradesh 201304`. Google supplies the embedded map and directions, so a network connection is necessary. Check the map pin and postal code with the academy on the actual deployment: some public listings use 201305. No tower, floor or office number is assumed.

## Admin and storage limitations

The `/admin/` panel is not linked from the public site. The static Vercel deployment has **no writable admin API, no persistent enquiry database and no live login**. Its login is disabled until a backend is configured. The counselling form prepares a WhatsApp message; it does not save an enquiry on static hosting, and the visitor must send the message.

A **local demonstration only** is implemented in `server.mjs`. NGA supplies credentials using environment variables, never committed in the project. No live account or password is included. Set `NGA_ADMIN_EMAIL`, `NGA_ADMIN_PASSWORD`, and optionally `NGA_DATA_FILE` using your own secure shell, then run `npm start`. The default data file is `$HOME/nga-private-data/content.json`, outside the public project. Never place private data in `public/`, `dist/`, a repository, or a ZIP. Use a trusted local machine with test data only. This demonstration is not production security, has not been audited, does not encrypt its data, and does not support multiple instances. Sessions are process-local and expire after four hours. Sign-in includes basic throttling and same-origin checks; stronger production controls are required.

The local demo supports enquiry listing, search/filter, status and notes, CSV export, course data editing, batch settings, contact details, JSON editing for selected page content and cards/logos, existing guide content, storage of verified-only testimonial records, and JPEG/PNG/WebP/MP4 uploads up to 15 MB. Uploaded files get random filenames and are not stamped with an NGA logo. Course and page editors use JSON and require valid complete records. New guide URLs are deliberately not created because only the existing guides were authorised; testimonials are not displayed on the public site because no testimonial section was requested. Settings for social links are stored, but no social links are displayed until explicitly designed. Admin changes cause a local static rebuild; they are not immediately editable on the static Vercel site. Where a batch announcement contains `Only N Seats Left`, changing the count replaces N. If the wording does not contain that pattern, update the announcement text explicitly.

For production, connect **Supabase PostgreSQL** for private enquiry and content records, staff-only Supabase Auth with MFA and roles, server-side validation and authorization in Vercel functions, and private object storage for approved uploads. Integrate public rendering or cache revalidation so edits appear immediately. Add audit logs, encrypted transport, backups, bot protection, retention controls, consent and a security/privacy review. NGA must create its own staff accounts and set service secrets as deployment environment variables. Do not use the local file fallback on Vercel or claim its ephemeral filesystem is durable. The local demo has no complete production-grade CMS or secure live media system.

## Assets and permissions

The supplied white NGA logo is used in the header/footer and the supplied NGA training image is used for the training and About layouts. The separately named transparent logo file was not provided in the workspace and has not been substituted or redrawn. The unbranded cruise ship used in the hero and Fast Track course is an **AI-generated representative image**, not a photograph of an actual NGA ship. Other course images are representative stock imagery. No relationship with pictured people, venues or employers is implied.

Four 16:9 industry videos are stored in `public/assets/videos/` with local poster frames and no audio. They autoplay muted and pause for reduced motion/offscreen. Pexels usage is subject to its licence: https://www.pexels.com/license/. Final branding, likeness, licensing and context should be reviewed before publication.

- Cruise: https://www.pexels.com/video/luxury-cruise-ship-at-sunset-34758780/ . A brightened overhead excerpt around 34–40 seconds is used because other portions, including the requested 3-second frame, show branding. The overhead image is less immediately recognisable as a ship than a bright side view; replace it with a licensed, unbranded daylight clip for a stronger match.
- Merchant Navy: https://www.pexels.com/video/aerial-view-of-cargo-ships-in-open-sea-37231586/ .
- Aviation: https://www.pexels.com/video/31923712/ . This cabin-crew clip is monochrome.
- Hospitality: https://www.pexels.com/video/man-checking-into-a-hotel-7820511/ . Reception excerpt is brightened.

The employer marks are representative logos, in the requested order; SVG sources are listed in `public/assets/logos/SOURCES.txt` and `NEW_SOURCES.txt`. The Viking SVG source specifies non-commercial purposes; obtain applicable rights, and verify all logo permissions and avoid implying an endorsement or employer partnership before any commercial publication.

## Faculty

The faculty section uses unnamed role cards. The optional `public/assets/team.json` can later contain verified `name`, `role`, `description`, `credentials`, and an optional `photo` path under `/assets/`. Publishing a changed static file requires deployment; a database-backed system would allow a managed update without one.
