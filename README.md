Series-de-Tiempo
Repositorio de código para los cursos de Cálculo Estocástico y Series de Tiempo.

Estructura
Series-de-Tiempo/
├── Codigo.py            ← Motor principal del Proyecto Final (Labs 1–5 + Proyecto 6)
├── seriesdetiempo.py    ← Modelo SARIMA(0,1,1)(0,1,1)₁₂ sobre AirPassengers
├── donsker.jsx          ← Visualización interactiva del Teorema de Donsker (React)
└── levy_area_Z2.gif     ← Animación del Área de Lévy

Archivos
Codigo.py — Motor del Proyecto Final de Cálculo Estocástico
Genera datos sintéticos calibrados a parámetros de AAPL, ejecuta cinco laboratorios y exporta figuras en PDF y un archivo results.json con resultados numéricos.
LabTemaMétodo1Estimación de un MBG con datos de una acciónMLE + Monte Carlo2Volatilidad realizada y ventanas móvilesDesv. estándar móvil anualizada3Opciones europeas vanillaMonte Carlo + Black-Scholes4Opciones americanas (put)Árbol binomial5Opciones parisinas down-and-outMonte Carlo con reloj de permanenciaProyecto 6Superficie de precio parisino V(H,D)Monte Carlo, heatmap H × D
Dependencias:
bashpip install numpy pandas matplotlib scipy
# Opcional para datos reales:
pip install yfinance
Ejecución:
bashpython Codigo.py

seriesdetiempo.py — Modelo SARIMA sobre AirPassengers
Ajusta un modelo SARIMA(0,1,1)(0,1,1)₁₂ al dataset clásico AirPassengers (1949–1960). Incluye respaldo con datos sintéticos si no hay conexión a internet.
Dependencias:
bashpip install pandas matplotlib statsmodels
Ejecución:
bashpython seriesdetiempo.py

donsker.jsx — Visualización del Teorema de Donsker
Componente React que ilustra la convergencia en distribución:
Wn(t)=S⌊nt⌋n→dB(t)n→∞W_n(t) = \frac{S_{\lfloor nt \rfloor}}{\sqrt{n}} \xrightarrow{d} B(t) \quad n \to \inftyWn​(t)=n​S⌊nt⌋​​d​B(t)n→∞
donde Sk=ξ1+⋯+ξkS_k = \xi_1 + \cdots + \xi_k
Sk​=ξ1​+⋯+ξk​ es una caminata aleatoria con ξi∈{−1,+1}\xi_i \in \{-1,+1\}
ξi​∈{−1,+1} equiprobables y B(t)B(t)
B(t) es el movimiento browniano estándar.
Funcionalidades: animación con control de velocidad, selector de n∈{100,500,1000,5000}n \in \{100, 500, 1000, 5000\}
n∈{100,500,1000,5000}, generación de nuevas muestras y rastros de trayectorias anteriores.

levy_area_Z2.gif — Animación del Área de Lévy
Animación generada con matplotlib que ilustra el Área de Lévy de un proceso estocástico bidimensional.

Reproducibilidad

Codigo.py usa semilla fija (seed=20260526) para resultados idénticos en cada ejecución.
seriesdetiempo.py incluye datos sintéticos de respaldo si no hay internet.
Los PDFs de entrega y datos pesados no están en este repositorio — residen en Google Drive.


Curso
UniversidadUniversidad PanamericanaCursosCálculo Estocástico · Series de TiempoAño2026
