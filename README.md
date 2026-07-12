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
available — hop by hop, to the nearest internet-connected device. That
device injects the update into the Hypercore network. When internet
returns, Hyperswarm resumes. The bridge steps aside.

It does not change what is recorded. It does not decide what
propagates. It moves the same signed feed by a different route when
the primary one is down.

---

## What it does

Two transports, one identity. One master seed derives two child keys
— one for the ANGX feed identity, one for the Reticulum destination.
Twenty-four words on paper recovers both on a fresh device.

When internet is present, Hyperswarm handles discovery and
replication directly. When it is absent, angx-bridge carries the same
feed updates over Reticulum instead, hop by hop, until they reach a
device that can inject them back into the Hypercore network. Neither
transport knows about the other. The bridge is what lets a steward,
a base, or a partner chain keep moving without caring which one is
active.

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
