# 🆕 Indications

The **Indications** widget provides a drug-centric view of the same Clinical Indications dataset described in the [Drugs and Clinical Candidates](../disease-or-phenotype/drugs.md) section of the Drug page. In this case, the drug is fixed, and the widget displays all diseases for which it has clinical evidence, aggregated across sources and [development stages](clinical-report.md#clinical-stage-categories).

The same aggregation logic applies: clinical reports sharing the same drug and disease are consolidated into a single record, and the maximum clinical stage is assigned using the same ranking rules.

```mermaid
flowchart LR
    CT["<b>Clinical trial</b> <br>NCT02684006 · Phase III</br>"]
    DL["<b>Drug label</b> <br>FDA label · Approval</br>"]
    CI["<b>Curated indication</b><br>ChEMBL · Phase II</br>"]
    DW["<b>Drug warning</b><br>ChEMBL · Withdrawal</br>"]

    CLIN["<b>Clinical indication</b><br>Drug A · Disease B</br>4 contributing reports</br>Sources: trial, label, ChEMBL"]

    APP["<b>Approval</b>"]

    CT --> CLIN
    DL --> CLIN
    CI --> CLIN
    DW --> CLIN
    CLIN --> APP

    subgraph reports["Clinical Reports"]
        CT
        DL
        CI
        DW
    end

    subgraph indication["Clinical indication"]
        CLIN
    end

    subgraph maxstage["Max stage"]
        APP
    end

    style CT fill:#c8f0e8,stroke:#3a9e82,color:#1a5c4a
    style DL fill:#c8f0e8,stroke:#3a9e82,color:#1a5c4a
    style CI fill:#c8f0e8,stroke:#3a9e82,color:#1a5c4a
    style DW fill:#c8f0e8,stroke:#3a9e82,color:#1a5c4a
    style CLIN fill:#dcd8f5,stroke:#7b6fc4,color:#3b2e8a
    style APP fill:#fce8dc,stroke:#c97a50,color:#8b3a10
    style reports fill: transparent, stroke: transparent
    style indication fill: transparent, stroke: transparent
    style maxstage fill: transparent, stroke: transparent
```

{% hint style="info" %}
For a full description of the **clinical stage categories** and their ranking, see [Clinical stage categories](clinical-report.md#clinical-stage-categories) in the Clinical Report page.
{% endhint %}

