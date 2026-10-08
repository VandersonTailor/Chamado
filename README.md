# Chamado: IT help-desk ticketing with a WhatsApp chatbot

Help-desk system built for the IT support team of an urban bus transport company. Employees open tickets either through a web form or by talking to a WhatsApp chatbot, and the support team follows everything on a login-protected panel that updates in real time.

## How it works

- **Web form** (`/chamado`): the employee fills in name, department and problem and receives a protocol number
- **WhatsApp chatbot:** a guided conversation (menu of common problems, description, department, machine IP) that validates each answer and opens the ticket automatically
- **Admin panel** (`/painel`): session login, ticket list, status updates and history
- **Live updates:** new tickets are pushed to the panel over WebSocket
- **Group notification:** an internal endpoint posts each new ticket to the support team's WhatsApp group

## Tech stack

- Node.js (ES modules), Express, express-session
- [Baileys](https://github.com/WhiskeySockets/Baileys) for the WhatsApp connection
- WebSocket (`ws`) for real-time updates
- JSON files for storage (tickets and protocol counter)

## Structure

```text
novo modo de chatbot - Copia/
|-- server.js    # web server: form, login, panel, ticket updates (port 3000)
|-- index.js     # WhatsApp bot, WebSocket server (8080) and bot API (4000)
`-- public/      # form, login and panel pages
```

## Running locally

Requirements: Node.js 18+ and a WhatsApp account to pair with the bot.

```bash
cd "novo modo de chatbot - Copia"
npm install express express-session node-fetch dotenv ws @whiskeysockets/baileys qrcode-terminal chalk

node server.js   # web form and panel on http://localhost:3000
node index.js    # bot: scan the QR code printed in the terminal
```

Before running, define the panel users and the session secret in `server.js` (they are intentionally left empty in this repository).

## Notes

- The chatbot messages and the interface are in Portuguese.
- The front-end files in `public/` are the minified production build.
