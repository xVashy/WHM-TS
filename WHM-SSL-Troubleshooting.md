# cPanel Hostname & SSL Troubleshooting Runbook

## 1. Locate DNS Management
Find where your domain's DNS is hosted by running this command on your server:
\`\`\`bash
dig ns domain.com +short
\`\`\`
* **Example:** `registrar-servers.com` indicates DNS is managed via **Namecheap**.

## 2. Get the Server Public IP
Retrieve your VPS public IPv4 address to point your A record to:
\`\`\`bash
curl -4 ifconfig.me
\`\`\`

## 3. Add the A Record
In your DNS provider's panel (e.g., Namecheap: **Domain List** → **Manage** → **Advanced DNS**):
* **Type:** A Record
* **Host:** `server`
* **Value:** [Your VPS Public IP from Step 2]

## 4. Verify Record Propagation
Check the authoritative nameserver:
\`\`\`bash
dig @dns1.registrar-servers.com server.domain.com A +short
\`\`\`
Check public DNS:
\`\`\`bash
dig @8.8.8.8 server.domain.com A +short
\`\`\`
*Both commands should return your VPS IP.*

## 5. Flush Local DNS Cache
* **Windows (Command Prompt as Admin):**
  \`\`\`cmd
  ipconfig /flushdns
  \`\`\`
* **Mac (Terminal):**
  \`\`\`bash
  sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder
  \`\`\`

## 6. Issue the SSL Certificate
Run the SSL check utility on your server:
\`\`\`bash
/usr/local/cpanel/bin/checkallsslcerts
\`\`\`
*Look for confirmation that domain control was validated for the hostname.*

## 7. Restart cPanel Daemon & Test
Restart the web service:
\`\`\`bash
/usr/local/cpanel/scripts/restartsrv_cpsrvd
\`\`\`
Open your browser and navigate to `https://server.domain.com:2087`. Click the padlock to verify the Let's Encrypt certificate.
