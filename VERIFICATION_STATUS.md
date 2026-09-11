# Stata Verification Status

All ten `.do` files in `stata/` have been run in Stata (18.0 SE or 18.5)
and checked against each file's "EXPECTED OUTPUT" comment block, sourced
from the manuscript's own published results. **All ten are verified —
every result matches its EXPECTED OUTPUT**, with one near-boundary rho
value flagged for a manual look (see `Weighting_Scheme_Sensitivity_Verification.do`
below).

| Script | Status |
|---|---|
| `Correlation_Matrix_Verification.do` | ✅ Verified — all 6 correlations and p-values matched exactly |
| `Meghalaya_Influence_Verification.do` | ✅ Verified — Cook's D and Model II coefficients matched exactly |
| `Migration_Model_Verification.do` | ✅ Verified — all coefficients matched exactly |
| `AgeStructure_Sensitivity_Verification.do` | ✅ Verified — 0 mismatches, footnote 1's claim confirmed |
| `Discriminating_Power_Verification.do` | ✅ Verified — all 5 percentages matched exactly |
| `PCA_and_Cluster_Analysis.do` | ✅ Verified — PCA loadings and clustering matched |
| `Entropy_Weighting_Verification.do` | ✅ Verified — weights and reclassification rate matched exactly |
| `OLS_Primary_Model_Verification.do` | ✅ Verified — after one round-trip: a double-log bug in the first version (`ln_nsdp` came out as 237.47 instead of 19.21) was caught by the author's own test run, fixed, and the corrected version re-run and confirmed (19.214, matching). |
| `Weighting_Scheme_Sensitivity_Verification.do` | ✅ Verified, with one confirmed manuscript error to fix before submission — 0 baseline mismatches; all six schemes' reclassification counts/rates matched exactly, including Scheme D's corrected 7/25.0% (confirming the Manipur tie-break fix). Independently recomputed in Python (scipy, plus a manual average-rank cross-check) directly from the manuscript's own published Table 5 columns: **Scheme D's true rho is 0.859, not the 0.872 printed in Table 7.** Every other scheme matches Table 7 to within 0.001–0.005 (normal rounding); Scheme D is the sole outlier at 0.013, and its correct value (0.859) coincidentally equals Scheme F's — consistent with Table 7's rho field for Scheme D having been left at a stale pre-fix value when the Manipur tie-break correction updated the reclassification count but not the correlation next to it. **Action required: change Table 7's Scheme D rho from 0.872\*\* to 0.859\*\* before submission.** |
| `CBR_Boundary_Reversal_Verification.do` | ✅ Verified — re-run in Stata 18.5 after the Note A11 tie-break fix, and confirmed against EXPECTED OUTPUT: 20 borderline states, 1 tie (Telangana), 0 unresolved ties, 7 changed / 13 unaffected, the same 7 named states (Odisha, Maharashtra, Karnataka, Punjab, West Bengal, Telangana, Tamil Nadu). Telangana's tie now resolves to S3 via the principled Note A11 rule (age 9.23 falls inside S3's own 7–10 band), matching what the corrected logic predicted — this was an earlier version's naive fallback that has now been properly re-verified, not assumed. |

Last updated after the author's full Stata run-through of all ten files,
including the fix-and-reverify cycle on two of them (`OLS_Primary_Model_Verification.do`
and `CBR_Boundary_Reversal_Verification.do`), plus an independent
Python cross-check of `Weighting_Scheme_Sensitivity_Verification.do`'s
Scheme D rho, which confirmed a manuscript error (Table 7 prints 0.872,
the correct value is 0.859) that needs to be corrected before
submission — see that row above for the full detail.
