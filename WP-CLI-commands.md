## WP-CLI Commonly used commands.
You can run these commands if you have access to the terminal or ssh.
Make sure you are on the public_html for apache or htdocs for nginx.
##
* [WP-CLI Core Checksum Audit](#wp-cli-core-checksum-audit)
* [WP-CLI Core Download](#wp-cli-core-download-force-update--repair)
* [Permalink Fixes](#wp-cli-rewrite-rules-flush)

## WP-CLI Core Checksum Audit
One of the most efficient ways to verify the integrity of a WordPress installation and immediately detect unauthorized or malicious modifications to core files
### Verify Core Files
\`\`\`
wp core verify-checksums --allow-root
\`\`\`
or
\`\`\`
wp core verify-checksums
\`\`\`

## WP-CLI Core Download Force Update & Repair

Re-downloading core files using the `--force` flag allows you to overwrite corrupted or modified WordPress core files without affecting your `wp-config.php` file or the `wp-content/` directory (your themes, plugins, and uploads remain untouched).

### Prerequisites
Make sure you are in the root directory of your WordPress installation:
\`\`\`bash
cd /path/to/your/wordpress/site
\`\`\`

---

### 1. Re-Download & Overwrite Core Files
To forcefully download and replace all core WordPress files with clean versions matching your current environment:
\`\`\`bash
wp core download --force
\`\`\`
*If running directly as the `root` user on WHM/cPanel servers, append `--allow-root`:*
\`\`\`bash
wp core download --force --allow-root
\`\`\`
*Verification:* You will see output stating `Success: WordPress downloaded.`

---

### 2. Download a Specific WordPress Version
If you need to downgrade or lock the reinstall to a specific version (e.g., matching your database version):
\`\`\`bash
wp core download --version=6.4.3 --force --allow-root
\`\`\`
*Verification:* The CLI outputs confirmation that the specified version has been downloaded and extracted.

## WP-CLI Rewrite Rules Flush

Flushing rewrite rules regenerates your WordPress permalink structure and updates the `.htaccess` or server rewrite rules. This is essential for resolving 404 errors on custom post types, newly activated plugins, or updated URL structures.

---

### 1. Flush Rewrite Rules (Standard)
To flush rewrite rules cleanly while preserving your current permalink structure:
\`\`\`bash
wp rewrite flush
\`\`\`
*If running directly as the `root` user on WHM/cPanel servers, append `--allow-root`:*
\`\`\`bash
wp rewrite flush --allow-root
\`\`\`
*Verification:* The CLI outputs `Success: Rewrite rules flushed.`

---

### 2. Hard Flush Rewrite Rules & Regenerate .htaccess
If 404 errors persist, perform a hard flush to force WordPress to overwrite and regenerate the physical `.htaccess` file on disk:
\`\`\`bash
wp rewrite flush --hard --allow-root
\`\`\`
*Verification:* The CLI confirms rules are flushed and displays the regenerated `.htaccess` file rules.

---

### 3. Verify Core Integrity Afterwards
After re-downloading core files, run a checksum audit to verify all files match official WordPress hashes:
\`\`\`bash
wp core verify-checksums --allow-root
\`\`\`
*Verification:* Output confirms `Success: WordPress installation verifies against checksums.`
