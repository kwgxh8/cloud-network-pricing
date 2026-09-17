# cloud network management: what it actually involves, the tools and features that matter, and how to run your own virtual cloud network with real pricing

People search "cloud network management" for a few different reasons, and it's worth separating them before anything else. Some are looking for software — a dashboard that monitors routers, switches, and firewalls from the cloud (Auvik, SolarWinds, and ManageEngine all sell into this space). Others are infrastructure people who just moved workloads into a public cloud and now need to run virtual networks: subnets, firewalls, load balancers, IP allocation, traffic visibility. And a third group is pricing out what it costs to build a networked cloud environment in the first place.

This article covers all three angles, then gets concrete: what a cloud platform's built-in networking layer looks like in daily use, based on Sharktech's OpenStack-based cloud (one of the providers that ships networking features as part of the platform rather than as paid add-ons), what the current plans cost, and where standalone network management tools still make sense.

## What cloud network management actually covers

Strip away the vendor slides and the working definition is simple: it's the practice of monitoring, configuring, and optimizing network resources — through software, without touching physical hardware. What that means in practice depends on what you're managing:

- **Your office or on-prem network from a cloud console.** This is the Auvik/SolarWinds world. The gear sits in a closet or data center; the management layer is hosted and accessed from anywhere. Good for distributed teams and MSPs.
- **Virtual networks inside a cloud platform.** Here the network itself is software-defined. You're creating private subnets, attaching floating IPs, writing firewall rules, and spinning up load balancers — all through a control panel or API. The physical layer (40G/100G links, redundant switching) is someone else's problem, which is the entire appeal.
- **The overlap.** Most real environments end up needing both: a cloud panel for the virtual side, plus monitoring tooling for visibility across everything.

If your search was really about the first category, the short answer is: look for a centralized dashboard, real-time alerts, and automated config backup, and expect to pay per device or per site. The rest of this article focuses on the second category, because that's where the infrastructure decisions — and the monthly bill — actually get made.

## The features that separate a usable cloud network from a minefield

When you evaluate any cloud platform for network management, there's a shortlist of capabilities that determine whether you'll be comfortable or constantly fighting the interface. Here's the list, and how it maps to a real platform — Sharktech's OpenStack-based cloud, in this case:

**Private networks and subnetting.** Every serious cloud lets you isolate backend traffic between VMs so databases and internal services never touch a public interface. Sharktech supports creating private networks and subnets directly in its cloud control panel, which isolates inter-VM traffic from public exposure.

**Virtual routers and floating IPs.** A virtual router gives you NAT and routing between private networks without configuring hardware. Floating IPs let you move a public address between VMs — useful for failover scenarios where you'd otherwise be waiting on DNS propagation.

**Firewall and security groups.** Granular, per-rule traffic control is non-negotiable. Sharktech uses security groups in the OpenStack style: rulesets attached to VMs or subnets, editable in seconds.

**Load balancing.** Distributing traffic across multiple VMs for availability. On Sharktech this is set up through the dashboard, and load balancing is listed as an included service on all cloud plans rather than a metered add-on.

**Traffic monitoring and analytics.** Visibility into usage and performance, so you can troubleshoot and plan capacity. The panel shows per-VM stats and network analytics.

**VPN bridging.** For hybrid setups, native VPN support connects the cloud environment to on-prem infrastructure. Sharktech includes this at no charge.

**IPv6 and API control.** Both are table stakes at this point. The platform exposes OpenStack REST APIs (Neutron for networking), so scripted changes and infrastructure-as-code workflows are possible without clicking through a portal.

One more thing that belongs on the list even though it isn't a feature you configure: **built-in DDoS protection**. Sharktech's network carries 60 Gbps-class DDoS mitigation as a standard layer, which changes the calculus for anything public-facing. On hyperscalers, comparable protection is typically a separate product line with its own pricing.

> The practical test for any platform: can you create a network, attach a firewall, and point a load balancer at two VMs in under ten minutes without opening documentation? If the answer involves a support ticket, keep shopping.

## Where the money goes: data transfer and the exit

Two cost areas surprise people who move to the cloud, and both are network problems, not compute problems.

**Egress fees.** Major providers charge for outbound data transfer, and heavy traffic can quietly dominate a monthly bill. Sharktech's model: incoming traffic is free, each cloud plan includes 20 TB of outgoing transfer, and overage is billed at $0.002 per GB — with no charge for ingress at all. For comparison, that works out to $2 per terabyte beyond the included allowance, which is a fraction of typical hyperscaler egress rates.

**Exit costs.** A subtler issue is lock-in. If your images and snapshots can't leave the platform, your negotiating position can't either. Sharktech's OpenStack foundation means you can download your VM disk images whenever you want — for backup, disaster recovery, or a clean migration to another provider. The vendor explicitly positions this as "no vendor lock-in ever," and it's backed by the ability to upload your own ISOs and qcow2 images too.

**IP addressing.** One public IPv4 address is included per service; additional addresses cost $1.50/month each, up to 16 on most tiers. IPv6 support is standard across deployments.

## Sharktech's cloud plans, in full

Sharktech sells its cloud in two billing flavors — Public Cloud (a base resource commit plus hourly billing for anything above it) and Dedicated Cloud (fixed resources, fixed monthly invoice). The current Public Cloud lineup is four tiers plus a custom option. This is everything shown on the official pricing store right now, nothing omitted:

| Plan | Included resources (base commit) | Maximum cap | Bandwidth (out) | Included network services | Price (USD) | Approx. hourly equivalent | Buy |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **Small** | 4 vCPU, 8 GB RAM, 300 GB SSD | 16 vCPU, 32 GB RAM, 2,400 GB SSD, 1,200 GB NVMe, 4,800 GB HDD | 20 TB (+$0.002/GB) | Security policies, load balancing, network management, routing, Kubernetes | $39.00/mo | ~$0.0609/hr | [Deploy the Small plan](https://bit.ly/SharKTech) |
| **Medium** | 8 vCPU, 16 GB RAM, 800 GB SSD | 32 vCPU, 64 GB RAM, 6,400 GB SSD, 3,200 GB NVMe, 12,800 GB HDD | 20 TB (+$0.002/GB) | Same as above | $79.00/mo | ~$0.1289/hr | [Deploy the Medium plan](https://bit.ly/SharKTech) |
| **Large** | 32 vCPU, 64 GB RAM, 1,500 GB SSD | 128 vCPU, 256 GB RAM, 12,000 GB SSD, 6,000 GB NVMe, 24,000 GB HDD | 20 TB (+$0.002/GB) | Same as above | $249.00/mo | ~$0.3989/hr | [Deploy the Large plan](https://bit.ly/SharKTech) |
| **Enterprise** | 64 vCPU, 128 GB RAM, 5,000 GB SSD | Unlimited | 20 TB (+$0.0015/GB) | Same as above | $499.00/mo | ~$0.7412/hr | [Deploy the Enterprise plan](https://bit.ly/SharKTech) |
| **Custom** | Built to spec | Built to spec | Built to spec | Built to spec | Contact sales | — | [Request a custom quote](https://bit.ly/SharKTech) |

A few details that matter when reading this table:

- **The base price covers the commit; the cap protects you.** On Small, Medium, and Large, the maximum column is a hard ceiling — you can burst above your included resources and pay hourly for the difference, but the bill can't run away past the cap. Enterprise has no cap at all.
- **Overage hourly rates** (Small through Large): CPU $0.0025/hr per core, RAM $0.0035/hr per GB, SSD $0.00006/hr per GB, NVMe $0.00009/hr per GB, HDD $0.00002/hr per GB. Enterprise tiers get slightly discounted overage rates.
- **Resources are a pool, not fixed VMs.** A Small allocation of 4 vCPU / 8 GB / 300 GB can be carved into any combination of virtual machines — one 4-core box, four 1-core boxes, whatever fits. You're managing a small virtual data center, not renting preset instances.
- **Locations:** Los Angeles, Las Vegas, Denver, Chicago, and Amsterdam, selectable at checkout.
- **Billing:** monthly base fee plus hourly overage; no long-term contract required.

There's also a fixed-price variant of the same infrastructure (billed as Dedicated Cloud) for teams that need a flat invoice. Listed configurations from recent plan data include an XS tier at $86.23/mo (8 vCPU, 16 GB RAM, 500 GB SSD) and an S tier at $140.95/mo (16 vCPU, 32 GB RAM, 500 GB SSD). If predictable billing matters more to you than burst flexibility, 👉 [check the current fixed-price options in the cloud store](https://bit.ly/SharKTech).

## A worked example of how overage billing behaves

The formula is straightforward: base monthly fee, plus hourly charges on whatever you consume above the included commit. Here's how it plays out with the current listed rates on a Large plan.

Say you run six VMs around the clock, each with 8 cores, 16 GB RAM, and 150 GB SSD. Together that's 48 cores, 96 GB RAM, and 900 GB of storage. Against the Large commit (32 cores, 64 GB, 1,500 GB SSD), you're over on CPU by 16 cores and RAM by 32 GB, with storage to spare.

$$\text{Monthly total} = 249 + 16 \times 0.0025 \times 720 + 32 \times 0.0035 \times 720$$

$$= 249 + 28.80 + 80.64 = \$358.44$$

The pattern to notice: bursting costs roughly $1.80 per extra core-month and $2.52 per extra GB of RAM-month. If you find yourself running at the cap every month, the next tier up is cheaper than permanent bursting — Medium's included 8 cores cost $79, while 8 burst cores on Small would run about $14 more per month than the same resources inside a Medium commit. The platform's cost calculator (built into the order page) lets you model this before committing, which is the right way to use it.

## What day-to-day management actually looks like

The control panel is where the "management" half of cloud network management happens. On Sharktech's setup, the cloud panel splits cleanly into Compute (VMs, Kubernetes, images, volumes), Networking (networks, VPN, routers, floating IPs), Security (security groups, load balancers), Storage & Backup, and Access (SSH keys).

The workflow for standing up a networked service is roughly: create a private network, boot VMs into it, attach a floating IP to the frontend machine, write security group rules so only the ports you need are open, put a load balancer in front, and bridge to your office over the built-in VPN if internal access is needed. Everything except the physical cabling is done in software, and the weekly-refreshed official OS images mean deployments start from patched systems.

Performance-wise, the numbers worth knowing from the platform's own specifications: the internal cloud network runs on 40G/100G links, per-volume disk I/O is rated around 350 MB/s for SSD and 1.2 GB/s for NVMe tiers, and the uptime guarantee is 99.999%. Third-party benchmarking of a 12 vCPU / 48 GB instance measured roughly 10 Gbps sustained download and over 20 Gbps upload between cloud regions, with 0.17 ms idle latency — for bandwidth-heavy workloads like streaming or file hosting, that's the headroom that matters.

## Do you still need standalone network management tools?

Here's the honest framing. If you run infrastructure inside a single cloud platform, its built-in networking panel covers most of what "cloud network management" promises: configuration, isolation, monitoring, and automation. Buying a separate NMS license to watch a handful of cloud VMs is usually redundant.

Standalone tools earn their keep when:

1. **You have physical network gear** — office switches, campus routers, on-prem firewalls. Cloud panels can't see those; a cloud-hosted NMS like Auvik or SolarWinds can.
2. **You're multi-cloud or hybrid** and need one pane of glass across AWS, Azure, GCP, and your own environment.
3. **You need deep observability** — historical baselines, anomaly detection, topology mapping — beyond what a provider's usage graphs give you.

The pragmatic split many teams land on: use the provider's panel and API as the source of truth for cloud network configuration, and layer a monitoring tool on top only when the environment gets heterogeneous. Starting out, that layer is almost always premature.

## Quick answers to the usual questions

**Is support included when something breaks at 2 AM?** Yes — 24/7/365, by phone and ticket, on all plans. Independent review testing measured a ticket response in under 40 minutes during off-peak hours. Advanced tuning questions (kernel-level network optimization, for example) get pointed in the right direction but may assume some sysadmin knowledge on your side.

**Is there a free trial or money-back guarantee?** No free trial, and payments are generally non-refundable per third-party review of the terms — the exception being billing disputes raised within 30 days that Sharktech agrees with, which result in account credit. The hourly billing model is the practical workaround: you can run a test VM for a few cents before committing to anything.

**How much cheaper is this than AWS/Azure/GCP?** Sharktech claims 50–80% savings against hyperscalers on equivalent workloads and guarantees at least 40%. The structural reasons are open-source software (no licensing pass-through), transparent hourly rates, and free ingress.

**Can I run Kubernetes?** Yes, cluster creation is supported through the panel, and Kubernetes is listed as an included service on all four tiers.

**Payment methods?** Credit cards, PayPal, wire transfer, Western Union, Alipay, and Bitcoin.

## Bottom line

Cloud network management is less about buying a magic dashboard and more about deciding where your network lives and who's responsible for the layers underneath. If your workloads are cloud-native, a platform with a complete built-in networking stack — private networks, routers, security groups, load balancers, VPN, monitoring, and APIs — gets you most of the way there, and Sharktech's OpenStack-based cloud is priced aggressively for exactly that use case, starting at $39/month with no egress charges on inbound traffic and no lock-in on your images. If your network includes physical gear or multiple clouds, add a dedicated monitoring tool on top rather than expecting either side to do both jobs.

Either way, model your expected usage before you pick a tier — the included calculator exists for precisely that. When you're ready, 👉 [explore the current plans and deploy from the cloud store](https://bit.ly/SharKTech), or if you'd rather talk through the architecture first, 👉 [book a free cloud hosting consultation with their team](https://bit.ly/SharKTech).
