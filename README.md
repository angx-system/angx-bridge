# angx-bridge

*Reticulum transport bridge for ANGX.*

---

ANGX runs on Hyperswarm — peer discovery and feed replication over the
internet. Most of the places ANGX is for do not have reliable internet.
A clinic on a bad connection, a base after a storm takes down the
tower, a builder somewhere a cell signal never reached in the first
place. The work and the surplus are still real. The log still needs
to move.

angx-bridge carries ANGX feed updates over Reticulum when the internet
is absent — LoRa, packet radio, satellite, whatever medium is actually
available — hop by hop, until they reach a device running both the
ANGX client and angx-bridge with an internet connection. That device
decodes the update and injects it into the Hypercore network. When
internet returns, Hyperswarm resumes. The bridge steps aside.

It does not change what is recorded. It does not decide what
propagates. It moves the same signed feed by a different route when
the primary one is down.

Like angx-reader's indexer, angx-bridge runs as a silent background
process — no interface of its own, nothing to open. Reader pairs its
background indexer with an optional GUI for viewing matches; bridge
has no equivalent.

---

## What it does

Two transports, one identity. angx-bridge does not generate a new
identity of its own. On whatever device it runs — a steward's laptop
or a base's persistent device — it derives one additional child key,
the Reticulum destination, from that device's existing ANGX seed. The
ANGX feed identity is untouched; the Reticulum key is simply a sibling
of it, backed up together with it, on that same device.

When internet is present, Hyperswarm handles discovery and
replication directly. When it is absent, angx-bridge carries the same
feed updates over Reticulum instead, hop by hop, toward the network.
Devices relaying the message in between need only plain Reticulum —
they route encrypted packets without needing ANGX or angx-bridge
installed at all. angx-bridge is a translator running at the two
endpoints of a route, not something that needs to exist anywhere in
between.

The message is only decoded and applied where both angx-client and
angx-bridge are running together — that pairing is what lets a device
recognize a Reticulum-carried update as an ANGX feed and write it to
Hypercore. Neither side of a route needs to be a specific, named base.
Whichever ANGX-client-and-bridge device the mesh reaches first, with
internet access at that moment, injects the update. From there it
propagates through Hyperswarm and the partner chain as normal.

Because of this, bases operating in regions with unreliable
connectivity — serving stewards who may drop offline often — should
run angx-bridge as a standing service to that region, not only for
their own logging. The base doesn't need to be the origin of a
message to be useful; it only needs to be reachable by mesh and online
when a message arrives. A base already holds the largest local
collection in its region, and running reader on top of that
collection already makes it the primary source of matches for
stewards nearby — running bridge as well extends that same role to
connectivity, not just to knowledge.

---

## What it doesn't do

angx-bridge has no opinion on what is true, what is matched, or what
gets curated into a base. It carries bytes. ANGX decides what those
bytes mean. A reader like angx-reader decides what relates to what.
angx-bridge only makes sure the feed gets there.

---

## Docs

- PROPOSAL.md — a possible stack

**Dependency:** [github.com/angx-system/angeliax](https://github.com/angx-system/angeliax)

---

*ANGX*
