# VPS NVMe from $1.99 a month: what the cheap plans include, is NVMe worth the premium, and which tier fits your workload?

JustHost.asia lists NVMe VPS plans from **$1.99/mo**, and the tier most people should actually buy, Arcturus (1 core, 2 GB RAM, 30 GB NVMe), comes to **$5.53/mo when you pay for 12 months**. On this provider's own configurator, choosing NVMe over a SATA SSD on identical hardware adds $0.26 to $1.76 a month, which settles the storage question quickly. RAM and port speed are what decide whether a given tier is usable, and those vary a lot across the nine plans below.

What follows: the full tariff table with the 12-month rates, a plain explanation of what NVMe changes at the interface level, where the advertised price separates from what you actually pay, and which tier matches a small database, a container host, or one low-traffic site.

> **Quick pick:** Arcturus, 1 core / 2 GB RAM / 30 GB NVMe, **$5.53/mo on 12-month billing** (list price $6.92). Enough memory for a small MySQL or Postgres instance alongside an app, with a 300 Mbps fair-share port. Choose Vega at $10.75/mo (2 cores / 4 GB / 80 GB) if you build container images or compile on the box itself.
> 👉 [See the current Arcturus configuration and price](https://justhost.asia/en/services/vps/tariffs/arcturus?ref=196392)

## The full NVMe VPS lineup and what each tier costs

Every plan below uses NVMe storage and KVM virtualisation. The last column is the effective monthly rate when you pay for 12 months, which is the only figure worth comparing across providers.

| Plan | vCPU / RAM | NVMe disk | Fair-share port | Price on 12-month billing | Order |
| --- | --- | --- | --- | --- | --- |
| VPS Promo | 1 core / 512 MB | 5 GB | 10 Mbps (≈4+ TB/mo) | $1.99/mo † | [Order VPS Promo](https://justhost.asia/en/services/vps/tariffs/promo-c1r512nvme?ref=196392) |
| New Star | 1 core / 1 GB | 10 GB | 100 Mbps (≈31+ TB/mo) | $3.05/mo (list $3.81) | [Order New Star](https://justhost.asia/en/services/vps/tariffs/new-star-c1r1024nvme?ref=196392) |
| Sirius | 1 core / 1 GB | 20 GB | 300 Mbps (≈93+ TB/mo) | $3.88/mo (list $4.85) | [Order Sirius](https://justhost.asia/en/services/vps/tariffs/sirius?ref=196392) |
| Arcturus | 1 core / 2 GB | 30 GB | 300 Mbps (≈93+ TB/mo) | $5.53/mo (list $6.92) | [Order Arcturus](https://justhost.asia/en/services/vps/tariffs/arcturus?ref=196392) |
| Double Star | 2 cores / 2 GB | 20 GB | 200 Mbps (≈62+ TB/mo) | $5.67/mo (list $7.08) | [Order Double Star](https://justhost.asia/en/services/vps/tariffs/double-star-c2r2048nvme?ref=196392) |
| Alpha Centauri | 2 cores / 2 GB | 40 GB | 400 Mbps (≈124+ TB/mo) | $7.19/mo (list $8.99) | [Order Alpha Centauri](https://justhost.asia/en/services/vps/tariffs/alpha_centauri?ref=196392) |
| Bright Star | 4 cores / 4 GB | 30 GB | 300 Mbps (≈93+ TB/mo) | $7.84/mo (list $9.80) | [Order Bright Star](https://justhost.asia/en/services/vps/tariffs/bright-star-c4r4096nvme?ref=196392) |
| Vega | 2 cores / 4 GB | 80 GB | 500 Mbps (≈155+ TB/mo) | $10.75/mo (list $13.44) | [Order Vega](https://justhost.asia/en/services/vps/tariffs/vega?ref=196392) |
| Capella | 4 cores / 4 GB | 120 GB | 750 Mbps (≈232+ TB/mo) | $14.64/mo (list $18.30) | [Order Capella](https://justhost.asia/en/services/vps/tariffs/capella?ref=196392) |

† The promo tariff is listed at $1.99 and shows no separate 12-month reduction, unlike every other plan on the page.

Three things the table makes obvious. New Star, Double Star and Bright Star carry a note that they are available when you order three months or more. Larger configurations exist above Capella, up to 8 cores and 24 GB. And the jump from Arcturus to Alpha Centauri costs $1.66/mo for a second core and 10 GB more disk, while the jump from Arcturus to Vega costs $5.22/mo for the same extra core plus 50 GB and a faster port. If disk space or build speed is your constraint, Vega is the better buy; if you just need more CPU threads, Alpha Centauri gets there for less.

Prices are shown in dollars on the site; confirm the billing currency at checkout if you are paying from outside the United States.

## NVMe versus SATA SSD: what the interface changes, and what it doesn't

NVMe moves data over PCIe, while SATA SSDs are limited by the SATA III interface at roughly 550 MB/s. A mechanical disk sits at about 160 MB/s and has to wait for the head to reach the right sector. The gap that matters for a VPS is on random access rather than headline throughput, because a busy database or container host issues thousands of small reads and writes, not one big sequential copy.

|  | NVMe | SATA SSD | Hard disk |
| --- | --- | --- | --- |
| Interface | PCIe | SATA III | SATA III |
| Throughput ceiling | Multiple GB/s | ~550 MB/s | ~160 MB/s |
| Random access | Very high IOPS | Moderate IOPS | Limited by seek time |
| Moving parts | None | None | Spinning platters |

Those figures describe storage interfaces. They are not a guarantee of VPS performance, and no honest vendor can give you a single speed multiplier, because what you actually get depends on the host hardware, how much I/O is allocated to your instance, and what your workload does. Anyone quoting "100x faster" is comparing a best-case synthetic benchmark against a worst-case spinning disk.

Where the difference shows up on a real server: index scans and joins that have to reach disk, dependency installs and compile steps that sit waiting on I/O, pulling and unpacking container layers, writing logs at volume, and large imports or local backups. Where it shows up less: anything CPU-bound. A slow PHP page or a badly tuned query will not be rescued by faster storage, and you would get more from a higher CPU tier than from a faster disk.

## The NVMe premium, priced

JustHost's configurator lets you pick HDD, SATA SSD or NVMe on identical CPU and RAM, which makes the storage premium visible instead of theoretical. These are all 12-month rates:

| Same specs | HDD | SATA SSD | NVMe |
| --- | --- | --- | --- |
| 1 core / 512 MB / 5 GB | $2.60 | $3.12 | $3.38 |
| 2 cores / 2 GB / 25 GB | $8.80 | $10.56 | $11.44 |
| 4 cores / 4 GB / 50 GB | $17.60 | $21.12 | $22.88 |

NVMe costs $0.26 to $1.76/mo more than the SATA SSD version of the same box, and $0.78 to $5.28 more than the hard-disk version. At the small end, skipping NVMe saves less than the price of a coffee. At the top end, the $5.28/mo gap against a hard disk is real money over a year, but you are buying it for workloads where a spinning disk becomes the bottleneck within weeks.

The practical conclusion: on this provider, there is very little reason to pick the SATA SSD option. Either you are running something so light that HDD is fine, or you are running something disk-sensitive enough that the extra dollar or two for NVMe pays for itself.

👉 [Compare all NVMe VPS tiers and their 12-month rates](https://justhost.asia/en/services/vps/tariffs-all?ref=196392)

## Four numbers behind the sticker price

**List price versus 12-month price.** Every plan except the promo carries a 20% reduction for annual payment. Sirius is $4.85 list and $3.88 on 12-month billing; Capella is $18.30 list and $14.64. If you pay monthly, expect the list figure. That is a normal pattern in this market, and it cuts both ways: a provider advertising $2.09/mo may be quoting a two-year term with a renewal rate of $4.68/mo, which is what Network Solutions publishes for its entry NVMe plan. Before comparing two hosts, multiply the first-term price by the term length, add the renewal price for the remaining years, and divide by the total months.

**The port, not the traffic counter.** JustHost labels bandwidth "unmetered", and the parenthetical on each plan translates the port speed into a monthly volume: 10 Mbps is about 4+ TB, 100 Mbps about 31+ TB, 750 Mbps about 232+ TB. Fair-share means you are sharing that port with other instances on the host rather than getting a dedicated line. For a proxy, a VPN endpoint or a small site, the 10 Mbps promo port is fine. For serving large files or video, port speed becomes your real ceiling long before any traffic quota does.

**Three-month minimums.** New Star, Double Star and Bright Star are marked as available on orders of three months or more, so the $3.05 headline cannot be had on a one-month trial of those specific plans.

**Asia-Pacific traffic rules are where cheap plans bite elsewhere.** OVHcloud advertises unlimited traffic on its VPS range, but the footnote excludes its Mumbai, Singapore and Sydney data centres, where quotas run from 500 GB to 3 TB and overage is throttled to 10 Mbps. Exabytes reserves 80% of a Singapore VPS's bandwidth for local traffic and 20% for international visitors. Neither detail appears in the headline price. If your audience and your server are on different continents, read the bandwidth clause before the price.

## Support, backups, and what the reviews actually say

Nothing in the plan listings mentions an automated backup service, so treat backups as your own responsibility until support tells you otherwise: a scheduled `restic` or `borg` job to object storage costs a few dollars a month and removes the entire category of disaster. DDoS protection against the main attack types is included, and the platform is KVM, so you get full root access and can install any Linux distribution.

Public reviews of justhost.asia on Trustpilot skew negative, and the complaints cluster around two things rather than the hardware: support that responds with a bot and no visible human agent, and long silences during outages, including one reviewer describing a full platform outage with no status update for 15 hours. The same reviewers repeatedly call the prices the lowest they have found. Both things can be true at once, and the sensible response is to price that risk in. Keep your own off-server backups, keep configuration in version control so a rebuild is a 20-minute job rather than a lost weekend, and do not run anything where an hour of downtime costs more than the server does.

Managed alternatives exist and cost accordingly: Exabytes charges S$50/mo on top of a plan for its management add-on, and Network Solutions sells its VPS range as self-managed only. If you cannot comfortably administer a Linux server, add a management fee to your budget before comparing prices, because a $5 server plus $35 of your own time is not a $5 server.

👉 [Start with the Arcturus plan and keep your own backups](https://justhost.asia/en/services/vps/tariffs/arcturus?ref=196392)

## Which tier fits which job

**A single low-traffic site, a proxy, a VPN endpoint, a monitoring node.** The $1.99 promo or New Star at $3.05. The promo's 512 MB of RAM rules out a control panel plus a database, but it handles nginx and a static site without complaint. The 10 Mbps port is the limit worth noting.

**A small database plus an application.** Arcturus at $5.53. Two gigabytes is the realistic floor for MySQL or Postgres alongside a web app; below that you will spend your evenings tuning the buffer pool.

**Containers, CI runners, anything that compiles.** Vega at $10.75, or Capella at $14.64 if 120 GB of images and build caches is closer to reality. Container image pulls and dependency installs are exactly the random-read workload NVMe helps with, and both plans give you enough disk that you are not pruning images weekly.

**Serving media or large downloads.** Capella's 750 Mbps port. Storage speed is irrelevant here; the port and the transfer allowance are the whole game.

**A control panel and multiple client sites.** Bright Star at $7.84 gives you four cores for the price of two, but only 30 GB of disk. If your clients' sites plus mail plus backups exceed that, Vega's 80 GB is the better trade even with fewer cores.

## FAQ

**Is an NVMe VPS noticeably faster than a SATA SSD VPS?**
For random I/O and storage latency, yes. For sequential throughput on a small plan, the network port will bottleneck you first. There is no universal multiplier, and on this provider the price difference is $0.26 to $1.76/mo, so the decision costs you almost nothing either way.

**Can the $1.99 plan run a database?**
Not a comfortable one. 5 GB of disk and 512 MB of RAM fit SQLite or a heavily tuned tiny instance, not MySQL with a control panel on top. Start at Arcturus for anything that stores user data.

**Why does the price say "from $3.05 when you pay for 12 months"?**
That is the list price of $3.81 with a 20% annual discount applied. Paying monthly costs the list price, and New Star, Double Star and Bright Star require an order of at least three months.

**What does "unmetered port, fair-share" mean in practice?**
There is no monthly traffic counter. Your ceiling is the port speed, shared with other instances on the same host, so a 100 Mbps port can move roughly 31 TB in a month if nothing else is competing for it.

**Are backups included?**
They are not listed as part of any plan, so assume they are not and set up your own before you put anything important on the server.

## Before you order

Two things to confirm on the order page, because neither is visible in the headline rate: the billing term you are actually signing up for and what the renewal price will be after the first term, and whether any backup or snapshot service is attached to the plan you picked. A 20% annual discount is worth having if you intend to keep the server; it is a waste if you are testing for a month.

Match the tier to the job rather than to the price list. Arcturus at $5.53 covers a database-backed site for most people, Vega at $10.75 covers containers and builds, and the $1.99 promo is a genuine option for a proxy or a static page as long as you accept 512 MB of RAM and a 10 Mbps port.

👉 [View JustHost.asia's current NVMe VPS plans and prices](https://justhost.asia/?ref=196392)
