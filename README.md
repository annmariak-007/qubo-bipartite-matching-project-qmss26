# qubo-bipartite-matching-project-qmss26
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/annmariak-007/qubo-bipartite-matching-project-qmss26/blob/main/Ann_QMSS26_Final_Project.ipynb)

Dataset

Nombre del dataset: Data México Employment and Industry Survey Subinstance

Fuente oficial o confiable: Data México Portal

Institución responsable: Secretaría de Economía / INEGI

URL de la fuente: https://datamexico.org

Raw URL of the CSV used in data: https://raw.githubusercontent.com/annmariak-007/qubo-bipartite-matching-project-qmss26/refs/heads/main/data/dataset_real_4x4.csv

Licencia o condiciones de uso: Creative Commons Attribution 4.0 International

Fecha de consulta: 2026-06-30

Dominio del problema: Urban Employment & Regional Talent Allocation


Modelado

Conjunto A (Set A - Entities): 4 Specialized Professional Skill Profiles.

A1: Data Analyst

A2: Logistics Operator

A3: Customer Service Lead

A4: Software Developer

Criterio para elegir exactamente 4 elementos de A: Selection based on the highest-growth employment volume indices reported in the primary technical service sector categories

Conjunto B (Set B - Entities): 4 Mexican Industrial State Regions.

B1: Nuevo León (Industrial Hub)

B2: Jalisco (Tech/Software Hub)

B3: Querétaro (Aerospace Hub)

B4: Quintana Roo (Tourism Hub)

Criterio para elegir exactamente 4 elementos de B: Selection based on representative economic diversity across four key geographic industrial ecosystems in Mexico.

Definición de x_ij = 1: Professional skill profile group i is officially allocated to regional economic hub j.

Interpretación de x_ij = 0: Professional skill profile group i is not allocated to regional economic hub j.

Matriz de scoreColumnas usadas: Regional Median Monthly Salary and Aggregate Job Vacancy Volume.Fórmula exacta de $S_{ij}$:$$S_{ij} = 0.5 \cdot \text{Normalized}(\text{Salary}_{ij}) + 0.5 \cdot \text{Normalized}(\text{Vacancy}_{ij})$$Explicación: The formula creates a composite suitability index normalized between 0.0 and 10.0. It balances regional market demand (vacancy volume) with financial compensation (salary), rewarding matches where both indices are optimally aligned.Matriz de compatibilidad $S$ (4x4):



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
