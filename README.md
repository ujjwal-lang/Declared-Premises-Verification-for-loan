# Customer-led premises verification

A self-serve mobile journey that lets a borrower verify their declared residential or business address from their own phone — and that reaches a decision without a person reviewing the submission.

Built as a product case study for a lending context. Concept work only; not affiliated with or endorsed by any lender, and no brand assets are reproduced.

---

## The problem

Address verification today is already self-serve — it's just badly built. A customer is asked over WhatsApp, finds a third-party GPS camera app, and sends a photo back. WhatsApp strips the EXIF data and compresses the image, so the genuine location evidence is destroyed by the channel collecting it. The workaround is burning coordinates into the pixels as visible text, which the app vendors themselves describe as not tamper proof.

A credit officer then looks at the result and decides whether it's good enough. They can judge whether a photo is sharp. They cannot judge whether it's recent, whether it's the right place, or whether that person took it. **The artifact doesn't contain the answer to the question being asked.**

So the manual step worth removing isn't a field visit — it's that review.

---

## Running the prototype

Open `index.html` in a browser. That's it — no dependencies, and it works offline.

On desktop it renders in a phone frame with an explanation panel alongside. On mobile it goes full-bleed with the panel hidden, and demo controls move behind a gear button.

**Demo controls** let you switch three things:

- **View** — the borrower's journey, or the credit ops console
- **Persona** — five borrowers with different failure modes (salaried renter, shopkeeper, driver with no premises, home-based business, low digital confidence in a rural area)
- **Outcome** — verified, quality retry, integrity flag, face mismatch, or permission denied

Worth trying: run the same persona through *quality retry* and then *integrity flag*. Same customer, same moment, deliberately opposite information design.

---

## Design decisions worth knowing

**The pin replaces the geocode.** Indian addresses don't reliably geocode to a door, so the customer drops a pin at their own doorstep and it's stored as a [DIGIPIN](https://dac.indiapost.gov.in/mydigipin/home) — India Post's 4-metre grid code. The allowed drag radius scales with how well the address could be placed on a map in the first place; for a village address there's no constraint at all.

**Verbose on quality failures, generic on integrity failures.** Telling someone their photo is dark helps them. Telling a fraudster their location looked simulated is free tuition.

**Nothing rejects anyone.** Every branch exits to one of three rails — self-serve, assisted capture, or a booked visit. Verification failure changes the rail; credit policy separately decides what a lower assurance tier means.

**One capture, two artifacts.** A short guided video for continuity, with full-size stills taken automatically on each hold-still beat. The video proves a nameplate is on a real building; the stills are what OCR and face match actually run on.

**Score and reason codes, not a verdict.** The borrower sees plain language. The score, the codes and the evidence live in a separate credit ops surface. Humans audit decisions in aggregate; they don't adjudicate individual photographs.

---

## What it doesn't do

Someone who fixes a fabricated nameplate to a neighbour's door will pass. Consumer GPS can't separate flat 402 from 302, and no design can claim otherwise — collections still finds them at the right building, so that's a data-quality defect rather than a loss.

The real defence is cost. Today fraud is a forged text overlay made in thirty seconds. After this it means travelling to a real address and staging a scene with your own face on camera. Organised fraud — where losses actually concentrate — is caught by comparing applications against each other, not by examining any single one.
