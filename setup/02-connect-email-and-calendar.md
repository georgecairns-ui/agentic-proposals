# Step 5: connect email and calendar

Goal: you can read every work inbox and calendar they use, each proven with a real read, and you've read the last 30 days. That's how you see what each client asked for and **confirmed in writing** (budget, scope, dates, who decides), spot new requests for a proposal or a quote, and find the clients they're talking to and the proposals they've already sent. The calendar shows which clients they're meeting. Ask about email and calendar before any other connection. One that is waiting on someone else is parked, and setup goes on.

## 5.1 One sentence on why, then their inboxes

> This is the big one. Clients confirm the important things by email, so when I write a proposal I'll read your emails with that client, in every inbox, and use exactly what they agreed. I never send, reply to or delete anything.

Then list back every address from step 1 in one short table, and check it with them:

| Address | Where it lives | Can I connect it? |
|---|---|---|
| james@cloudsocials.example | Outlook, work account (Microsoft 365) | Yes, with the Microsoft 365 connection. Your IT team may need to approve it |
| james.thorpe@gmail.example | Gmail | Yes, with the Gmail connection |

Add the calendar too, if it's somewhere else. If there's only one address, one line will do.

## 5.2 Connect each one, and check for yourself

Find the guide for each inbox and calendar:

| They use | Guide |
|---|---|
| Gmail or Google Workspace, Google Calendar | `setup/connections/gmail-and-google-calendar.md` |
| Outlook or Microsoft 365 with a work account | `setup/connections/microsoft-365.md` |
| Outlook.com or Hotmail (a personal Microsoft account) | `setup/connections/microsoft-365.md`: on Pro and Max it connects as a personal account; on Team and Enterprise there's no connector for it, so go to 5.5 |
| iCloud, Yahoo, a hosting company's email or another provider | There's no Claude connector for it. Go to 5.5 |

Email and calendar can come from different providers (for example work email in Outlook and meetings in Gmail). Find the guide for each separately. One with no connector goes to 5.5; every other one still goes through 5.2 and 5.3 and must be proven.

Then look up this session's connections (`session_connectors_status`) and act on what you find, for each inbox and calendar connector:

| What you find | What you do |
|---|---|
| It's there and on | Go to 5.3 |
| It's there but switched off for this session | Switch it on (`set_session_connector_enabled`). They'll be asked to approve: tell them that's expected. It works from your next message, so end this message by saying you've switched it on and will check it next |
| It isn't there | Give them the path from the guide, in their guide mode: open Connectors (`setup/connections/where-to-click.md` says where, for their plan), then the app's name, then Connect, then sign in on Google's or Microsoft's own page and approve. Ask them to tell you when it's done, then look again |
| It needs signing in (`needs_auth`) | Tell them the one thing to do: open Connectors (or type `/mcp` in this chat), choose it and sign in. Then look again |
| It's not working (`failed`) | Reconnect it (`reconnect_session_connector`). It's ready from your next message; end this one by saying so, then look again |
| They can't add it until someone else acts (their IT administrator or Claude Owner must approve it, or they need a password reset) | Park it as `waiting` (5.5) and connect the others now |

Keep going round this table until each one is on, or parked as `waiting`. Never ask for their email password: they sign in on Google's or Microsoft's own screen.

If the same connector can only be signed in to one account at a time and they have 2 addresses there, connect the main one and treat the other as having no connector of its own (5.5): it forwards into the connected one.

## 5.3 Prove it

With their permission, for each connected inbox read the subjects and senders of the 5 most recent emails, and read today's calendar, and say what you see in one line each, without quoting anything private:

> I can see your work inbox (last email from Dev at Hollins Lettings, 20 minutes ago), your Gmail (2 new today) and 3 things in your calendar today.

If a read fails, look up the connection status again and go back to 5.2. A connection only counts once a read has worked.

## 5.4 Read the last 30 days

Tell them first: "I'll now read the last 30 days of your email, to find the clients you're talking to and the proposals you've already sent. On a busy inbox this takes a few minutes. I'll keep you posted."

1. For every connected inbox, list every thread from the last 30 days, sent and received, by sender and subject only.
2. Leave out newsletters, receipts, automatic notifications and no-reply senders.
3. Open only the threads from real people, in batches. After each batch, one progress line: "Read 140 of 380 conversations, 6 clients so far."
4. **Clients and prospects:** anyone they're quoting, scoping or discussing work with, the same people step 8 sets up a folder for (`setup/proposals-04-your-client-folders.md`). For each one, save a short summary as `files/02-clients/_found-in-email/<Client Name>.md`, in the form step 8 uses for `Emails with <name>.md`: who they are, the contact (name, role, email), what they asked for, and what they **confirmed in writing** (budget, scope, dates, who decides) at the top, with their exact words where they matter. If that file already exists (a resumed setup), add to it instead of overwriting it: keep what is there and add what's new. Never whole threads. The folder starts with `_`, so the app doesn't treat it as a client; step 8 moves each summary into the right client's folder.
5. **Proposals already sent:** in their sent email, a proposal or quote they sent a client (an attachment with "proposal" or "quote" in its name, or an email that sets out options and prices). Add it to that client's summary: the date sent, the file name, what it offered and the prices as written, and whether the client has replied since. Don't add it to the app: it isn't one of the proposals you wrote.
6. Calendar: don't copy any events (Agentic Proposals has no calendar). Read the last 30 days of the calendar only to learn who they meet and what's recurring: add "met on <date>" to the summary of any client they met, and note their usual working days and hours in `context/routines.md`.

Every tool reads them as one inbox from now on. Keep the counts for the hand-over (emails read, clients found, proposals already sent). Nothing is sent, labelled, archived or marked as read.

## 5.5 The only ways past this step

Each inbox and calendar ends in one of these:

- **Proven:** 5.3 worked, and 5.4 (the 30-day read) is done for it.
- **No Claude connector for it** (iCloud, Yahoo, a hosting company's email, a personal Outlook address on Team or Enterprise, or a second address the connector can't take). Say plainly: "There's no Claude connector for [provider], so I can't connect to your email live." Offer the one alternative: forward it into an inbox that is connected. Record it as `no-connector`. No third-party service.
- **Waiting on someone else.** Their IT administrator or Claude Owner has to approve the connector, or they need a password reset. Offer to draft the message they can send (you never send it). Record it as `waiting`, with `waitingOn` (for example "IT") and the one thing still to do in `note`, and add a line to "Notes for next time" in `setup/progress.md`. Connect everything else they have now (for example their Gmail), then go on to step 6. When it's sorted, they press **Finish connecting** on Home or tell you, and you connect it, prove it and read its last 30 days then (`.claude/skills/connect-a-tool`, "Waiting on someone else").

When nothing at all can be connected for email yet, setup still goes on. Say plainly what won't work until email is in ("Until your email is connected, I can't read what your clients confirmed in writing. Proposals still work from what's in each client's folder."), and go on to step 6.

If they don't want to connect email at all, say in one line what won't work without it ("I won't be able to read what your clients asked for and confirmed in writing, or find the clients and proposals already in your email"), and ask once if they'd like to go ahead. If they still say no, stop setup here, note it in `setup/progress.md`, and tell them they can type `/setup` whenever they're ready. Don't go on to step 6 without email.

## 5.6 Record it

In `apps/home/data/connections.json` (format: `setup/connections/README.md`, "Recording a connection"): `"status": "connected"` and today's date in `checked` for each one proven, or `no-connector`, or `waiting` with `waitingOn`.

- **One inbox, email and calendar from the same provider:** 1 row, keyed `gmail-and-google-calendar` or `microsoft-365`, the same row step 1 started.
- **More than one inbox:** one row per inbox, with the address in `name`. Each keeps its guide's key; when 2 would share a key, add the address (`gmail-and-google-calendar-sam-gmail-com`).
- **Email and calendar from different providers:** each has its own row. A no-connector email row is keyed by the provider's name in lower case with hyphens (for example `icloud-mail`), and a proven calendar keeps its guide's key (`gmail-and-google-calendar` or `microsoft-365`). The same goes the other way round. When email and calendar come from the same provider and neither has a Claude connector (for example iCloud), they share 1 row keyed by the provider's name, for example `icloud`.

In `context/tools.md` ("Connected apps"): each inbox and calendar, how connected, today's date, "Read; save summaries into client folders", and "Never send, reply, forward, delete, archive, label or unsubscribe". Tick step 5 in `setup/progress.md`, noting anything `waiting`.

## Rules for their inbox, from now on

- Read only what a proposal needs: emails with that client. Don't read more than you need.
- Never send, reply, forward, delete, archive, label, mark as read, unsubscribe or accept an invite, even though the connection technically allows some of these.
- The covering email and follow-ups live on the proposal in the app; the person opens them in their email and sends them. Each goes from the address the client wrote to. Save a draft into their mailbox only if they ask for that specific email.
- Don't copy whole private emails into this folder. A short summary with the key facts and exact words that matter, in the client's folder, is enough.
