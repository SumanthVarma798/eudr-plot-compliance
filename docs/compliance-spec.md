# EUDR compliance spec — regulation → data requirements

> Working spec for `eudr-plot-compliance`. Source of truth: Regulation (EU) 2023/1115
> ([EUR-Lex](https://eur-lex.europa.eu/eli/reg/2023/1115/oj)). Every claim below is traceable
> to an article; where this doc and the regulation disagree, the regulation wins.
> Drafted 2026-07-08 (E1.1).

## 1. Core obligation — Article 3

A relevant product may be placed on (or exported from) the EU market **only if all three** hold:

1. **Deforestation-free** (Art. 2(13)), and
2. **Produced in accordance with the relevant legislation of the country of production**
   (Art. 2(40): land-use rights, environmental law, labour law, tax/anti-corruption, FPIC where applicable), and
3. **Covered by a due diligence statement (DDS)** filed in the EU Information System.

Prong 2 is widely under-served by satellite-only competitors — legality evidence
(pattas / land records, plantation licences) is a data-collection problem, which is our lane.

## 2. Scope — commodities (Annex I)

In-scope commodities: cattle, cocoa, **coffee**, oil palm, **rubber**, soya, **wood** —
plus Annex I derived products, matched by HS code.

Product focus for Indian exporters:

| Commodity | Key HS codes | Geography |
|---|---|---|
| Coffee | 0901 | Coorg / Chikkamagaluru (Karnataka) |
| Natural rubber | 4001, 4005–4008, 4011–4013 (incl. tyres) | Kerala; tyre majors as aggregators |
| Wood | 44xx, 94xx (furniture), 47/48 (pulp/paper) | secondary focus |

A product is out of scope if its HS code is not in Annex I, even if it contains an
in-scope commodity in trace amounts.

## 3. Definitions with teeth — Article 2

- **Cutoff date: 31 December 2020.** Land deforested on or before this date is permanently
  clean under EUDR; land converted after is permanently dirty for in-scope production.
- **Deforestation** = conversion of forest **to agricultural use**, human-induced or not.
  It is a *land-use conversion* test, not a tree-felling test: forest cleared for roads or
  buildings is not EUDR-deforestation.
- **Forest degradation** = structural conversion of primary or naturally-regenerating forest
  into plantation forest (or other wooded land). **Applies to wood products only.**
  Coffee and rubber are judged on deforestation alone.
- **Forest** (FAO definition): >0.5 ha, trees >5 m, canopy cover >10%, not predominantly
  agricultural/urban use. ⚠️ **Shade-grown Coorg coffee can satisfy this definition on
  satellite baselines** → false-positive handling is a core product feature (see E1.2,
  multi-baseline agreement).

## 4. Geolocation — Article 9 (our data schema)

- Every plot of production: latitude/longitude to **at least 6 decimal digits** (~11 cm).
- Plots **> 4 ha: polygon mandatory**. Plots **≤ 4 ha: a single point is legally sufficient**
  (no lower bound).
- Product standard ≠ legal minimum: typical Indian smallholder plots (1–3 ha) only *require*
  a point, but a point cannot be credibly baseline-checked. **Verified walked polygons are
  the moat dataset** (→ E3 field-capture PWA).

## 5. DDS + TRACES — who files what

- The **operator** (first placer on the EU market — i.e. the EU importer) files the DDS in the
  EU Information System (TRACES); it returns a **reference number** that must accompany the
  customs declaration. Large downstream **traders** carry operator-like duties.
- Non-EU producers/exporters are **not directly regulated** — the compliance burden flows
  upstream *contractually*: no plot data, no purchase order.
- **Product thesis:** our paying customer is the Indian exporter (curer / dealer / tyre-major
  supply chain), who needs **independently verifiable data collection and distribution** to
  keep EU buyers. The importer's legal risk is the exporter's commercial risk.

## 6. Enforcement clock + risk tier

- **2026-12-30** — large operators/traders. **2027-06-30** — micro/small enterprises.
  (Already delayed twice; a further delay is the track's main external risk.)
- Country benchmarking (Art. 29): low / **standard** / high risk. **India = standard risk** →
  no simplified due diligence for our buyers; competent authorities check ≥3% of operators.

## 7. Open questions (feed E1.2 / E1.3)

- [ ] Which 2020 baselines disagree worst on shade coffee and rubber? (E1.2)
- [ ] Exact DDS field list from Annex II → schema for the pilot packet. (E1.3)
- [ ] How do aggregating exporters reference thousands of smallholder plots in one DDS? (E1.3)
- [ ] TraceX teardown: what do they miss for smallholders? (E1.3)
