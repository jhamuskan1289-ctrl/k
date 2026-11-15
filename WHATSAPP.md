# WhatsApp in Kinora

## README section (paste into your README.md)

### WhatsApp integration
Kinora connects to WhatsApp in two ways:
1. **Click-to-chat (works everywhere, no setup).** "Share on WhatsApp" on the Clinic tab and "Remind family on WhatsApp" on the Medicines tab open WhatsApp with the message already written. Sharing health data needs the person's consent switch.
2. **Automatic reminders (server sends the message).** When Twilio keys are set on the server, the refill reminder is sent straight to the family member's WhatsApp, with no tap needed. Without keys, the app falls back to click-to-chat.

Server settings (Render, Environment tab):
| Name | Value |
|---|---|
| TWILIO_ACCOUNT_SID | from the Twilio console |
| TWILIO_AUTH_TOKEN | from the Twilio console |
| TWILIO_WHATSAPP_FROM | whatsapp:+14155238886 (Twilio sandbox number, the default) |

Limits: 10 messages per sign-in session per hour. The server never stores phone numbers from this feature.

## Setting up automatic sending (free sandbox, about 10 minutes)
1. Make a free account at twilio.com and open Messaging > Try it out > Send a WhatsApp message.
2. The page shows a sandbox number and a join code like "join word-word". From the phone that will receive reminders, send that code to the sandbox number on WhatsApp. (Every receiving phone must do this once; it is a sandbox rule.)
3. Copy your Account SID and Auth Token from the Twilio console home page.
4. In Render: your service > Environment > add TWILIO_ACCOUNT_SID and TWILIO_AUTH_TOKEN > Save. Render restarts.
5. In Kinora: sign in with the real OTP flow (not "Explore the demo"), save a family member's phone number, open Medicines, tap "Remind family on WhatsApp". A green "Reminder sent on WhatsApp" message appears.

Demo mode ("Explore the family demo") never sends automatically; it opens click-to-chat instead.

## What to tell judges
"Kinora is linked to WhatsApp. Families can share a consented health summary on WhatsApp in one tap, and low-medicine refill reminders go to the caregiver's WhatsApp automatically through the Twilio WhatsApp API from our Flask backend."
Be honest that it runs on the Twilio sandbox; production needs a Meta-verified WhatsApp Business number and approved message templates.

## Judge Q&A
- **Is it real or a demo?** Real Flask server and database. WhatsApp sending uses Twilio's sandbox for the hackathon.
- **Why Twilio?** It is the fastest official route to the WhatsApp Business API without waiting for Meta approval.
- **Privacy?** Summaries only share after the person switches consent on. The server only forwards the message and keeps no copy.
- **Abuse?** Sending needs a signed-in session and is capped at 10 per hour.
- **What next?** Verified WhatsApp Business number, templates for daily medicine reminders, and sending OTP codes over WhatsApp.
