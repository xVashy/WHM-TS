## Exim Mail Queue Flushing
When you need to force an immediate delivery attempt for stuck messages such as after fixing a network issue, resolving a DNS or TLS problem, cleaning up a spam compromise, or unblocking a rate-limit.

### 1. Check Stuck Queue Count
\`\`\`bash
exim -bpc
\`\`\`

### 2. Force Delivery of Queued Messages
\`\`\`bash
exim -qff
\`\`\`
