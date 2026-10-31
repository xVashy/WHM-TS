Find where DNS is hosted
On the server, run: dig NS domain.com +short. The result tells you where DNS is managed (for example, registrar-servers.com means Namecheap). The hostname's A record must be added there.
2
Get the VPS public IP
On the server, run: curl -4 ifconfig.me. This returns the VPS's public IPv4 address, which the A record will point to.
3
Add the A record for the hostname
In the DNS host's panel (Namecheap: Domain List → Manage → Advanced DNS), add an A record. Host: the hostname part, for example server. Value: the VPS IP from step 2.
4
Verify the record is live
Check the authoritative nameserver: dig @dns1.registrar-servers.com server.domain.com A +short. Then check public DNS: dig @8.8.8.8 server.domain.com A +short. Both should return the VPS IP. If they do, the record is live.
5
Flush local DNS
Windows: run ipconfig /flushdns in Command Prompt. Mac: run sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder in Terminal. Then fully restart the browser. Check what your PC resolves with nslookup server.domain.com.
6
If still stale, add a hosts file entry
If your network's DNS still says the domain doesn't exist but nslookup server.domain.com 8.8.8.8 works, add a hosts entry: VPS-IP server.domain.com. Windows file: C:\Windows\System32\drivers\etc\hosts (open Notepad as Administrator). Mac: sudo nano /etc/hosts. Flush DNS again afterwards.
7
Issue the SSL certificate
On the server, run: /usr/local/cpanel/bin/checkallsslcerts. Look for the line saying domain control was validated for the hostname. Warnings about other subdomains (mail, webmail, autodiscover) with no DNS records can be ignored.
8
Restart cPanel and confirm
On the server, run: /scripts/restartsrv_cpsrvd. Fully reopen the browser and go to https://server.domain.com:2087. Click the padlock and confirm the certificate is issued to the hostname by Let's Encrypt. AutoSSL renews it automatically, so keep the A record in place. Remove the hosts entry once your DNS catches up.
