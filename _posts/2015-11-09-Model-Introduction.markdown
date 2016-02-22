---
layout:     post
title:      Model Overview
date:       2015-11-09 12:00:00
author:     Shengyen Li
---
{% include latex.html %}

#Model Introduction

This computational framework provides a interdisciplinary environment for alloy design. One sample design procedure is demonstrated to select the chemical composition and processing conditions for high work to necking Ni${(1-x-y)}$Al$x$Cr$y$.

The classic nucleation, growth, and coarsening models with CALPHAD approach are used for simulating $\gamma^{\prime}$ precipitation. With the growth of the $\gamma^{\prime}$, the processing time is decided to maximize the yield stress at service temperature. To evaluate the stress-strain curve and work to necking, the mechanistic models including PyMKS and constitutive plastic deformation model are implemented. With the processing-structure-property correlation, genetic algorithm directs the search until the alloy requirements are satisfied.

![](https://farm2.staticflickr.com/1611/25171597896_08f0a1a6d1_o_d.png)


#Model calibration

##Processing-Structure correlation: Nucleation, Growth, and Coarsening models


<!-- \def\arraystretch{1}
\begin{table}[H]
\setlength{\extrarowheight}{0.15cm}
\centering
\caption{The functions and parameters ; }
\begin{tabular}{ c c c c c c c c }
\hline
  & \multicolumn{2}{c}{Experimental results} & & \multicolumn{4}{c}{Model parameters} \\
\cline{2-3}
\cline{5-8}
Sample  &  \parbox[t]{2cm}{\centering Composition\\ at\%}  &  \parbox[t]{1cm}{\centering $T_p$\\ Kelvin}  &  Ref  & \parbox[t]{1cm}{\centering $E_{int}$\\$mJ/m^2$}  & \parbox[t]{2cm}{\centering $N_0$\\ $1/m^2$} & \parbox[t]{2cm}{\centering $|\Delta H^{\gamma - \gamma^{\prime}}|$\\ $\times 10^{4}$ $J/mol$} & \parbox[t]{2.5cm}{\centering $\alpha_{int}$\\ $\times 10^{-6}$ $mol/m^2$} \\
\hline

\hline
\end{tabular}
\label{tab:kmodelparameters}
\end{table} -->

| Sample | Comp %| $T_p$ K | Ref | $E_{int} \frac{mJ}{m^2}$ | $N_0 \frac{1}{m^2}$ | $\| \Delta H^{\gamma  - \gamma'} \|$ | $\alpha_{int} 10^{-6}$ $mol/m^2$ |
| :----: | :---: | :-------: | :---: | :----------------------: | ------------------- |:-----------------------------------: | :----------------: |
|   Kt1  |  Ni-7.5Al-8.5Cr |  873  |  [1]    | 15  | $1.5 10^{26}$ |   1.52   | 0.99 |
|   Kt2  |  Ni-9.8Al-8.3Cr | 1073  |  [2] | 24  | $5.0 10^{27}$ |   1.34   | 1.80 |
|   Kt3  |  Ni-6.5Al-9.5Cr |  873  |  [3]  | 18  | $4.0 10^{26}$ |   1.64   | 1.10 |

![](https://farm2.staticflickr.com/1610/24830242879_697fcb6f21_o_d.png)
![](https://farm2.staticflickr.com/1687/24830242769_d7f46b9c13_o_d.png)

##Elastic deformation

To validate the PyMKS calculations, 16 microstructures are created for PyMKS and SfePy calculations. $V_f^{\gamma^{\prime}}$ increases from 5\% to 80\% and the Young's moduli (Y) is decided by the mean stress and applied elastic strain. SfePy and PyMKS take 22 and 1 seconds in average to finish 1 calculation.

![](https://farm2.staticflickr.com/1666/24571110373_944b1d9e45_o_d.png)

##Plastic deformation

\def\arraystretch{1}
\begin{table}[H]
\setlength{\extrarowheight}{0.15cm}
\centering
\caption{The testing samples for plastic deformation model \cite{le2014influence}; $\sigma_{ys}$ and $\varepsilon_{ys}$ represent the starting stress and strain of the calculation}
\begin{tabular}{ c c c c }
\hline
Sample   &  $V_f^{\gamma^{\prime}}$  &  $\sigma_{ys}$, MPa  & $\varepsilon_{ys}$, \%  \\
\hline
PD1    &  0.323  &  450  &  0.29 \\
PD2    &  0.296  &  560  &  0.33 \\
PD3    &  0.278  &  570  &  0.36 \\
\hline
\end{tabular}
\label{tab:IRRsamples}
\end{table}

![](https://farm2.staticflickr.com/1715/25104690141_1c32cca92c_o_d.png)

##Optimization for high work to necking

\begin{table}[H]
%\setlength{\extrarowheight}{0.15cm}
\centering
\caption{The domain for GA optimization }
\begin{tabular}{ c c c c }
\hline
     &  $C_{Al}$  &  $C_{Cr}$   &  $T_p$, Kelvin \\
\hline
min  &  \multicolumn{2}{c}{0.10}  &  1123  \\
max  &  0.25  &  0.20  &  1473  \\
\hline
\end{tabular}
\label{tab:optdomain}
\end{table}

(1) Precipitation stress: x-volume fraction of $\gamma^{\prime}$, y-mean radius and calculated APB energy
![](https://farm2.staticflickr.com/1690/24830243249_502c641963_o_d.png)
(2) Yield stress: x-processing temperature, y-Al and Cr content, wt%
![](https://farm2.staticflickr.com/1551/24830243629_5376343c25_h_d.jpg)
(3) Work to necking: x-processing temperature, y-Al and Cr content, wt%
![](https://farm2.staticflickr.com/1628/25079663882_8dbca803cc_h_d.jpg)


#Reference

##Nucleation

Russell KC, Advances in Colloid and Interface Science 1980;13:205

##Growth

Rougier L, Jacot A, Gandin CA, Di Napoli P, Th ́ery PY, Ponsen D, Jaquet V, Acta Materialia 2013;61:6396
Du Q, Poole W, Wells M, Acta Materialia 2012;60:3830
Aaron HB, Fainstein D, Kotler GR, Journal of applied physics 1970;41:4404
Chen Q, Jeppsson J, Agren J, Acta materialia 2008;56:1890
Perez M, Dumont M, Acevedo-Reyes D, Acta Materialia 2008;56:2119

##Coarsening

Perez M, Dumont M, Acevedo-Reyes D, Acta Materialia 2008;56:2119

##Yield Stress

Ahmadi M, Povoden-Karadeniz E, Whitmore L, Stockinger M, Falahati A, Kozeschnik E, Materials Science and Engineering: A 2014;608:114
Mishima Y, Ochiai S, Hamao N, Yodogawa M, Suzuki T, Japan Institute of Metals, Transactions 1986;27:656
Roth H, Davis C, Thomson R, Metallurgical and Materials Transactions A 1997;28:1329
Mecking H, Kocks U, Acta Metallurgica 1981;29:1865
Sinclair C, Poole W, Brechet Y, Scripta Materialia 2006;55:739
Reed RC, The superalloys. Cambridge Univ. Press, 2006
Crudden D, Mottura A, Warnken N, Raeisinia B, Reed R, Acta Materialia 2014;75:356
Collins D, Stone H, International Journal of Plasticity 2014;54:96
Kozar R, Suzuki A, Milligan W, Schirra J, Savage M, Pollock T, Metallurgical and Materials Transactions A 2009;40:1588

##PyMKS

Fast T, Niezgoda SR, Kalidindi SR, Acta Materialia 2011;59:699
Fast T, Kalidindi SR, Acta Materialia 2011;59:4595
Kalidindi SR, International Scholarly Research Notices 2012;2012

##Plastic deformation

Huang M, Rivera-D ́ıaz-del Castillo P, Bouaziz O, van der Zwaag S, Materials Science and Technology 2008;24:495
Huang M, Castillo PRDd, Van Der Zwaag S, Materials Science and Technology 2007;23:1105
Rivera-D ́ıaz-del Castillo P, Hayashi K, Galindo-Nava E, Materials Science and Technology 2013;29:1206
