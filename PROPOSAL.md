# Proposal

*A potential stack for angx-bridge.*

---

angx-bridge runs on the same device as an ANGX client — a steward's
laptop or a base's persistent device. It does not replace Hyperswarm.
It stands in for it only when the internet is not there.

---

**1. Primary path** — Hyperswarm. When internet is present, Hyperswarm
handles peer discovery and feed replication directly. angx-bridge is
idle. ANGX behaves exactly as specified, with no bridge in the loop.

**2. Fallback path** — Reticulum. Reticulum handles the hard problem
— multi-hop routing, addressing, and fragmentation over unreliable
radio — that Hypercore has no native mechanism for. When internet is
absent, angx-bridge carries feed updates over whatever medium
Reticulum has available — LoRa, packet radio, satellite — hop by hop.
Devices relaying the message in between need only plain Reticulum;
they route encrypted packets without any ANGX or angx-bridge
component installed. The message is decoded and applied only where
both angx-client and angx-bridge are running together, on a device
that currently has internet access — that pairing is what recognizes
a Reticulum-carried message as an ANGX feed update and injects it
into the Hypercore network. There is no designated destination: the
first such device the mesh reaches, with internet available at that
moment, is the one that catches it. When internet returns to the
originating device, Hyperswarm resumes there and angx-bridge steps
aside again.

**3. Identity** — angx-bridge introduces no new seed of its own. On
whatever device it runs, it derives one additional child key — the
Reticulum destination — from that device's existing ANGX seed, the
same one that already produces the ANGX feed identity on that device.
The two keys are siblings, backed up together: the existing recovery
phrase for that device restores both on a fresh install. A steward's
device and a base's device each hold their own independent seed and
backup — angx-bridge never shares or merges identity across them.
Losing a device's phrase loses both of that device's keys together;
it has no bearing on any other device's identity.

**4. Notification** — LXMF, Reticulum's native store-and-forward
messaging, carries any message a local client wants delivered over the
same offline transport as feed updates — not just from angx-bridge,
from anything running on the device. Sideband, an open-source
Reticulum client, is where they arrive. angx-bridge does not generate
notifications; it makes the channel available.

---

Every component is open source, self-hostable, and replaceable.
No vendor dependency. The right implementation of any layer may
look different from what is proposed here.

---

*ANGX*
