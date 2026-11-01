# Gmail search queries for lead discovery

Run each of these (with the date filter and the standard exclusions appended), merge results by thread ID, and de-duplicate.

Standard exclusions: `-category:promotions -category:social -from:noreply -from:no-reply -from:notifications -in:sent`

## Direct inquiry
- `(quote OR quotation OR estimate OR pricing OR "how much" OR budget OR proposal)`
- `(website OR "web app" OR "mobile app" OR app OR portal OR dashboard OR software)`
- `(developer OR "development" OR "build" OR "develop" OR redesign OR revamp)`
- `(enquiry OR inquiry OR requirement OR "looking for")`

## Specific services
- `(whatsapp bot OR chatbot OR automation OR "AI" OR integration)`
- `(CRM OR ERP OR "inventory" OR "billing" OR "booking system" OR "management system")`
- `(ecommerce OR "online store" OR shopify OR "payment gateway")`

## Platforms and referrals
- `from:(upwork.com OR freelancer.com OR linkedin.com OR toptal.com OR fiverr.com OR guru.com)`
- `(referred OR referral OR "recommended you" OR "gave me your" OR "got your contact")`

## Warm threads
- `in:inbox is:unread` (scan for anything business-shaped the above missed)
- `(meeting OR call OR demo OR "let's discuss" OR "connect")`
- `(proposal OR "follow up" OR "following up")` — replies to the user's outreach

## Existing clients (upsell)
- Threads with senders the user has previously sent invoices or proposals to: `(invoice OR "change request" OR "new feature" OR "phase 2" OR "additional")`
