# vps plans: How to Pick the Right BandwagonHost VPS for Your Workload Without Overpaying

When you start searching for **vps plans**, you're usually trying to answer one of three questions: which spec tier actually fits what I'm running, whether paying annually is worth it, and whether a budget provider can handle a real workload instead of just existing as a placeholder on a comparison site. This walkthrough is built around those questions, using BandwagonHost (also known to its Chinese user base as 搬瓦工) as the concrete example — not because it's the only option, but because its plan structure is unusually transparent about what you get at each tier and where the price jumps happen.

## What You're Actually Buying With a Self-Managed VPS

Before comparing numbers, it helps to be clear about the category. BandwagonHost sells **self-managed KVM VPS** instances. That label matters for two reasons.

KVM means full hardware virtualization — you get your own kernel, your own init system, tun/tap for VPNs, and you can install basically any Linux distribution you want. The control panel is KiwiVM, which BandwagonHost built in-house. It handles the things you'd expect: start/stop, OS reload, snapshots, rDNS (PTR) management, datacenter migration, and an emergency console. You also get root access and a routed IPv6 /64 subnet on every plan.

Self-managed is the part people underestimate. BandwagonHost does not configure your web server, harden your SSH setup, debug your app, or install your SSL certificates. If you want a one-click WordPress installer or a managed support ticket that fixes your nginx config at 3 a.m., this is the wrong product. The trade-off is price — self-management is the main reason the entry tier lands at $49.99/year instead of $20/month.

If you're comfortable at a Linux shell, or you're willing to learn, that trade-off is fine. If the words "I just want it to work" describe your situation, you're better off with a managed host and should stop reading here.

## The Standard KVM PROMO Lineup: Where the Value Actually Lives

BandwagonHost's main product page lists six standard KVM PROMO plans. These are the ones most buyers should be looking at first — they're the cheapest per spec, they support multiple datacenter locations, and they include free migration between those locations if you pick wrong the first time.

Here's the full current lineup, pulled from the official cart page:

| Plan | RAM | vCPU | SSD (RAID-10) | Monthly Transfer | Link Speed | Cheapest Billing Cycle | Annual Price (when available) | Order Link |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 20G KVM PROMO | 1 GB | 2× Intel Xeon | 20 GB | 1 TB | 1 Gbps | $49.99/year | $49.99 | [Get the 20G plan](https://bwh81.net/aff.php?aff=77528&pid=44) |
| 40G KVM PROMO | 2 GB | 3× Intel Xeon | 40 GB | 2 TB | 1 Gbps | $52.99/half-year | $99.99 | [Get the 40G plan](https://bwh81.net/aff.php?aff=77528&pid=45) |
| 80G KVM PROMO | 4 GB | 4× Intel Xeon | 80 GB | 3 TB | 1 Gbps | $19.99/month | $199.99 | [Get the 80G plan](https://bwh81.net/aff.php?aff=77528&pid=46) |
| 160G KVM PROMO | 8 GB | 5× Intel Xeon | 160 GB | 4 TB | 1 Gbps | $39.99/month | $399.99 | [Get the 160G plan](https://bwh81.net/aff.php?aff=77528&pid=47) |
| 320G KVM PROMO | 16 GB | 6× Intel Xeon | 320 GB | 5 TB | 1 Gbps | $79.99/month | $799.99 | [Get the 320G plan](https://bwh81.net/aff.php?aff=77528&pid=48) |
| 480G KVM PROMO | 24 GB | 7× Intel Xeon | 480 GB | 6 TB | 1 Gbps | $119.99/month | $1199.99 | [Get the 480G plan](https://bwh81.net/aff.php?aff=77528&pid=49) |

A few things worth noticing before you click anything.

The 20G plan is the only one that's **annual-only** at the entry price. You can't pay monthly on it. That's actually the strongest signal in the lineup: BandwagonHost prices it as a loss-leader-ish annual commitment, and if you're not willing to drop $49.99 upfront, this tier isn't really aimed at you. Worked out monthly, it's about $4.17 — cheaper than almost anything else on the market with these specs, but only because you're paying for a year.

The 40G plan opens up a half-year option at $52.99, and the annual drops to $99.99. That's the point where the per-month math starts to make sense for people who want to test the water without committing a full year.

From the 80G plan upward, you get monthly billing. The 80G at $19.99/month is the first tier where you can genuinely treat the VPS as a throwaway — spin it up for a project, cancel next month, no harm done. The annual price of $199.99 works out to roughly $16.67/month, so committing to a year saves you about 16%.

The CPU allocation is worth a quick note. BandwagonHost's terms of service specify CPU shares rather than dedicated cores: the 20G plan gets 50% of one core, the 40G gets 75% of one core, the 80G gets a full core, and the higher tiers stack partial cores on top. This is normal for budget VPS and isn't hidden, but it does mean a "5× Intel Xeon" label on the 160G plan isn't the same as five dedicated cores — it's a fair share of five cores, with the slice growing as you move up the ladder.

## Which Plan Matches Which Workload

The spec table is only useful if you can map it to what you're actually doing. Here's how the tiers shake out in practice, based on what BandwagonHost itself says the plans are suited for and what the configuration can realistically handle.

**The 20G plan ($49.99/year)** is for a single lightweight service. A personal blog with low traffic, a tiny VPN endpoint for yourself, a monitoring agent, a DNS resolver, a Tor relay, a small git mirror. One gigabyte of RAM is the real ceiling — once you've got a web server, a database, and your application runtime loaded, you don't have much room left for actual work. If you're running WordPress, expect to keep caching aggressive and plugins minimal.

**The 40G plan ($99.99/year or $52.99/half-year)** is where small personal projects start to breathe. Two gigabytes is enough for a small LAMP stack, a low-traffic Nextcloud instance, a Matrix server with a handful of users, or a development sandbox you actually use daily. The extra CPU share also helps when something needs to compile.

**The 80G plan ($19.99/month or $199.99/year)** is the first tier that handles a real small business workload. Four gigabytes runs a moderately busy WordPress site with a cache plugin, a small forum, a lightweight Docker setup with two or three containers, or a staging environment that mirrors production. This is also where you start getting a secondary private network interface, which matters if you want to put two VPS instances on an internal private network.

**The 160G plan ($39.99/month or $399.99/year)** is the sweet spot for a small production site. Eight gigabytes comfortably runs a mid-traffic web app, a Minecraft server with a dozen players, a medium Postgres database, or a CI runner. Five vCPU shares means contention is less of an issue even under bursty load.

**The 320G and 480G plans** are for people who already know they need them. Sixteen to twenty-four gigabytes of RAM and 5–6 TB of transfer push you into territory where you're running multiple production services, a heavier database, a build farm, or a sizable media pipeline. At $799.99 and $1199.99 annually, you're no longer in "cheap VPS" territory — you're comparing against small dedicated servers and cloud instances from Vultr, DigitalOcean, and Hetzner, and the comparison should be done on total cost including bandwidth, not headline RAM.

## When the Standard Plans Aren't Enough: CN2 GIA and E-Commerce Tiers

BandwagonHost's standard KVM PROMO plans route over regular IP transit. For most users in North America and Europe that's fine. But if your audience is in China, or you're connecting from China to a VPS abroad, regular transit gets congested badly during peak hours — packet loss rates can hit 30% or more, which makes web conferencing, gaming, and even basic page loads painful.

That's the problem BandwagonHost's CN2 GIA plans exist to solve. CN2 GIA (Global Internet Access) is China Telecom's premium AS4809 network, and CTGNet (AS23764) is its newer equivalent. BandwagonHost sells these as "SPECIAL" plans in four locations: **Los Angeles (eCommerce SLA tier), Hong Kong, Tokyo, and Osaka**.

The pricing structure is very different from the standard lineup. A SPECIAL 40G KVM PROMO V5 in Singapore or Osaka starts at $49.99/month (not per year) with 500 GB of transfer and a 1.5 Gbps link. The same 40G spec on the standard plan is $99.99/year. The premium routing costs roughly six times more for the entry tier, and the gap widens as you scale up — a Hong Kong 1280G CN2 GIA plan runs $18989.99/year.

The trade-off is real performance for China-bound traffic. BandwagonHost's own explanation is unusually direct: CN2 GIA IP transit can cost up to $120 per megabit, which is why a 1 Gbps commitment on this network can run a $100,000 monthly bill in some markets. They're not marking up arbitrarily; they're passing along a genuinely expensive upstream.

If you don't have users in China, **skip the CN2 GIA plans entirely**. The standard KVM PROMO plans in Los Angeles, New York, Vancouver, Amsterdam, and Fremont are better value for any other audience. If you do have China users, the Los Angeles eCommerce SLA tier is the cheapest entry point — it uses CN2 GIA/CTGNet, CMIN2 (China Mobile), and China Unicom Premium routing, with a 99.99% SLA and AMD EPYC NVMe hardware. Hong Kong and Tokyo have lower latency but cost substantially more.

You can browse the full CN2 GIA lineup through 👉 [the BandwagonHost CN2 GIA plan page](https://bwh81.net/aff.php?aff=77528&gid=1), which lists every SPECIAL plan across all four premium locations.

## Datacenter Choice and Free Migration

One thing BandwagonHost does better than most budget providers is datacenter flexibility. Standard KVM PROMO plans can be deployed in roughly a dozen locations — including Los Angeles (Coresite LA2 / USCA_2 and the DC9 eCommerce facility), Fremont, New York (Coresite NY1), New Jersey, Vancouver, and Amsterdam — and you can migrate a live VPS between any of them from the KiwiVM panel without losing data and without opening a ticket.

That matters more than you'd think. If you pick a location based on a guess about where your users are, and the latency turns out wrong, you're not stuck. The migration is free and the IP address changes, but the disk image, snapshots, and configuration come along.

Recent hardware updates worth knowing about: BandwagonHost has rolled out AMD EPYC servers with NVMe RAID-10 storage in New York, Hong Kong (HK3 and HK8), and Los Angeles DC9. If you're signing up fresh, you'll likely land on the newer hardware. If you're on an older node, migration to a newer datacenter is the way to get there without paying for a new plan.

## Promo Codes: What's Actually Active

BandwagonHost runs promo codes occasionally, and the recurring ones are the only ones worth chasing — a one-time discount on a yearly plan is fine, but a recurring discount applies to every renewal, which compounds over years.

Based on currently visible coupon listings, the codes below have been reported as active across multiple third-party trackers. Treat any specific discount percentage as "best known" rather than guaranteed — BandwagonHost occasionally rotates these, and the only way to confirm a code still works is to apply it in the cart before paying.

- **BWHCGLUKKB** — reported as a recurring 6.78% discount on all VPS plans. This is the most consistently cited code across coupon trackers.
- **ireallyreadtheterms8** — reported as a 5.5% to 7% recurring sitewide discount. The variable range suggests it may apply differently across plan tiers.
- **BWH1ZBPVK** — listed as a sitewide recurring discount, percentage varies by source.

None of these are large discounts. A 6.78% recurring reduction on the $49.99/year 20G plan saves about $3.40 per year. The value scales with plan size — on the $1199.99/year 480G plan, the same code saves roughly $81 annually, which is more meaningful. The point of using a code isn't to transform a plan's value; it's to not leave a small but permanent discount on the table.

To apply a code: add a plan to cart, proceed to checkout, find the "Promotional Code" field, enter the code, and click apply. The discount should reflect in the order total before you pay. If a code comes back invalid, it's been retired — try the next one on the list.

## How the Purchase Actually Works

The buying flow is straightforward but worth knowing in advance if you've never used BandwagonHost.

You pick a plan, pick a billing cycle, pick a datacenter (for plans that support multiple locations), and check out. Operating system selection happens **after** the service is activated, in the KiwiVM panel — you don't choose OS at purchase time. Available templates include AlmaLinux, RockyLinux, CentOS, Debian, Ubuntu, CentOS Stream, and Fedora, with 32-bit and 64-bit versions where applicable. Manual ISO installation is also supported if you want something not on the list.

Setup is instant once payment clears. BandwagonHost accepts the usual payment methods — credit card, PayPal, and (notably for users in regions where card acceptance is spotty) Alipay and UnionPay. The 30-day refund policy applies to first orders, so if the network performance isn't what you expected, you can pull out within the first month and get the service fee back.

The 99.95% uptime guarantee on standard plans (99.99% on the eCommerce SLA tier) is a service-level commitment, not a cash refund schedule — read the terms for the exact credit structure if uptime matters to your decision.

## BandwagonHost vs. the Obvious Alternatives

If you're searching "vps plans" you're almost certainly comparing BandwagonHost against Vultr, DigitalOcean, Linode, or Hetzner. Here's the honest version of that comparison.

**Against Vultr and DigitalOcean:** BandwagonHost's standard plans are cheaper per gigabyte of RAM and per terabyte of transfer, especially at the entry tier. The $49.99/year 20G plan has no real equivalent at Vultr or DO — their cheapest tiers run $5–6/month with similar specs but billed monthly, which works out to $60–72/year. BandwagonHost loses on flexibility (no hourly billing, no API-driven spin-up for ephemeral workloads) and on the breadth of datacenter locations. Vultr and DO win if you need instances you can spin up and destroy by the hour, or if you want a polished control panel and managed databases.

**Against Hetzner:** Hetzner is cheaper than BandwagonHost at the mid and high tiers if your audience is in Europe. Hetzner's CX series offers more RAM per dollar than BandwagonHost's 160G and 320G plans, and the network is excellent for European traffic. BandwagonHost's advantages are the CN2 GIA routing for China traffic (Hetzner has nothing comparable), the wider spread of U.S. datacenters, and the acceptance of payment methods that matter for users outside Europe.

**Against Linode/Akamai:** Similar story to Vultr/DO — BandwagonHost is cheaper for steady-state workloads, Linode is better for ephemeral use and has a more polished managed offering.

The pattern: BandwagonHost wins on price-per-spec for persistent workloads, especially annual commitments, especially if China routing matters. It loses on flexibility, API-driven infrastructure, and managed services. If you're running a single website or a small set of services that stay up all year, BandwagonHost is hard to beat. If you're building infrastructure that scales up and down by the hour, use something else.

## Common Questions Before You Buy

**Can I upgrade between plans later?** BandwagonHost doesn't do in-place plan upgrades the way DigitalOcean does. You can order a larger plan, migrate your data over (or restore a snapshot), and cancel the smaller one. The free datacenter migration tool helps here. It's not seamless, but it's not painful either.

**What happens if I exceed the monthly transfer cap?** BandwagonHost doesn't bill overages on the standard plans — they cap your port speed instead. If you blow through your transfer allowance, your link gets throttled until the next cycle. For the 20G plan with 1 TB of transfer, that's a real consideration if you're serving media. For the 320G and 480G plans with 5–6 TB, you have to be doing something fairly bandwidth-heavy to hit the cap.

**Is the 99.95% uptime realistic?** BandwagonHost has been around since 2012 and owns its hardware and IP space, which is more than can be said for some reseller-style budget hosts. The uptime figure is a commitment, not a measurement — third-party monitoring services generally show BandwagonHost in the 99.9%+ range, with occasional dips during upstream carrier issues. The China-routed plans sometimes see brief congestion-related slowdowns that don't count against the SLA but do affect real-world performance.

**Do I need the CN2 GIA plan if I'm in China but my users aren't?** No. CN2 GIA matters for traffic heading *into* China. If you're in China accessing a VPS abroad, you want CN2 GIA on the VPS side because the route from China to the VPS uses the premium network. If your users are in Europe or North America and you happen to be in China, the standard plans in Los Angeles or Amsterdam are fine — your users never touch the congested China-bound path.

**Can I run a VPN on these plans?** Yes. All BandwagonHost VPS plans include PPP and VPN support (tun/tap) by default, with full root access. This is explicitly listed in the plan features. You can run WireGuard, OpenVPN, or any other VPN stack without needing to request anything special.

**What's the refund policy on annual plans?** The 30-day refund applies to first-time orders. If you buy a year, decide within 30 days it's not for you, you get the annual fee back. After 30 days, you're committed. This is more generous than providers that prorate refunds with penalties, but it does mean the first month is effectively a trial period — use it to test actual network performance from your real user locations.

## A Quick Decision Framework

If you've read this far and still aren't sure which plan to pick, here's the short version.

- **Personal blog, low-traffic site, single lightweight service:** 20G plan, annual, $49.99. Don't overthink it.
- **Small project you actually use, dev environment, small Nextcloud:** 40G plan, $99.99/year.
- **First real production site, small business workload, moderate Docker usage:** 80G plan, $19.99/month or $199.99/year if you're confident you'll keep it.
- **Production site with real traffic, game server, CI runner, medium database:** 160G plan, $39.99/month.
- **Multiple services, heavier database, build farm:** 320G or 480G, and at this point you should also be quoting Hetzner and Vultr bare metal before deciding.
- **Audience in China:** Skip the standard plans and go straight to the CN2 GIA tier, starting with Los Angeles eCommerce SLA if latency isn't critical, or Hong Kong/Tokyo if it is.

The plan that's right for you isn't the one with the most impressive spec sheet — it's the one that matches what you're actually going to run, billed at a cycle that matches how confident you are about staying. BandwagonHost's lineup is built so that the gap between tiers is large enough to make the decision obvious once you know your workload. The mistake to avoid is buying two tiers up "just in case" — the upgrade path through migration is easy enough that starting one tier lower and moving up when you hit a wall is usually cheaper than overprovisioning from day one.

You can see the full current plan list and pricing at 👉 [BandwagonHost's VPS hosting page](https://bwh81.net/aff.php?aff=77528&gid=1), where every standard and premium plan is listed with live availability by datacenter.
