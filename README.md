# ABC Tutoring prototype

Static, responsive prototype for Dana's tutoring service. Run `python3 -m http.server 8000`, then visit http://localhost:8000.

## Included
- Home, tutor listing with subject filters, booking flow and confirmation.
- Six sample tutors: four math, one science, one reading. Portraits are placeholders.
- Required parent and student details and Online/In person selection, one-hour available slots, immediate confirmation, no online payment. Session type appears in confirmation, management, and the booking_completed analytics event.
- Browser-local bookings remove their times from availability and survive refresh.
- Demo management: dana@example.com / demo1234. Edit/add tutors or mark them unavailable, manage availability, inspect bookings and simulated notification status.
- PostHog US integration configured with the supplied public project token. Explicit events only; parent/student names and email are not sent in custom event properties. Session recording and autocapture are disabled.

## PostHog dashboard
Create a dashboard named “ABC Tutoring — Booking overview” with:
1. Trend: `booking_completed`, total count, titled “Website bookings”.
2. Trend: `booking_completed`, breakdown by `subject`, titled “Bookings by subject”.
3. Funnel: `page_viewed` → `booking_completed`, unique users, titled “Visitor-to-booking conversion”.
4. Funnel: `tutor_list_viewed` → `booking_started` → `booking_time_selected` → `booking_completed`, unique users, titled “Where parents leave booking”.

All custom events have `prototype: true`. Automated smoke testing generates sample analytics. The management dashboard's figures are browser-local demo counts, not queries of PostHog. Use PostHog for cross-visitor analytics and its dashboard sharing link for the assessment submission.

## Publish
Upload these root files to the vichiaseeds/vichiaseeds.github.io repository. Configure GitHub Pages to publish from the root of the deployed branch. No build step or backend is required; hash routes work on Pages. Expected site URL: https://vichiaseeds.github.io/.

## Prototype boundaries
This is not a production booking system. Data lives in localStorage on each browser and is not synchronized. The demo password offers no security. Notifications are explicitly simulated, not delivered. Real authentication, shared booking storage with transactional conflict prevention, and notification delivery must be connected before real use. Dana's business phone, real tutor details/photos and meeting/location instructions are still needed. No payment processing is requested.

Unavailable tutors remain listed with booking disabled. Required fields and tutor grade ranges are validated. Booking writes use a Web Lock and recheck current availability to prevent overlapping one-hour sessions across tabs in the same browser. Slot changes preserve entered details. Different browsers/devices still require transactional shared storage.
