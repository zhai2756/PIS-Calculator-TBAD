# PIS Calculator for TBAD Endovascular Repair

> **Post-Implantation Syndrome (PIS) Risk Prediction Calculator**  
> For patients undergoing thoracic endovascular aortic repair (TEVAR) for type B aortic dissection (TBAD).

---

## 🔗 Live Calculator

**👉 [Click here to use the calculator](https://yourname.github.io/PIS-Calculator-TBAD)**

*(Replace `yourname` with your actual GitHub username after deployment)*

---

## 📋 Overview

This web-based calculator implements a validated **Ridge Logistic Regression** model to predict the risk of post-implantation syndrome (PIS) after TBAD endovascular repair. 

- **Development cohort:** 554 patients (PIS rate: 13.4%)
- **External validation:** 174 patients (AUC-ROC: 0.769; AUC-PR: 0.531; Brier score: 0.195)
- **Selected model:** Ridge Logistic Regression (penalty = 'elasticnet', l1_ratio = 0.0, C = 0.131)
- **Model selection rationale:** Reliable generalization (external gap = –0.003), non-significant DeLong test vs. complex models (p = 0.27), superior interpretability for clinical nomogram construction.

---

## 🩺 How to Use

1. Enter the patient's **9 preoperative variables** (all routinely available in clinical practice):
   - Age (years)
   - Surgery duration (minutes)
   - Contrast dose (mL)
   - Stent count (number)
   - TBAD stratum (Complicated / High-risk / Uncomplicated)
   - Neutrophils (×10⁹/L)
   - Lymphocytes (×10⁹/L)
   - APTT (seconds)
   - Fibrinogen (g/L)

2. Click **"Calculate PIS Risk"**.

3. The calculator returns:
   - Individualized PIS probability (%)
   - Risk stratification tier (Low / Medium / High)
   - Clinical recommendations based on the risk tier

---

## ⚠️ Risk Stratification Thresholds

| Risk Tier | Probability | Clinical Recommendation |
|-----------|-------------|------------------------|
| **Low** | < 10% | Standard perioperative care; routine monitoring |
| **Medium** | 10% – 30% | Enhanced inflammatory monitoring; consider prophylactic NSAIDs or corticosteroids if no contraindications |
| **High** | > 30% | Intensive monitoring (q6h temperature, inflammatory markers); early CT imaging if fever develops; multidisciplinary management |

---

## 📊 Model Formula (Raw-Value Logistic Model)

```
logit(PIS) = 0.3626
           + (–0.000539 × Age)
           + (0.000017 × Surgery_duration)
           + (–0.049867 × Contrast_dose)
           + (0.030304 × Stent_count)
           + (–1.159217 × TBAD_stratum)
           + (0.028992 × Neutrophils)
           + (0.011586 × Lymphocytes)
           + (–0.000906 × APTT)
           + (0.022362 × Fibrinogen)

PIS Probability = 1 / (1 + e^(–logit))
```

**TBAD stratum coding:** 0 = Complicated, 1 = High-risk, 2 = Uncomplicated. Higher scores indicate lower PIS risk (β = –1.159 per unit).

---

## ✅ Validation & Reproducibility

- The calculator was **internally verified** by back-calculation against the development cohort (n = 554), showing **perfect agreement** (error < 10⁻⁶) with the original standardized model.
- All standardization parameters (RobustScaler + StandardScaler) are documented in the Supplementary Material of the associated manuscript.
- The calculator is a **single, self-contained HTML file** with no external dependencies or server-side processing required.

---

## 📄 Citation

If you use this calculator in your research or clinical practice, please cite:

```
[Your Name]. A Ridge Logistic Regression Model for Predicting Post-Implantation Syndrome 
After TBAD Endovascular Repair: Development, Validation, and a Web-Based Calculator. 
Journal of Vascular Surgery / European Journal of Vascular and Endovascular Surgery, [Year].
```

---

## 📜 License

This project is licensed under the **MIT License** — see [LICENSE](./LICENSE) for details.

> **Note:** This calculator is provided for academic and educational purposes. It is intended to **assist clinical decision-making, not replace it**. Always use your professional judgment when managing patients.

---

## 🛠️ Technical Details

- **Frontend:** Pure HTML5 + CSS3 + Vanilla JavaScript (no frameworks, no build step)
- **Backend:** None — all computation runs client-side in the browser
- **Compatibility:** Modern browsers (Chrome, Firefox, Safari, Edge) on desktop and mobile devices
- **Offline use:** The HTML file can be saved locally and opened directly in any browser without internet connection

---

## 📬 Contact

For questions, issues, or collaboration inquiries, please contact:

- [Your Name] — [Your Email]  
- [Your Institution / Department]

---

## 🙏 Acknowledgments

This calculator was developed as part of a clinical prediction modeling study following the **TRIPOD** guidelines and the **JVS/EJVES** standard for machine learning models in vascular surgery. Model development involved 6-fold nested cross-validation with stratified sampling, external validation on an independent cohort, and comprehensive calibration and decision-curve analysis.
