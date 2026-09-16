# Conference landing page

Static page for GitHub Pages. To point it at a new conference, edit two lines near the bottom of `index.html`:

    var CALENDLY = "https://calendly.com/paul-tyler-zinnia/<event-slug>";
    var CONFERENCE = "Meet me at <Conference name>";

Add a phone number to `paul-tyler.vcf` with `TEL;TYPE=CELL:+1...` if you want it in the saved contact.
Deliberately omitted: this repo is public, so the file is crawlable and the number would stay
in git history permanently. The Calendly event already collects the invitee's mobile, so the
exchange happens one-to-one with people who actually booked.

## The headshot exists twice, on purpose

It's inlined as a base64 `data:` URI in `index.html` **and** kept as `paul-tyler.jpg`.
Don't "optimize" the inline copy away: an external `<img>` silently breaks when the page is
opened as a local `file://` (double-clicked from Finder), and inlining also makes it one
request instead of two on conference wifi. The `.jpg` has to stay too — `og:image` and the
favicon need a real file URL and can't accept a data URI. Re-inline after replacing the photo:

    python3 -c "import base64;b=base64.b64encode(open('paul-tyler.jpg','rb').read()).decode();print(b)"

## Design

Urbanist (Google Fonts) throughout, Zinnia card language: white cards on `#F8F8F8`, `#E2E4E8` borders,
12px radius, `0 2px 6px rgba(0,0,0,.06)` shadow. Hero card carries the eyebrow, headshot, name, and the
primary Book button, with Save contact / LinkedIn as a pair beneath it.

## Colors

Zinnia brand, with one deliberate deviation. No stock Zinnia orange reaches 4.5:1 on white
(`#F46C00` is 3.00:1, `#FB471F` is 3.49:1), so white text on a brand-orange fill fails WCAG AA.

- **Decorative / non-text** — true brand color: the top rule uses the full
  `#FFC600 → #F46C00 → #FB471F` gradient, and the headshot ring is `#F46C00`.
- **Anything text touches** — deepened: links are `#C24E00` (4.51:1 on the `#F8F8F8` paper),
  and the primary button fills `#C24E00 → #A83C12` so its white label clears 4.79:1 at the
  lightest point.

Don't swap the button back to `#F46C00`; it drops the CTA to 3.00:1. The button's `small`
is plain white for the same reason — a peach tint falls to 4.06:1 at the light end of the fill.

Deploy: push these files to a repo, Settings → Pages → Deploy from branch (main, root).
