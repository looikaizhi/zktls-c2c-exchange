<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="../assets/brand/banner-dark.svg">
  <img alt="C2C zkTLS Exchange Protocol: Alipay / Wise → MPC-TLS prover → verifier server → on-chain escrow contract" src="../assets/brand/banner-light.svg" width="760">
</picture>

# Protocol Docs · English Navigation

**A TLSNotary-based zkTLS semi-decentralized C2C fiat ↔ crypto exchange protocol**

[🚀 Quickstart](hands-on/01-quickstart.md) · [🧠 Deep-dive](deep-dive/01-overview.md) · [📚 Source map](reference/code-map.md) · [🌐 中文](../zh/README.md)

</div>

---

> [!NOTE]
> Open-source documentation accompanying a master's thesis. All facts follow the **actual code and source data**; code references are written as `file:line` and are clickable.

## ⏱ In 30 seconds

**The pain point**: in fiat ↔ crypto C2C exchange, the off-chain payment fact (an Alipay/Wise transfer) **cannot be directly verified by an on-chain contract**, so it can only rely on centralized-platform custody + manual arbitration.

**The solution**: off-chain, **MPC-TLS (TLSNotary)** turns the payment fact into a cryptographic proof; after the verifier server signs it, it is **verified directly inside the on-chain contract**, with asset custody and order state executed deterministically on-chain. Two innovations: ① an **order-binding hash** that cryptographically binds the off-chain proof to the on-chain order (preventing cross-order reuse/tampering); ② a **semi-decentralized dual-domain architecture** (decentralized on-chain execution + constrained off-chain notarization).

---

## 🎯 The gap it fills: three properties at once

This scheme is the only one of the mainstream routes that **achieves all three properties while supporting fiat exchange** (thesis ch2 comparison):

| Property | Centralized exchange | P2P OTC | On-chain DEX+oracle | **This work** |
|---|:---:|:---:|:---:|:---:|
| Supports fiat exchange | ✓ | ✓ | ✗ | **✓** |
| Trustless asset custody | ✗ | ✗ | ✓ | **✓** |
| Cryptographically verifiable payment proof | ✗ | ✗ | N/A | **✓** |
| On-chain account-identifier privacy | ✗ | ✗ | N/A | **✓** |

> [!NOTE]
> The cost: a weak trust in the verifier server + limited single-point-of-failure resistance under the current single node — the engineering trade-off of semi-decentralization.

---

## 🧭 Choose your path

<table>
  <tr>
    <th width="33%">🚀 Hands-on<br><sub>want to run it</sub></th>
    <th width="34%">🧠 Deep dive<br><sub>want to understand it</sub></th>
    <th width="33%">📚 Reference<br><sub>look things up</sub></th>
  </tr>
  <tr>
    <td valign="top">

1. [Quickstart](hands-on/01-quickstart.md)<br><sub>minimal local loop, zero real accounts</sub>
2. [Demo walkthrough](hands-on/02-demo-walkthrough.md)<br><sub>five steps of a real exchange</sub>
3. [Troubleshooting](hands-on/03-troubleshooting.md)<br><sub>error reference + FAQ</sub>

</td>
    <td valign="top">

1. [Overview](deep-dive/01-overview.md) ⭐<br><sub>protocol panorama & reading map</sub>
2. [zkTLS & TLSNotary](deep-dive/02-zktls-tlsnotary.md)<br><sub>the cryptographic foundation</sub>
3. [Threat model](deep-dive/03-threat-model.md)<br><sub>why it is designed this way (T1–T5)</sub>
4. [Protocol design](deep-dive/04-protocol-design.md) ⭐<br><sub>system design & two innovations</sub>
5. [Security analysis](deep-dive/05-security-analysis.md)<br><sub>the S1–S5 security argument</sub>
6. [Evaluation](deep-dive/06-evaluation.md)<br><sub>measured Gas / latency data</sub>

</td>
    <td valign="top">

- [Source map](reference/code-map.md) ⭐<br><sub>thesis concept ↔ source location</sub>
- [Contracts](reference/contracts.md)<br><sub>interfaces / events / permissions</sub>
- [Verifier & plugins](reference/verifier-plugin.md)<br><sub>extensibility, new platforms</sub>
- [Glossary](reference/glossary.md)<br><sub>term lookup</sub>
- [Thesis info](thesis.md) · [Attribution](ATTRIBUTION.md)

</td>
  </tr>
</table>

---

## 📊 Key numbers

<table>
  <tr>
    <td align="center" width="25%"><h3>≈ &#36;0.13</h3><sub>on-chain cost per exchange<br>Arbitrum One, mean tier</sub></td>
    <td align="center" width="25%"><h3>5.94 s</h3><sub>Alipay end-to-end (ideal)<br>broadband 17.44 s</sub></td>
    <td align="center" width="25%"><h3>9.74 s</h3><sub>Wise end-to-end (ideal)<br>broadband 24.02 s</sub></td>
    <td align="center" width="25%"><h3>336 / 0</h3><sub>contract tests pass / fail<br>live run</sub></td>
  </tr>
</table>

> [!IMPORTANT]
> For the recomputation process, see [deep-dive/06-evaluation.md](deep-dive/06-evaluation.md).

---

<details>
<summary>📑 <b>Thesis chapter ↔ document map</b> (click to expand)</summary>

| Document | Main thesis source |
|---|---|
| [deep-dive/01-overview](deep-dive/01-overview.md) | abstract, ch1.3, ch4.1 |
| [deep-dive/02-zktls-tlsnotary](deep-dive/02-zktls-tlsnotary.md) | ch2.2–2.4 |
| [deep-dive/03-threat-model](deep-dive/03-threat-model.md) | ch3.1, ch3.5, ch3.6 |
| [deep-dive/04-protocol-design](deep-dive/04-protocol-design.md) | ch4.1–4.6 |
| [deep-dive/05-security-analysis](deep-dive/05-security-analysis.md) | ch4.7, ch4.8 |
| [deep-dive/06-evaluation](deep-dive/06-evaluation.md) | ch6 + `data_analysis/` |
| [reference/contracts](reference/contracts.md) | ch4.2, `packages/contracts` |
| [reference/verifier-plugin](reference/verifier-plugin.md) | ch4.3, ch4.4, `verifier`+`plugin-sdk` |
| [reference/code-map](reference/code-map.md) | ch4, ch5, the whole monorepo |
| [hands-on/*](hands-on/01-quickstart.md) | ch5, README, demo/keeper |

</details>
