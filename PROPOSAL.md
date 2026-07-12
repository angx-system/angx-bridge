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
Reticulum has available — LoRa, packet radio, satellite — hop by hop,
to the nearest internet-connected device. That device injects the
update into the Hypercore network on the bridge's behalf. When
internet returns, Hyperswarm resumes and angx-bridge steps aside
again. Neither transport is aware of the other; the bridge is what
decides which one is live.

**3. Identity** — one master seed, two child keys. One key is the
ANGX feed identity, used exactly as the protocol expects. The other
is the Reticulum destination, used only by angx-bridge. Both derive
from the same seed, so a single recovery phrase — twenty-four words on
paper — restores both on a fresh device. Losing the phrase loses both
identities together; there is no recovering one without the other.

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
