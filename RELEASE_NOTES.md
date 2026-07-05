# Arista VeloCloud — SD-WAN Topology Builder
## Release Notes — v1.0

A single-page, zero-dependency web app for drawing SD-WAN topologies. Everything runs in the browser (one `index.html`), auto-saves locally, and deploys to GitHub Pages.

**Live:** https://ameyaarista.github.io/arista_sdwan_topology_builder/
**Repo:** https://github.com/ameyaarista/arista_sdwan_topology_builder

---

## Highlights

- 20+ SD-WAN, network, cloud, and SASE/SSE device types with real product icons
- Smart connections that auto-style themselves (SD-WAN, IPsec, Interconnect, plain)
- Layered ("tiered") auto-layout plus one-click Auto-arrange
- 7 starter templates
- Full editing: drag, resize, recolor, inline-rename, align & distribute
- Group/region containers, text annotations, freehand pen
- PNG / SVG export, browser auto-save, undo/redo
- Live topology validation and a curated Arista/VeloCloud resource library

---

## Device library

Organized into categories in the **Add Device** palette:

- **SD-WAN Devices** — Spoke, Hub, Cluster, AWS Hub, Azure Hub, GCP Hub, Virtual WAN
- **Network Devices** — Router, Switch, Firewall, 5G, Satellite
- **Management** — VCO (Orchestrator), VCG (Gateway)
- **Clouds** — Internet, MPLS
- **SASE / SSE** — Zscaler, Palo Alto Prisma, Netskope

Each device drops onto the canvas where you're looking, with an auto-generated name.

## Connections

- Draw connections from a device's **Suggested connections** panel, which only offers valid targets.
- **Automatic link styling by endpoint type:**
  - **Interconnect** (purple) — core ↔ core (hub/cluster)
  - **IPsec** (orange dashed) — gateway ↔ SSE/firewall, firewall ↔ spoke/hub/cluster/gateway, and spoke/hub/cluster ↔ SSE
  - **Plain, unlabeled** — SSE ↔ Internet, and any link touching a router/switch
  - **SD-WAN** — default overlay for everything else
- **Connection rules** — Virtual WAN connects only to an Azure Hub; Internet/MPLS/router/switch/5G/satellite connect to anything; gateways connect to any node.
- Transport tags rotate to run **along** the connection line and stay upright.
- **Manual connectors** — solid and dotted line tools (bottom toolbar) to link any two nodes.
- **Per-connection color** and **custom labels** (edit inline by double-clicking a line).
- Select a connection to delete it, recolor it, or relabel it.

## Templates

Seven ready-made topologies in the **Templates** menu:

- Hub & Spoke
- Full Mesh (2×2 layout)
- Multi-Region (default landing view)
- 5-Site (2 hubs, 3 spokes)
- 3-Site (1 hub, 2 spokes)
- NSDvEdge
- NSDvGateway

## Layout & arrangement

- **Tiered auto-layout** stacks nodes into meaningful layers (bottom → top): routers/switches, spokes/firewalls, clouds (Internet/MPLS), hubs/clusters, VWAN, SSE, VCO — with barycenter ordering so linked nodes line up vertically. Empty tiers are compacted so nothing floats.
- **Auto-arrange** button re-runs the layout and fits to screen.
- **Align & distribute** — select multiple nodes to align left/center/right, top/middle/bottom, or distribute evenly.
- **Snap-to-grid** toggle and **live alignment guides** while dragging.
- Multiple subnets on a device lay out in a neat side-by-side row.
- **Fit / 1:1 / zoom** controls; pan by scrollbars, two-finger scroll, or Space/middle-mouse drag.

## Editing & productivity

- **Group-select** (rubber-band marquee + Shift-click) and move groups together.
- **Move, resize** (corner handle), and **recolor** nodes (SD-WAN devices, subnets and their connectors, groups — green/blue/gray).
- **Inline editing everywhere** — double-click or the ✎ badge to rename devices, gateways, subnets (CIDR), text, groups, and connections. No popups.
- **Delete** via the × badge or Delete/Backspace.
- **Undo / redo** (buttons + Ctrl/Cmd+Z), and **auto-save** to the browser so a refresh keeps your work.

## Annotation

- **Group / region containers** — labeled boxes drawn behind nodes; grab by header/border, resize, recolor, rename.
- **Text boxes** — click to place, type inline.
- **Freehand pen** in multiple colors with a clear-drawing option.

## Validation

Live **Topology checks** panel flags:
- Orphan nodes (no connections)
- Duplicate device names
- Duplicate / overlapping CIDRs (subnets and clouds)

## Export & persistence

- **Export as PNG or SVG** — one-click image of the diagram, tightly cropped with a white background.
- **Auto-save** to browser localStorage; **Reset** and **Clear canvas** to start over.

## Resources

- **VeloCloud resources** dropdown with the Arista Knowledge Base, VCO orchestrator logins, the SD-WAN data sheet, and the full set of admin/design/deployment/API guides and release notes.

## Deployment

- GitHub Actions workflow publishes the app to GitHub Pages on every push to `main`.

---

## Notable fixes

- Fixed a malformed-SVG bug (unclosed `<g>` from the subnet connector) that could hide device icons on templates with subnets.
- Fixed runaway/asymmetric dragging by using stable screen-space deltas and a non-shifting "world" viewBox with scroll compensation.
- Fixed horizontal scrolling and made the canvas scrollbar reliably visible.
- Mutually-exclusive header dropdowns (only one opens at a time).
