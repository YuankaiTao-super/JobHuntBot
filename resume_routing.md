# Resume Routing

## Strategy

- Use **role-family routing plus light Precision tailoring**.
- Quantitative Research / Trading and Risk are the primary search families.
- Data and Operations Research are secondary families.
- Apply all screening exclusions before choosing or tailoring a resume.

## Immutable and Base-File Policy

- Everything inside `my-materials/original_CV/` is an immutable reference. Never modify, overwrite, rename, or delete it.
- Quant, Risk, Data, and BA are reusable base resumes. Do not edit their source files in place for a specific application.
- Copy the selected base `.tex` and required local dependencies into `my-materials/tailored/<company>/<role>/` before making job-specific edits.
- Never overwrite a base PDF. Compile a new, clearly named PDF in the tailored job directory.

## Available Base Resumes

| Version | PDF | Editable source | Status |
|---|---|---|---|
| Original reference | `my-materials/original_CV/CV_Yuankai_Tao.pdf` | `my-materials/original_CV/CV_Yuankai_Tao.tex` | Available; immutable reference only |
| Quant | `my-materials/Quant/CV_Yuankai_Tao_Quant.pdf` | `my-materials/Quant/CV_Yuankai_Tao_Quant.tex` | Available |
| Risk | `my-materials/Risk/CV_Yuankai_Tao_Risk.pdf` | `my-materials/Risk/CV_Yuankai_Tao_Risk.tex` | Available |
| Data | `my-materials/Data/CV_Yuankai_Tao_Data.pdf` | `my-materials/Data/CV_Yuankai_Tao_Data.tex` | Available |
| BA | `my-materials/BA/CV_Yuankai_Tao_BA.pdf` | `my-materials/BA/CV_Yuankai_Tao_BA.tex` | Available |

## Routing Table

| Priority | Role family | Default base | Typical titles/signals | Do not use for |
|---|---|---|---|---|
| Primary | Quantitative Research / Trading | Quant | Quantitative Research Intern, Quantitative Trading Intern, Systematic Research, Alpha Research, derivatives or portfolio modeling | Deep Learning-focused; required C++ or Java; PhD-only |
| Primary | Risk Analytics / Quantitative Risk | Risk | Market Risk, Model Risk, Credit Risk, Portfolio Risk, Risk Analytics, Model Validation, VaR/CVaR | Pure audit/accounting unless selected; required C++ or Java |
| Secondary | Data Science / Data Engineering | Data | Data Scientist Intern, Applied ML, Data Engineer, Analytics Engineer; Python/SQL, pipelines, cloud, tabular ML | Deep Learning-focused; required C++ or Java; PhD-only |
| Secondary | Business / Data Analytics | BA | Business Analyst, Data Analyst, BI/Reporting, KPI, dashboard, Excel/SQL-heavy analytics | Software engineering or research-heavy roles |
| Secondary | Operations Research / Optimization | Quant by default; Data when pipeline/analytics-heavy | Operations Research Intern, Optimization Scientist, Decision Scientist, Supply Chain Analytics, simulation, stochastic modeling | Senior operations management; required C++ or Java |

## Tie-Break Rules

1. Use Risk rather than Quant when the JD centers on controls, exposure, VaR/CVaR, stress testing, validation, credit, or regulatory risk.
2. Use Quant rather than Risk when the JD centers on alpha, forecasting, trading strategies, derivatives, stochastic modeling, or portfolio construction.
3. Use Data rather than BA when Python pipelines, ML, cloud, databases, or production data processing are central.
4. Use BA rather than Data when Excel, SQL reporting, KPI design, dashboards, stakeholder analysis, or business decisions are central.
5. For Operations Research, use Quant for mathematical modeling/optimization and Data for analytics/pipeline implementation.
6. If two routes remain equally plausible, stop and show the user both choices rather than silently choosing.

## Tailoring Threshold

- **High fit:** create a tailored copy unless the user asks for the stable base version.
- **Medium fit:** use the base PDF by default; tailor only if a few truthful keyword/order changes materially improve alignment.
- **Low fit / Stretch:** do not tailor unless the user explicitly selects the role.
- **Excluded:** do not route or tailor Deep Learning-focused roles, roles requiring C++ or Java, or roles requiring PhD-student status.

## JD Tailoring Procedure

1. Preserve the full JD in the job record when an application is actually attempted.
2. Separate required qualifications from preferred qualifications.
3. Select 2–4 relevant experiences from `experience_bank.md` and tell the user which were selected and why.
4. Build a truthful keyword list supported by existing evidence.
5. Copy the base `.tex` and its required local files to the tailored job directory.
6. Reorder or tighten bullets, adjust emphasis, and add/remove supported Skills keywords. Do not fabricate claims.
7. Compile a new PDF and inspect it for errors, overflow, missing glyphs, broken links, and unintended extra pages.
8. Record the exact output path in `job_pool.csv`; after confirmed submission, record it in `application_log.csv`.

## Naming Convention

Use:

`my-materials/tailored/<company-slug>/<role-slug>/CV_Yuankai_Tao_<Company>_<Role>_vNN.{tex,pdf}`

Never overwrite an earlier tailored version.

## Final Verification

- Confirm that the chosen route matches the JD rather than only the title.
- Confirm that every added skill or keyword is supported.
- Confirm that the base source remains unchanged.
- Confirm that the PDF displayed by the ATS has the intended filename.
- Stop before final submission and show the user the selected resume, experiences, key edits, and high-impact answers.
