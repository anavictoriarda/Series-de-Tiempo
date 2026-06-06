\documentclass[11pt, a4paper]{article}

% ---------------------------------------------------------------------------
% Paquetes
% ---------------------------------------------------------------------------
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage[spanish]{babel}
\usepackage{geometry}
\geometry{margin=2.5cm}
\usepackage{hyperref}
\hypersetup{
    colorlinks = true,
    linkcolor  = black,
    urlcolor   = blue!60!black,
}
\usepackage{listings}
\usepackage{xcolor}
\usepackage{booktabs}
\usepackage{parskip}
\usepackage{titlesec}

% ---------------------------------------------------------------------------
% Estilo de código
% ---------------------------------------------------------------------------
\definecolor{codegray}{rgb}{0.95,0.95,0.95}
\definecolor{codecomment}{rgb}{0.4,0.4,0.4}
\lstset{
    backgroundcolor = \color{codegray},
    basicstyle      = \ttfamily\small,
    commentstyle    = \color{codecomment}\itshape,
    breaklines      = true,
    frame           = single,
    framerule       = 0pt,
    rulecolor       = \color{codegray},
    xleftmargin     = 8pt,
    xrightmargin    = 8pt,
}

% ---------------------------------------------------------------------------
% Título
% ---------------------------------------------------------------------------
\title{
    \textbf{Series-de-Tiempo}\\[6pt]
    \large Repositorio de código — Cálculo Estocástico y Series de Tiempo
}
\author{0250749-design}
\date{Universidad Panamericana \\ 2026}

% ---------------------------------------------------------------------------
\begin{document}
% ---------------------------------------------------------------------------

\maketitle
\tableofcontents
\bigskip
\hrule
\bigskip

% ===========================================================================
\section{Descripción general}
% ===========================================================================

Este repositorio contiene el código fuente de los proyectos y visualizaciones
desarrollados para los cursos de \textbf{Cálculo Estocástico} y
\textbf{Series de Tiempo}. Incluye un motor de simulación en Python,
un modelo SARIMA aplicado al dataset clásico \emph{AirPassengers},
una visualización interactiva del Teorema de Donsker en React, y
una animación del Área de Lévy.

% ===========================================================================
\section{Estructura del repositorio}
% ===========================================================================

\begin{lstlisting}
Series-de-Tiempo/
|-- Codigo.py              <- Motor principal del Proyecto Final (Lab 1-5 + Proyecto 6)
|-- seriesdetiempo.py      <- Modelo SARIMA(0,1,1)(0,1,1)_12 sobre AirPassengers
|-- donsker.jsx            <- Visualizacion interactiva del Teorema de Donsker (React)
|-- levy_area_Z2.gif       <- Animacion del Area de Levy
|-- README.tex             <- Este documento
\end{lstlisting}

% ===========================================================================
\section{Archivos}
% ===========================================================================

% ---------------------------------------------------------------------------
\subsection{\texttt{Codigo.py} — Motor del Proyecto Final de Cálculo Estocástico}
% ---------------------------------------------------------------------------

Motor de cálculo completo del Proyecto Final. Genera datos sintéticos
calibrados a parámetros realistas de una acción tecnológica (AAPL),
ejecuta cinco laboratorios de análisis y un proyecto de cierre, y
exporta todas las figuras en PDF junto con un archivo \texttt{results.json}
con los resultados numéricos.

\medskip
\textbf{Laboratorios que ejecuta:}

\begin{center}
\begin{tabular}{@{}lll@{}}
\toprule
\textbf{Lab} & \textbf{Tema} & \textbf{Método} \\
\midrule
1 & Estimación de un MBG con datos de una acción & MLE, simulación Monte Carlo \\
2 & Volatilidad realizada y ventanas móviles      & Desv. estándar móvil anualizada \\
3 & Opciones europeas vanilla                     & Monte Carlo + Black-Scholes \\
4 & Opciones americanas (put)                     & Árbol binomial \\
5 & Opciones parisinas down-and-out               & Monte Carlo con reloj de permanencia \\
\midrule
Proyecto 6 & Superficie de precio parisino $V(H,D)$ & Monte Carlo, heatmap $H \times D$ \\
\bottomrule
\end{tabular}
\end{center}

\medskip
\textbf{Dependencias:}

\begin{lstlisting}[language=bash]
pip install numpy pandas matplotlib scipy
# Opcional para datos reales:
pip install yfinance
\end{lstlisting}

\textbf{Ejecución:}

\begin{lstlisting}[language=bash]
python Codigo.py
\end{lstlisting}

Las figuras se guardan en \texttt{figs/} y los resultados numéricos en
\texttt{results.json}.

% ---------------------------------------------------------------------------
\subsection{\texttt{seriesdetiempo.py} — Modelo SARIMA sobre AirPassengers}
% ---------------------------------------------------------------------------

Ajusta un modelo \textbf{SARIMA$(0,1,1)(0,1,1)_{12}$} al dataset clásico
\emph{AirPassengers} (1949--1960, pasajeros mensuales de aerolíneas).
El script carga los datos desde GitHub de Plotly, los preprocesa con
\texttt{pandas} y estima el modelo con \texttt{statsmodels}.
Incluye un mecanismo de respaldo que genera una serie sintética si no
hay conexión a internet.

\medskip
\textbf{Modelo:} SARIMA$(p,d,q)(P,D,Q)_s$ con
$p=0,\ d=1,\ q=1,\ P=0,\ D=1,\ Q=1,\ s=12$.

\medskip
\textbf{Dependencias:}

\begin{lstlisting}[language=bash]
pip install pandas matplotlib statsmodels
\end{lstlisting}

\textbf{Ejecución:}

\begin{lstlisting}[language=bash]
python seriesdetiempo.py
\end{lstlisting}

% ---------------------------------------------------------------------------
\subsection{\texttt{donsker.jsx} — Visualización del Teorema de Donsker}
% ---------------------------------------------------------------------------

Componente de React que ilustra la convergencia en distribución del
Teorema de Donsker (1951):

\[
W_n(t) = \frac{S_{\lfloor nt \rfloor}}{\sqrt{n}} \xrightarrow{d} B(t)
\quad \text{cuando } n \to \infty
\]

donde $S_k = \xi_1 + \cdots + \xi_k$ es una caminata aleatoria con
$\xi_i \in \{-1, +1\}$ equiprobables, y $B(t)$ es el movimiento
browniano estándar.

\medskip
\textbf{Funcionalidades interactivas:}
\begin{itemize}
    \item Animación cuadro a cuadro con control de velocidad ($0.5\times$, $1\times$, $2\times$, $4\times$).
    \item Selector de $n \in \{100, 500, 1000, 5000\}$ para observar la convergencia.
    \item Generación de nuevas muestras con rastros de trayectorias anteriores.
    \item Pausa, reinicio e indicador de valor instantáneo $W_n(t)$.
\end{itemize}

\medskip
\textbf{Requisitos:} React 18+, sin dependencias externas adicionales.

% ---------------------------------------------------------------------------
\subsection{\texttt{levy\_area\_Z2.gif} — Animación del Área de Lévy}
% ---------------------------------------------------------------------------

Animación que ilustra el Área de Lévy de un proceso estocástico
bidimensional. Generada con \texttt{matplotlib} en Python.

% ===========================================================================
\section{Reproducibilidad}
% ===========================================================================

\begin{itemize}
    \item \texttt{Codigo.py} usa semilla fija (\texttt{seed=20260526}) para
          garantizar resultados idénticos en cada ejecución.
    \item \texttt{seriesdetiempo.py} incluye respaldo con datos sintéticos
          si la conexión a internet no está disponible.
    \item Los datos pesados y PDFs de entrega \textbf{no se incluyen} en
          este repositorio; residen en Google Drive.
\end{itemize}

% ===========================================================================
\section{Curso}
% ===========================================================================

\begin{center}
\begin{tabular}{@{}ll@{}}
\toprule
Universidad & Universidad Panamericana \\
Cursos      & Cálculo Estocástico · Series de Tiempo \\
Año         & 2026 \\
\bottomrule
\end{tabular}
\end{center}

% ---------------------------------------------------------------------------
\end{document}
% ---------------------------------------------------------------------------
\end{antml:parameter>
