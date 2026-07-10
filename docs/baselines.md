# Forest-baseline observations

> Working notes for issue #3. Conclusions come from direct inspection of the same randomly selected demonstration polygon in Kodagu. The polygon is not a verified farm or production boundary. These datasets support risk assessment; none is legally authoritative by itself.

## Comparison table

| Dataset | Version inspected | What it represents | Access method | Direct plot observation | Interpretation status |
|---|---|---|---|---|---|
| JRC Global Forest Cover 2020 | v3 | JRC 10 m forest-reference map representing forest cover at 31 December 2020 | QGIS WMS: `https://ies-ows.jrc.ec.europa.eu/iforce/gfc2020/wms.py?`, layer `gfc2020_v3`; accessed 2026-07-09 | The demonstration area was not classified uniformly: mapped forest appeared in some parts of the polygon and not in others. | Screenshot reviewed 2026-07-10. The patchiness could reflect real land-cover variation, classification error, boundary choice, or some combination; this view alone cannot distinguish them. |
| Hansen Global Forest Change | 2025 update (v1.13) | Landsat-derived percent tree cover for 2000 plus annual stand-replacement tree-cover loss through 2025 | GLAD Global Forest Change Earth Engine app; accessed 2026-07-10 | Most visible pixels around the demonstration location fall in the 75–100% tree-cover-in-2000 class. Little mapped loss is visually apparent across 2001–2025. | The view indicates high historical tree cover and low visible loss, but it does not measure the polygon, prove current forest cover, isolate post-2020 loss quantitatively, or establish conversion to agriculture. |
| JRC Tropical Moist Forest | 2025 layers in Whisp | Undisturbed tropical moist forest plus annual degradation and deforestation layers | Whisp polygon analysis; accessed 2026-07-10 | 159.82 ha (17.89%) mapped as undisturbed TMF; after 2020, 9.66 ha degradation and 4.37 ha deforestation were reported. | Much lower 2020 forest extent than Hansen-derived tree cover. TMF disturbance is still not proof of EUDR forest-to-agriculture conversion. |
| Whisp multi-layer analysis | App v2.1.0 / library v3.0.0a14 | Convergence-of-evidence polygon statistics and screening risk | Anonymous GeoJSON upload; accessed 2026-07-10 | 893.57 ha polygon; perennial-crop risk `Low`, annual-crop risk `More info needed`, timber risk `Low`. | Useful screening output, not a compliance decision. The summary needs inspection because underlying forest layers disagree and some post-2020 disturbance layers are non-zero. |

## Plot used for all comparisons

- File: `plots/coorg-coffee-01.geojson`
- Geometry: one valid, closed WGS84 polygon with 17 unique boundary vertices and no holes.
- Centroid: approximately 75.770299° E, 12.440870° N, plausibly within Kodagu.
- Computed area: approximately 893.0 ha.
- Selection note: this boundary was drawn randomly for tool-learning. It is a demonstration area, not a verified farm, estate, cadastral parcel, or production plot.
- Scope note: its large area is acceptable for comparing tool behavior, but it cannot be used as evidence about a real producer or supply chain.
- Precision note: most ordinates serialize to six decimal places, while two longitude values serialize to five. A JSON serializer may have removed trailing zeroes, so this does not prove lower capture accuracy; the source/export precision still needs confirmation.

## JRC GFC2020 v3 observation notes

### What the data shows

Within the drawn boundary, the visible `gfc2020_v3` classification was spatially discontinuous: broad areas were covered by the green forest mask while other areas, including some that appear tree-covered in the satellite image, were not.

### What we can infer

The demonstration polygon should not be summarized as simply “forest” or “non-forest” from this visual inspection. Any polygon-level conclusion needs either a measured overlap statistic or careful qualification that the classification is mixed. Visual similarity to tree cover is not ground truth and does not prove that an unmasked area is a classification error.

### What remains unknown

- The percentage of the polygon classified as forest.
- Whether the mapped pattern represents real land-cover variation, shade-coffee classification behavior, boundary error, or dataset error.
- How the same polygon compares with Hansen GFC, JRC TMF, and Whisp.

### What the law requires

GFC2020 v3 has no legal value by itself. It can support deforestation-risk assessment, but it does not determine EUDR compliance or replace due diligence.

## Hansen Global Forest Change observation notes

### What the data shows

At the demonstration location, most visible pixels are colored in Hansen's 75–100% tree-cover-in-2000 class. Few loss-year pixels are visually apparent in the 2001–2025 view.

### What we can infer

The surrounding landscape had high Landsat-estimated tree cover in 2000 and appears to have relatively little stand-replacement tree-cover loss compared with the amount of tree cover shown.

### What remains unknown

- The exact tree-cover percentage or loss area inside the GeoJSON polygon, because the GLAD app view does not display the polygon or calculate zonal statistics.
- Whether any sparse loss pixels occurred specifically after 2020.
- Whether any tree-cover loss represents conversion to agriculture, another land use, harvesting, disturbance, or mapping noise.

### What the law requires

Hansen tree-cover loss is not equivalent to EUDR deforestation. EUDR requires forest-to-agricultural-use conversion after the cutoff; a loss pixel alone does not establish that transition.

## Whisp observation notes

Whisp returned polygon-level statistics that the individual viewers did not:

| Whisp field | Area | Share of 893.57 ha |
|---|---:|---:|
| `EUFO_2020` (JRC GFC2020 v3) | 323.19 ha | 36.17% |
| `GFC_TC_2020` (Hansen-derived tree cover) | 772.43 ha | 86.44% |
| `TMF_undist` | 159.82 ha | 17.89% |
| `Coffee_FDaP` | 78.76 ha | 8.81% |
| `TMF_deg_after_2020` | 9.66 ha | 1.08% |
| `TMF_def_after_2020` | 4.37 ha | 0.49% |
| `GFC_loss_after_2020` | 6.01 ha | 0.67% |

The three 2020 forest/tree-cover layers therefore do not agree on extent. Hansen-derived tree cover is the broadest, JRC GFC2020 v3 is intermediate, and undisturbed TMF is the narrowest. This is partly expected because they measure different concepts; disagreement is not automatically an error.

Whisp's indicators reported tree cover `yes`, commodity overlap `no`, disturbance before 2020 `yes`, and disturbance after 2020 `no`. It classified perennial-crop risk as `Low`, annual-crop risk as `More info needed`, and timber risk as `Low`.

## Step 5 verdict

### Do the baselines agree?

They agree that the demonstration landscape is substantially tree-covered, but they disagree sharply on how much qualifies under each 2020 layer: approximately 86% Hansen-derived tree cover, 36% JRC GFC2020 v3 forest, and 18% undisturbed TMF. Small post-2020 disturbance areas are present in several raw layers.

### What should an EU importer conclude?

The evidence is not sufficient for an EUDR compliance conclusion. A prudent importer should treat it as a screening result requiring clarification, not as a clean/dirty verdict. The polygon is a random demonstration area rather than a verified farm, and the analysis does not prove land use, agricultural conversion, production linkage, or legality.

### What did Whisp leave unexplained?

- Why the perennial-crop result is `Low` despite large differences between forest layers and non-zero post-2020 disturbance areas.
- Which thresholds turned the raw disturbance areas into the aggregate `disturbance after 2020 = no` indicator.
- Whether any detected loss or disturbance represents conversion to agriculture.
- Why only 78.76 ha overlaps the coffee model and whether that model is reliable for shade coffee in Kodagu.

Whisp is valuable because it exposes many layers quickly, but its single risk label can hide consequential disagreement. A defensible product should retain layer-level evidence, explain thresholds, flag conflicts, and route ambiguous plots to review rather than presenting an unexplained verdict.

## Evidence status

- `evidence/issue-003/step-01-coorg-plot-satellite.png`: reviewed and usable for Step 1; shows the demonstration polygon over Google Satellite with the polygon and basemap layer names visible.
- `evidence/issue-003/step-02-jrc-gfc2020-v3-qgis.png`: preserved; shows the JRC mask and layer name, but the polygon layer is unchecked.
- `evidence/issue-003/step-02-jrc-gfc2020-v3-with-plot.png`: reviewed and usable for Step 2; shows satellite, `gfc2020_v3`, the demonstration-polygon boundary, and the visible layer names together.
- `evidence/issue-003/step-03-hansen-gfc.png`: reviewed and usable for Step 3 as a location-level visual inspection; the polygon itself is not rendered by the GLAD app.
- `evidence/issue-003/step-04-whisp-results.png`: Whisp polygon/result overview.
- `evidence/issue-003/step-04-whisp-risk-results.png`: Whisp risk outcomes showing perennial `Low`, annual `More info needed`, and timber `Low`.
- Original GeoJSON copied into the repository without altering its coordinates.
