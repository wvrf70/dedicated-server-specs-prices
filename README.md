# buy dedicated server: A Plain-English Guide to Specs, Real Prices and Picking the Right Configuration

Searching "buy dedicated server" usually lands you between two extremes: bargain listings that promise a server for the price of a pizza, and enterprise pages where the price is hidden behind a "contact us" wall. What's harder to find is the practical middle ground — what a current, honestly-specced bare-metal machine actually costs, what each line of the spec sheet means, and how to match a configuration to the job you're running.

This guide walks through all of it, using Sharktech's dedicated bare-metal lineup as the working example. The company publishes full configurations with transparent pricing on its dedicated servers page, includes DDoS protection on every service, and runs a 10Gbps network as standard, which makes it a useful reference point for what a no-games dedicated offering looks like right now. Every price and spec below comes from their current product page and official documents.

## What You're Actually Buying

A dedicated server is a physical machine leased to exactly one customer. No neighbors on the host, no hypervisor taking a cut of your CPU cycles, no noisy-neighbor surprises at 2 a.m. when someone else's cron job spikes the disk queue.

The distinction that matters here is "bare-metal." Plenty of hosts sell "dedicated servers" where you get the box but only OS-level access. A bare-metal dedicated server goes further: you get down to the hardware layer, can install a custom OS, partition disks however you want, and — if you're that kind of person — run your own virtualization stack on top of it. Sharktech's own FAQ draws this line explicitly: every server they sell is a bare-metal dedicated server with hardware-level access through their management panel, not just an OS login.

When a dedicated server is the right call:

- **Steady, resource-heavy workloads** — database clusters, game servers, video encoding, CI runners that hammer CPU and disk I/O around the clock. Cloud billing punishes exactly this pattern.
- **Predictable costs** — one monthly number, no egress surprises, no 40-line invoice.
- **Full control** — custom kernels, your own hypervisor, security requirements that rule out shared infrastructure.

When it isn't: short-term projects, spiky traffic, or a site that currently runs fine on a $10–50 VPS. If you don't know why you need exclusive hardware, you probably don't need it yet, and upgrading later is a normal path — Sharktech and most competitors help with migration when you outgrow a smaller box.

## Decoding the Spec Sheet Before You Spend Anything

Dedicated server listings throw around Xeon generations, U.2 bays, and bandwidth terms that read like a parts catalog. Here's what each piece actually does to your workload, using the current Sharktech lineup as the illustration.

### CPU: cores versus clock speed

The processor line tells you most of what you need to know about a config's personality:

- **Dual Xeon E5-2695v4 (36 cores at 2.1GHz)** — older Broadwell-generation silicon, but 36 cores across two sockets for cheap. Good for throughput jobs where individual threads are slow but you have plenty of them.
- **Dual Xeon Gold 6248 (40 cores at 2.5GHz)** — a newer Cascade Lake part with faster per-core performance. The general-purpose sweet spot of the lineup.
- **Dual Xeon Gold 6246 (24 cores at 3.3GHz)** — fewer cores, but each one runs 800MHz faster. This is the config for latency-sensitive work: game servers, real-time apps, anything where single-thread speed drives the experience.
- **AMD EPYC 7702P and Dual EPYC 7702 (64 and 128 cores at 2.0GHz)** — pure core count. Virtualization hosts, render farms, batch processing, anything embarrassingly parallel.

The rule of thumb: if your users feel every millisecond, buy clock speed. If your work is a queue of independent jobs, buy cores.

### RAM: base configs and the upgrade path

The current lineup ships with 64GB (entry configs) or 128GB DDR4, with documented upgrade options up to 1TB. Memory is one of the easiest things to under-buy and one of the most annoying to fix after deployment, so size it against your actual workload rather than the sticker price — the upgrade options are priced in the cart during ordering, so you can see the delta before committing.

### Storage: three different animals that all get called "drives"

- **SATA/SAS bays** — the bulk tier. The 3.5-inch bay configs accept upgrades up to 16TB SATA HDDs, the 2.5-inch bays top out at 4TB SATA SSDs. Backups, media libraries, archive data.
- **M.2 NVMe (2TB standard)** — the fast boot/app tier on every configuration in the lineup.
- **U.2 NVMe bays** — enterprise NVMe with upgrade options at 3.84TB, 7.68TB, and 15.36TB per drive. This is the tier for databases and VM storage where IOPS are the bottleneck.

A config with both M.2 NVMe and open U.2 or SATA bays gives you room to grow. A config with only NVMe bays (like the EPYC machines) trades flexibility for a cleaner storage layout.

### Network: what "10Gbps with 300TB/month" means in practice

Every configuration in the current lineup includes a 10Gbps port with 300TB of monthly transfer, upgradeable to 40Gbps or 100Gbps. Two things worth understanding about that number:

First, 300TB is enormous for normal traffic. Sharktech's own cart page breaks it down to roughly 9.86TB per day or 0.41TB per hour. A busy web application will use a fraction of that.

Second, it's metered, not unmetered. If you genuinely saturate a 10Gbps port around the clock, you'd burn through 300TB in about 67 hours of full-rate transfer (10Gbps is roughly 4.5TB per hour). Almost nobody does this, but if you're planning large-scale CDN egress or constant bulk replication, do the arithmetic first or ask about the heavier network tiers.

One more network point that's specific to this provider: DDoS protection is included on all services via their proprietary mitigation system, not sold as an add-on. Their acceptable use policy notes that mitigation is intended for normal usage patterns, and you can't attack your own servers to test it — a reasonable clause that keeps the protection usable for everyone on the network.

## The Full Lineup: All Current Configurations and Prices

Sharktech currently lists eight readily available bare-metal configurations. All include free setup, 10Gbps networking with 300TB/month, the included DDoS protection, the server management panel, and 24/7 support. Monthly and annual pricing below is taken directly from their product page:

| Configuration | CPU | RAM | Storage | Network | Monthly | Annual total | Order |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Dual E5-2695v4 (2.5" bays) | Dual Xeon E5-2695v4, 36 × 2.1GHz | 64GB DDR4 | 2TB M.2 NVMe + 6 × 2.5" SATA/SAS bays | 10Gbps, 300TB/mo | $259/mo | $2,641.80/yr | [ Order the $259/mo plan](https://portal.sharktech.net/aff.php?aff=1611&url=https://portal.sharktech.net/cart.php?a=add&pid=741) |
| Dual E5-2695v4 (3.5" bays) | Dual Xeon E5-2695v4, 36 × 2.1GHz | 64GB DDR4 | 2TB M.2 NVMe + 6 × 3.5" SATA/SAS bays | 10Gbps, 300TB/mo | $269/mo | $2,743.80/yr | [ Contact sales](https://portal.sharktech.net/aff.php?aff=1611&url=https://sharktech.net/free-consultation) |
| Dual Gold 6248 (3 bays) | Dual Xeon Gold 6248, 40 × 2.5GHz | 128GB DDR4 | 2TB M.2 NVMe + 3 × 3.5" SATA/SAS bays | 10Gbps, 300TB/mo | $299/mo | $3,049.80/yr | [ Order the $299/mo plan](https://portal.sharktech.net/aff.php?aff=1611&url=https://portal.sharktech.net/cart.php?a=add&pid=660) |
| Dual Gold 6248 (6 bays) | Dual Xeon Gold 6248, 40 × 2.5GHz | 128GB DDR4 | 2TB M.2 NVMe + 6 × 2.5" SATA/SAS bays | 10Gbps, 300TB/mo | $309/mo | $3,151.80/yr | [ Order the $309/mo plan](https://portal.sharktech.net/aff.php?aff=1611&url=https://portal.sharktech.net/cart.php?a=add&pid=636) |
| Dual Gold 6246 (high clock) | Dual Xeon Gold 6246, 24 × 3.3GHz | 128GB DDR4 | 2TB M.2 NVMe + 3 × 3.5" SATA/SAS bays | 10Gbps, 300TB/mo | $309/mo | $3,151.80/yr | [ Order the 3.3GHz plan](https://portal.sharktech.net/aff.php?aff=1611&url=https://portal.sharktech.net/cart.php?a=add&pid=814) |
| Dual Gold 6248 (U.2) | Dual Xeon Gold 6248, 40 × 2.5GHz | 128GB DDR4 | 2TB M.2 NVMe + 6 × U.2 NVMe bays | 10Gbps, 300TB/mo | $329/mo | $3,553.20/yr | [ Order the U.2 config](https://portal.sharktech.net/aff.php?aff=1611&url=https://portal.sharktech.net/cart.php?a=add&pid=766) |
| AMD EPYC 7702P | EPYC 7702P, 64 × 2.0GHz | 128GB DDR4 | 2TB M.2 NVMe + 10 × U.2 NVMe bays | 10Gbps, 300TB/mo | $499/mo | $5,089.80/yr | [ Order the EPYC 7702P](https://portal.sharktech.net/aff.php?aff=1611&url=https://portal.sharktech.net/cart.php?a=add&pid=729) |
| Dual AMD EPYC 7702 | Dual EPYC 7702, 128 × 2.0GHz | 128GB DDR4 | 2TB M.2 NVMe + 10 × U.2 NVMe bays | 10Gbps, 300TB/mo | $699/mo | $7,129.80/yr | [ Contact sales](https://portal.sharktech.net/aff.php?aff=1611&url=https://sharktech.net/free-consultation) |

Every row can be upgraded at order time: RAM up to 1TB, CPU swaps within each platform, additional NVMe (including the 15.36TB U.2 drives), and 40G/100G network tiers. If a configuration you want isn't listed, their sales team sources hardware from vendors for custom builds — you can 👉 [get a free consultation for a custom build](https://portal.sharktech.net/aff.php?aff=1611&url=https://sharktech.net/free-consultation) directly.

One caveat the company states openly on the page: because of industry-wide hardware shortages, delivery in under 24 hours can't be guaranteed, especially for customized machines. If you have a hard launch date, order with margin.

## Matching a Configuration to Your Job

The table is only useful if you know which row is yours. Based on the specs above:

**Game servers and latency-sensitive apps.** The 24-core Gold 6246 at $309/mo is the natural fit — 3.3GHz cores handle player simulation and tick loops better than more-but-slower cores. If budget matters more than frames, the $259 Dual E5-2695v4 handles moderate player counts fine. Included DDoS protection is the quiet advantage here; Sharktech's own customer testimonials include game operators describing sustained 3–8Gbit attacks absorbed without service interruption, which is the exact failure mode that gets cheaper hosts to null-route your IP.

**Web applications, APIs, and databases.** The Dual Gold 6248 at $309/mo with six drive bays gives you compute plus storage flexibility, or step up to the $329 U.2 config if your database lives and dies on NVMe IOPS. The 10Gbps port plus 300TB means bandwidth stops being a planning constraint.

**Virtualization hosts, render farms, and parallel batch work.** The EPYC 7702P at $499/mo (64 cores, 10 U.2 bays) or the dual-EPYC machine at $699/mo (128 cores) are built for exactly this. Running your own VM fleet on dedicated silicon at a fixed monthly price is the classic escape route from hyperscaler bills that scale with your success.

**Bulk storage and backups.** The 3.5-inch bay configs accept 16TB HDD upgrades, which is the cheapest path to serious capacity. Media archives, backup targets, log retention.

If none of these map cleanly onto your needs, that's what the consultation link is for — custom CPU, GPU, or memory arrangements are a normal part of their sales process rather than an exception.

## Where the Real Discount Lives: Billing Cycles

You won't find coupon codes on the official site, and the "verified promo codes" floating around third-party coupon aggregators aren't something I can confirm, so treat those with suspicion. The genuine, always-on saving is the billing cycle discount built into the pricing table:

- **Quarterly billing** works out to roughly 5% off the monthly rate
- **Semi-annual** around 10% off
- **Annual** around 15% off on most configurations

Run the numbers on two examples. The $259/mo Dual E5-2695v4 costs $2,641.80 billed annually — $220.15 per month, a $38.85 monthly saving. The $499/mo EPYC 7702P drops to $424.15/mo on annual billing ($5,089.80 total), saving you just under $900 a year. Discount depth varies slightly by configuration (the $329 U.2 machine's annual price works out to 10% off rather than 15%), so check the totals in the cart before choosing a cycle — you can 👉 [configure the E5-2695v4 with annual billing](https://portal.sharktech.net/aff.php?aff=1611&url=https://portal.sharktech.net/cart.php?a=add&pid=741) and see the exact figures.

The catch, and it's an important one: per the Terms of Service, **all payments to Sharktech are nonrefundable**, including setup and recurring charges. Services auto-renew each term unless you cancel at least five days before the term ends (by email to their sales address), and billing disputes must be raised within 30 days of the invoice. This is standard for the dedicated server industry, but it changes the math on that 15% annual discount. My suggestion: if this is your first server with the company, pay monthly for a term, confirm the hardware and network behave the way you need, then move to annual billing on renewal. The 15% is still there when you're sure.

## Before You Click Order: The Checklist

A short list of things that are easier to know now than to learn from a ticket:

1. **Refunds don't exist.** TOS is explicit. Budget accordingly, and start smaller if uncertain.
2. **Cancellation needs lead time.** Five days before your term ends, or it renews.
3. **Delivery isn't instant.** Hardware shortages mean sub-24-hour provisioning isn't guaranteed; custom builds take longer.
4. **This is unmanaged infrastructure.** You handle the OS, patching, and software stack. Support covers the infrastructure layer and is available 24/7, but nobody is going to configure your firewall rules for you.
5. **OS and control panel options are priced in the cart.** Linux and BSD are free paths; Windows and panels like cPanel are line items — check their cost at configuration time, not after.
6. **Pick your location deliberately.** Five data centers are available: Los Angeles (near One Wilshire), Las Vegas, Denver (on the H5 Data Center campus), Chicago, and Amsterdam. Choose the one closest to your users — Amsterdam matters if your audience is European, LA if you're serving the Pacific side.
7. **Sanity-check your bandwidth plan.** 300TB/month covers almost every realistic workload, but it's metered. Constant bulk transfer at line rate will hit the cap in under three days of saturation.
8. **Custom requirements go through sales first.** GPUs, unusual memory amounts, specific storage layouts — a conversation before ordering beats a surprise after.

## What Actual Buyers Say

Third-party signal on Sharktech is limited but honest-looking. On Trustpilot the company averages 3.4 out of 5 across 13 reviews — a small sample that splits in both directions. Recent positive reviews focus on value (one December 2025 reviewer praises an $8/mo VPS as the cheapest on the market; a January 2026 reviewer calls their yearly VPS plan the best deal around) and uptime (a year of use with zero downtime reported). The negative side includes a detailed June 2025 billing dispute involving PayPal subscription charges after cancellation — refunded, but only after the customer pushed — and a serious 2022 data-loss complaint from the pre-current-era of the company.

The pattern is consistent with what you'd expect from an infrastructure-first provider: people buying raw hardware and network capacity at aggressive prices tend to be satisfied; people expecting managed-service hand-holding or friction-free billing edge cases tend not to be. The company has operated from Las Vegas since 2003, originally as a DDoS-protection-focused host, and its reputation in hosting communities rests on that network-engineering side of the house rather than on marketing.

## Short Verdict

If your search for "buy dedicated server" comes from running real workloads — game communities, production apps, virtualization fleets, an escape from unpredictable cloud invoices — the current Sharktech lineup is a legitimately transparent place to shop: published prices from $259/mo, free setup, DDoS protection included rather than upsold, 10Gbps standard with 300TB of transfer, and five data centers to choose from. The honest trade-offs are no refunds, unmanaged service, and provisioning that can take longer than a day.

If your budget tops out below $100/mo, there are cheaper dedicated boxes at big-name budget hosts — just read those spec sheets carefully, because older single-socket hardware on a 1Gbps port is a different product category from what's described above.

The practical next step costs nothing: 👉 [browse the current configurations and verify the pricing yourself](https://portal.sharktech.net/aff.php?aff=1611&url=https://sharktech.net/dedicated-servers/), or if your requirements don't fit any listed row, 👉 [talk to their sales team about a custom build](https://portal.sharktech.net/aff.php?aff=1611&url=https://sharktech.net/free-consultation) — they respond within hours, and the consultation is free.
