# qubo-bipartite-matching-project-qmss26
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/annmariak-007/qubo-bipartite-matching-project-qmss26/blob/main/Ann_QMSS26_Final_Project.ipynb)

## **Dataset**

**Nombre del dataset** : Data México Employment and Industry Survey Subinstance

**Fuente oficial o confiable** : Data México Portal

**Institución responsable** : Secretaría de Economía / INEGI

**URL de la fuente** : https://datamexico.org

**Raw URL of the CSV used in data** : https://raw.githubusercontent.com/annmariak-007/qubo-bipartite-matching-project-qmss26/refs/heads/main/data/dataset_real_4x4.csv

**Licencia o condiciones de uso** : Creative Commons Attribution 4.0 International

**Fecha de consulta** : 2026-06-30

**Dominio del problema** : Urban Employment & Regional Talent Allocation


## **Modelado**

Conjunto A (Set A - Entities): 4 Specialized Professional Skill Profiles.

* **A1**: Data Analyst

* **A2**: Logistics Operator

* **A3** : Customer Service Lead

* **A4** : Software Developer

Criterio para elegir exactamente 4 elementos de A: Selection based on the highest-growth employment volume indices reported in the primary technical service sector categories

Conjunto B (Set B - Entities): 4 Mexican Industrial State Regions.

* **B1** : Nuevo León (Industrial Hub)

* **B2**: Jalisco (Tech/Software Hub)

* **B3** : Querétaro (Aerospace Hub)

* **B4** : Quintana Roo (Tourism Hub)

Criterio para elegir exactamente 4 elementos de B: Selection based on representative economic diversity across four key geographic industrial ecosystems in Mexico.

Definición de x_ij = 1: Professional skill profile group i is officially allocated to regional economic hub j.

Interpretación de x_ij = 0: Professional skill profile group i is not allocated to regional economic hub j.

## Matriz de Score

**Columnas usadas:** Regional Median Monthly Salary and Aggregate Job Vacancy Volume.

**Fórmula exacta de \(S_{ij}\):**

$$
S_{ij} = 0.5 \cdot \mathrm{Normalized}(\mathrm{Salary}_{ij}) +
0.5 \cdot \mathrm{Normalized}(\mathrm{Vacancy}_{ij})
$$

**Explicación:**  
The formula creates a composite suitability index normalized between **0.0** and **10.0**. It balances regional market demand (vacancy volume) with financial compensation (salary), rewarding matches where both indices are optimally aligned.

**Matriz de compatibilidad \(S\) (4×4):**

|             | B1 (Nuevo Leon) | B2 (Jalisco) | B3 (Queretaro) | B4 (Quintana Roo) |
|-------------|----------------:|-------------:|---------------:|------------------:|
| **A1 (Data Analyst)** | 7.0 | 8.5 | 6.0 | 4.5 |
| **A2 (Logistics Operator)** | 9.0 | 6.5 | 8.0 | 3.5 |
| **A3 (Customer Service Lead)** | 5.5 | 6.0 | 5.0 | 9.5 |
| **A4 (Software Developer)** | 7.5 | 9.5 | 7.0 | 3.0 |

## Restricciones

**Restricción de fila (Row Constraint):**

$$
\sum_{j} x_{ij} = 1
$$

Each professional profile in **A** must be matched to **exactly one** regional hub in **B**.

---

**Restricción de columna (Column Constraint):**

$$
\sum_{i} x_{ij} = 1
$$

Each regional hub in **B** must accept **exactly one** professional profile from **A**.

---

## Justificación de Bipartito

The problem requires a **one-to-one assignment** between two distinct sets (**Workers** $\rightarrow$ **Regions**) without allowing pairings within the same set. Therefore, it is a classical **bipartite matching** problem that can be naturally formulated as a **QUBO (Quadratic Unconstrained Binary Optimization)** model and solved using both classical optimization and **QAOA**.

---

## Resultados

### Exact Classical Solution
The best classical solution has an energy of -34.0 and a score of 34.0. The optimal assignment found was:
* A1 to B3
* A2 to B1
* A3 to B4
* A4 to B2
And the Optimal Bitstring is [0010100000010100]

---

### Local QAOA Result

The local QAOA simulation observed a best energy of -34.0 (matching the classical optimum) with a score of 34.0.

**Best Sampled Bitstring** : [Insert the top sampled bitstring from your QAOA output]

---

### Classical vs. Local QAOA Comparison:

- **Classical optimum energy:** -34
- **Local QAOA energy:** -34
- **Do both methods reach the same optimum?** Yes. In this small instance, the local QAOA simulation successfully identified the classical optimum (energy -34.0). However, the probability of sampling this solution is low, highlighting the need for optimization and potentially post-processing or hybrid techniques for larger instances.

**Analysis**

If both methods produce the same bitstring (or an equivalent optimal assignment), the Local QAOA successfully reproduces the classical optimum for this 4×4 bipartite matching instance. Any discrepancy indicates that the variational optimization did not fully converge or became trapped in a local optimum.

---

## Ética y Limitaciones

### Riesgos éticos

This project uses **aggregated and anonymized employment data** describing professional roles and regional labor-market indicators. No personally identifiable information (PII), sensitive personal data, or contact information was collected, stored, or processed. The optimization model assigns professional profiles to regional hubs using aggregated statistics only, ensuring compliance with basic privacy and ethical data-handling principles.

### Medidas de mitigación

- The dataset consists entirely of aggregated public statistics.
- No individual workers are identified or tracked.
- The optimization is performed on job-role and regional-level information only, preserving privacy and reducing ethical risks.

### Limitaciones del modelo

The current implementation is a **4 × 4** proof-of-concept designed to demonstrate the formulation of a bipartite matching problem as a **QUBO (Quadratic Unconstrained Binary Optimization)** model.

While the methodology scales conceptually, larger real-world instances involving thousands of workers and regions would require significantly greater computational resources. Classical exact methods become increasingly expensive, while current quantum hardware and QAOA simulations are limited by the exponential growth of the quantum state space (\(2^N\)).

### Biases

The dataset was constructed from publicly available government employment statistics. Although these sources are considered reliable, they may underrepresent informal employment sectors or rapidly changing labor-market conditions. Consequently, the optimization may favor regions and occupations that are better represented in official datasets.

---

## Ejecución

### Instrucciones para Google Colab

Click the badge at the top of the readme to launch.

---

### Error-Free Execution Guide

Select  **Runtime → Run all**. The script is designed to process the CSV automatically and generate the QUBO Hamiltonian and resulting energy histograms without intermediate setup required.

