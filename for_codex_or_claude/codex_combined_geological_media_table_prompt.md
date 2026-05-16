# Task: Build One Combined Geological Media Parameter Table for the Thesis

Hello. Please review my whole thesis project and prepare **one combined geological media parameter table**.

## Project Structure

Start from:

```text
main.tex
```

Then follow every:

```latex
\input{...}
\include{...}
```

recursively.

Read all imported thesis files, especially:

```text
introduction.tex
annotations.tex
chapters/chapter1/*
chapters/chapter2/*
chapters/chapter3/*
sources.tex
```

Then inspect the folder:

```text
Insar/data
```

This folder should contain tables with geological media / rock material parameters.

---

# Main Goal

I need **one final combined table** of geological media parameters that is consistent with the theory and mathematical formulation of the thesis.

The output should preferably be created in both formats:

```text
combined_geological_media_parameters.csv
combined_geological_media_parameters.tex
```

The CSV should be the main clean machine-readable table.

The LaTeX table should be suitable for inclusion in the thesis. If the full table is too wide for the main thesis text, create:

```text
combined_geological_media_parameters_compact.tex
combined_geological_media_parameters_full_appendix.tex
```

---

# Thesis Context

Thesis title:

```text
AI Directional Prediction of Thermoelastic Wave Propagation in Geological Media
```

The theoretical chapters define the problem using **effective material parameters** for a **locally homogeneous and isotropic thermoelastic medium**.

Important positioning:

Real geological media are heterogeneous, porous, fractured, layered, and often anisotropic. However, the mathematical formulation in the thesis uses simplified effective parameters for rock types such as sandstone, basalt, granite, and limestone.

Therefore:

- do not combine all available data blindly;
- first read the theory;
- identify which physical parameters are actually used;
- then decide which data from `Insar/data` is suitable.

---

# Step 1: Read Thesis Structure

Open `main.tex`.

Follow all imports recursively.

Create a short internal map of the thesis structure:

```text
main.tex
├── annotations.tex
├── introduction.tex
├── chapters/chapter1/...
├── chapters/chapter2/...
├── chapters/chapter3/...
└── sources.tex
```

Then briefly identify:

- where Chapter 1 is located;
- where Chapter 2 is located;
- where Chapter 3 is located;
- which variables and parameters are used in the thesis;
- which material parameters are needed for the mathematical formulation.

Do not rewrite the thesis text unless absolutely necessary.

---

# Step 2: Extract Required Theoretical Parameters

From the thesis theory, identify the material parameters required for the mathematical formulation and prediction framework.

Expected relevant parameters include:

```text
material / rock type
rock group
density rho
Young's modulus E
Poisson's ratio nu
shear modulus mu or G
bulk modulus K
Lamé parameter lambda
coefficient of linear thermal expansion alpha
thermal conductivity k
specific heat capacity Cp
volumetric heat capacity C = rho * Cp
thermoelastic coupling coefficient gamma = 3Kalpha
P-wave velocity Vp, if available
S-wave velocity Vs, if available
porosity, if available and relevant
```

Use the thesis as the source of truth for which columns are needed.

---

# Step 3: Inspect `Insar/data`

Open every relevant file in:

```text
Insar/data
```

Inspect all tables related to:

```text
geological media
rock types
density
porosity
elastic parameters
thermal parameters
thermoelastic parameters
P-wave velocity
S-wave velocity
material presets
sandstone
basalt
granite
limestone
```

For each table/file, identify:

```text
file name
columns
units
rock/material types included
whether the table is directly suitable, partially suitable, or not suitable
reason for inclusion or exclusion
```

---

# Step 4: Select Suitable Data

Create one combined table using only data that matches the thesis formulation.

Selection rules:

- Include only data relevant to thermoelastic wave propagation.
- Prefer effective parameters usable in a locally homogeneous isotropic thermoelastic model.
- Do not include unrelated columns.
- Do not include duplicate/conflicting rows without explaining the conflict.
- If the same material appears in multiple files, merge it carefully.
- If units differ, convert everything to SI units.
- If a derived parameter can be computed safely, compute it.
- If a parameter is missing, leave it blank or use `N/A`.
- Do not invent missing values.
- If a value is approximate or uncertain, mark it clearly in `notes`.
- If multiple values exist for the same material, preserve source information in `source_file` and explain in `notes`.

---

# Step 5: Use SI Units

Normalize units to SI:

```text
density: kg/m^3
Young's modulus: Pa
shear modulus: Pa
bulk modulus: Pa
Lamé parameter: Pa
thermal expansion coefficient: 1/K
thermal conductivity: W/(m*K)
specific heat capacity: J/(kg*K)
volumetric heat capacity: J/(m^3*K)
thermoelastic coupling coefficient: Pa/K
P-wave velocity: m/s
S-wave velocity: m/s
porosity: percent
```

If source data uses other units, convert carefully.

Examples:

```text
g/cm^3 -> kg/m^3
GPa -> Pa
km/s -> m/s
MPa -> Pa
```

---

# Step 6: Compute Derived Parameters Where Possible

Use these formulas only when the required input values are available and reliable.

```text
mu = E / (2 * (1 + nu))

K = E / (3 * (1 - 2 * nu))

lambda = E * nu / ((1 + nu) * (1 - 2 * nu))

C = rho * Cp

gamma = 3 * K * alpha

Vp = sqrt((K + 4 * mu / 3) / rho)

Vs = sqrt(mu / rho)
```

Important:

- Use SI units before computing.
- Clearly state which columns are original and which are derived.
- Do not compute a derived parameter if required inputs are missing.
- Do not compute if units are unclear.
- Do not silently overwrite original values with derived values.
- If both original and derived values exist, preserve the original and add a note.

---

# Step 7: Final Combined Table Structure

Create one final combined table.

Preferred columns:

```text
material
rock_group
rho_kg_m3
E_Pa
nu
mu_Pa
K_Pa
lambda_Pa
alpha_1_K
k_W_mK
Cp_J_kgK
C_J_m3K
gamma_Pa_K
Vp_m_s
Vs_m_s
porosity_percent
source_file
value_type
notes
```

Where:

```text
material = rock name, e.g. sandstone, basalt, granite, limestone
rock_group = sedimentary / igneous / metamorphic / carbonate / volcanic / etc.
source_file = data file from Insar/data
value_type = original / derived / approximate / mixed
notes = explanation of missing values, conversions, assumptions, conflicts
```

Adjust the columns only if the actual data requires a better structure, but keep the final table aligned with the thesis theory.

---

# Step 8: Output Files

Generate these files:

```text
combined_geological_media_parameters.csv
combined_geological_media_parameters.tex
```

If the LaTeX table is too wide, also generate:

```text
combined_geological_media_parameters_compact.tex
combined_geological_media_parameters_full_appendix.tex
```

The CSV must contain the full combined table.

The LaTeX table should be readable and suitable for thesis inclusion.

For LaTeX:

- use `table` environment;
- use `tabular` or `longtable` if needed;
- include a caption;
- include a label;
- avoid overly wide columns;
- use SI units in column names or table notes.

Example label:

```latex
\label{tab:combined_geological_media_parameters}
```

Example caption:

```latex
\caption{Combined effective material parameters for geological media used in the thermoelastic prediction framework.}
```

---

# Step 9: Final Report

After creating the files, report:

```text
1. Which thesis files were inspected.
2. Which data files in Insar/data were inspected.
3. Which tables were used.
4. Which tables were excluded and why.
5. Final columns of the combined table.
6. Unit conversions performed.
7. Derived formulas used.
8. Missing values.
9. Conflicting or duplicate materials.
10. Warnings about uncertain data.
11. Paths to generated CSV and LaTeX files.
```

---

# Important Constraints

Do not modify the thesis text unless explicitly necessary.

Do not add new theory.

Do not invent missing values.

Do not overclaim that the combined table represents exact real geological field conditions.

Treat all values as effective material parameters for simplified thermoelastic modelling.

Keep the table consistent with Chapters 1–3.

The final result must be **one combined table**, preferably in:

```text
CSV
LaTeX
```

The table should support the thesis methodology and mathematical formulation, not become an unrelated geological database.

---

# Before Starting

Before editing or generating files, first print a short plan:

```text
Plan:
1. Inspect main.tex and imported thesis files.
2. Extract required theoretical parameters.
3. Inspect Insar/data.
4. Select suitable columns and rows.
5. Normalize units.
6. Compute derived parameters where possible.
7. Generate one combined CSV table.
8. Generate one LaTeX table.
9. Report findings and warnings.
```
