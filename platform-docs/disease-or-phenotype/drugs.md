# 🆕 Drugs and Clinical Candidates

The **Drugs and Clinical Candidates** widget provides a disease-centric view of drugs and clinical candidates with evidence for the disease, based on the **Clinical Indications** dataset.&#x20;

A clinical indication consolidates all clinical reports sharing the same drug and disease into a single record, aggregating evidence across sources and development stages while preserving traceability to each contributing report.

For each drug/indication pair, the widget displays the **maximum clinical stage** reached across all contributing reports. This is determined by ranking harmonised clinical stage values from each clinical report, with one explicit rule: if at least one supporting report has a stage of _Phase IV_ or _Withdrawal_, the maximum clinical stage is set to _Approval_, reflecting the assumption that marketing authorisation must have been reached before a post-marketing or withdrawal context can occur.

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
For a full description of the **clinical stage categories** and their ranking, see [Clinical stage categories](../drug/clinical-report.md#clinical-stage-categories) in the Clinical Report page.
{% endhint %}

