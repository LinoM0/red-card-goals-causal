------------------------------------------------------------------------

## Summary

-   **Goal of the challenge** – *Determine whether issuing a red card ultimately leads to **more total goals** in a football match.*

-   **Data** – 20 000 football matches (10 European leagues, 5 seasons) (games.csv) + minute-stamped goals & red-cards (events.csv).

-   **Two analytical lenses**

    1.  **Across-matches:** compare matches with vs. without a red.

        -   OLS (no controls) → +0.05 extra goals (p \> .05).
        -   OLS (with controls) → +0.07 extra goals (p \< .05).
        -   Poisson GLM (with controls) → +2.6 % goals (p \< .05).
        -   Limitation: ignores timing; prone to omitted-variable bias.

    2.  **Within-match:** use only games with a single red card.

        -   Paired *pre/post* rate diff ⇒ +0.013 g · min⁻¹ (p \< .05).
        -   **Poisson GLM + log-exposure offset** ⇒ per-minute goal rate **↑ 55 %** after a red card\
            (exp(γ̂₁) ≈ 1.55, ϕ ≈ 1.05).

-   **Robustness** – Effect survives league, team, season/trend controls.

-   **Core finding**

    > **Once a match goes to 10 v 11, the combined scoring rate of both teams rises by ≈ 55 %.**

-   **Caveats** – Unobserved match-intensity & fatigue may confound across-match results; even in within-match comparisons omitted variables may still exist.

### Directions for Future Work

-   **Heterogeneity checks**

    -   Separate uplifts by *league*, *home-vs-away offender*, and *card-minute buckets* (0–15, 16–30 …).

-   **Richer causal frameworks**

    -   **Propensity-score matching** at match level using league, season, team attack/defence ratings.
    -   Minute-resolved **Difference-in-Differences**: untreated minutes from no-card matches as control.
    -   **Event-time hazard models** (discrete-time logit / Cox PH) with time-varying “RedOnPitch” covariate.
    -   **Synthetic control** for repeated fixtures (same home/away pair across seasons).

-   **Model extensions**

    -   Allow for multiple cards: indicator for ≥ 2 reds; interaction with first-card timing.
    -   Hierarchical (mixed-effects) Poisson to share strength across teams/leagues.

------------------------------------------------------------------------


