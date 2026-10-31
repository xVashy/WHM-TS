## WP-CLI Commonly used commands.
You can run these commands if you have access to the terminal or ssh.
Make sure you are on the public_html for apache or htdocs for nginx.


## WP-CLI Core Checksum Audit
one of the most efficient ways to verify the integrity of a WordPress installation and immediately detect unauthorized or malicious modifications to core files
### Verify Core Files
\`\`\`bash
wp core verify-checksums --allow-root
\`\`\`
