[README_SeriesTiempo.md](https://github.com/user-attachments/files/28657510/README_SeriesTiempo.md)

# Series-de-Tiempo

Repositorio de código para el curso de **Series de Tiempo**.

---

## Estructura

```
Series-de-Tiempo/
└── seriesdetiempo.py    ← Modelo SARIMA(0,1,1)(0,1,1)₁₂ sobre AirPassengers
```

---

## Archivos

### `seriesdetiempo.py` — Modelo SARIMA sobre AirPassengers

Ajusta un modelo **SARIMA(0,1,1)(0,1,1)₁₂** al dataset clásico AirPassengers
(1949–1960, pasajeros mensuales de aerolíneas). El script carga los datos,
los preprocesa con `pandas` y estima el modelo con `statsmodels`.
Incluye un mecanismo de respaldo que genera una serie sintética si no
hay conexión a internet.

**Modelo:** SARIMA$(p,d,q)(P,D,Q)_s$ con $p=0,\ d=1,\ q=1,\ P=0,\ D=1,\ Q=1,\ s=12$.

**Dependencias:**
```bash
pip install pandas matplotlib statsmodels
```

**Ejecución:**
```bash
python seriesdetiempo.py
```

---

## Reproducibilidad

Los PDFs de entrega **no están en este repositorio** — residen en Google Drive.

---

## Curso

| | |
|---|---|
| Universidad | Universidad Panamericana |
| Curso | Series de Tiempo |
| Año | 2026 |
