# 🆕 Drugs and Clinical Candidates

The **Drugs and Clinical Candidates** widget on the Target page is based on the **Clinical Target** dataset. Unlike the [Disease page equivalent](../disease-or-phenotype/drugs.md), which fixes a disease and lists drugs, this view fixes a target and surfaces the diseases for which connected drugs have clinical evidence.

The dataset is built by joining two sources: clinical reports, which link drugs to diseases, and drug mechanism of action data, which links drugs to targets. Each row in the widget represents a drug linked to both the selected target and disease. The **maximum stage** shown is the highest clinical development stage that the drug has reached across all its supporting indications.

```mermaid
flowchart TD
    T["<b>Target</b><br>e.g. BRAF"]
    D["<b>Drug</b><br>e.g. Vemurafenib"]
    DIS["<b>Disease</b><br>e.g. Melanoma"]

    T -->|"Mechanism of action"| D
    D -->|"Clinical report"| DIS

    subgraph inferred["Inferred target–disease"]
        T
        D
        DIS
    end

    style T fill:#dcd8f5,stroke:#7b6fc4,color:#3b2e8a
    style D fill:#c8f0e8,stroke:#3a9e82,color:#1a5c4a
    style DIS fill:#fce8dc,stroke:#c97a50,color:#8b3a10
    style inferred fill: transparent, stroke:#ccc, color:#888
```

{% hint style="info" %}
For a full description of the **clinical stage categories** and their ranking, see [Clinical stage categories](../drug/clinical-report.md#clinical-stage-categories) in the Clinical Report page.
{% endhint %}
