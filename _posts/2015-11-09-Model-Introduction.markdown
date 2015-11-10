---
layout:     post
title:      Model Overview
date:       2015-11-09 12:00:00
author:     Shengyen Li
---

#Model Introduction
This computational framework provides a interdisciplinary environment for alloy design. One sample design procedure is demonstrated to select the chemical composition and processing conditions for high work to necking Ni${(1-x-y)}$Al$x$Cr$y$.

The classic nucleation \cite{russell1980nucleation}, growth \cite{ rougier2013numerical,du2012mathematical,aaron1970diffusion,chen2008analytical,perez2008implementation}, and coarsening \cite{perez2008implementation} models with CALPHAD approach are used for simulating $\gamma^{\prime}$ precipitation. With the growth of the $\gamma^{\prime}$, the processing time is decided to maximize the yield stress at service temperature \cite{ahmadi2014yield, mishima1986solid, roth1997modeling, mecking1981kinetics, sinclair2006model, rivera2013computational,reed2006superalloys, crudden2014modelling, collins2014modelling, kozar2009strengthening}. To evaluate the stress-strain curve and work to necking, the mechanistic models including PyMKS \cite{fast2011new, fast2011formulation, kalidindi2012computationally} and constitutive plastic deformation model \cite{rivera2013computational,huang2008irreversible} are implemented. With the processing-structure-property correlation, genetic algorithm directs the search until the alloy requirements are satisfied.

<img src='Ni-SA.png'>


##Model calibration
###Processing-Structure correlation: Nucleation, Growth, and Coarsening models 
\def\arraystretch{1}
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
Kt1  &  Ni-7.5Al-8.5Cr &  873  &  \cite{booth2008effects}    & 15  & $1.5\times 10^{26}$ & 1.52 & 0.99 \\
Kt2  &  Ni-9.8Al-8.3Cr & 1073  &  \cite{sudbrack2008effects} & 24  & $5.0\times 10^{27}$ & 1.34 & 1.80 \\
Kt3  &  Ni-6.5Al-9.5Cr &  873  &  \cite{booth2010nanometer}  & 18  & $4.0\times 10^{26}$ & 1.64 & 1.10 \\
\hline
\end{tabular}
\label{tab:kmodelparameters}
\end{table}

<img src='Seidman_ternary_n.png'>
<img src='Seidman_ternary_r.png'>

###Elastic deformation
To validate the PyMKS calculations, 16 microstructures are created for PyMKS and SfePy calculations. $V_f^{\gamma^{\prime}}$ increases from 5\% to 80\% and the Young's moduli (Y) is decided by the mean stress and applied elastic strain. SfePy and PyMKS take 22 and 1 seconds in average to finish 1 calculation.
<img src='exam_pymks.png'>

###Plastic deformation
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

<img src='SS_850.png'>


###Optimization for high work to necking
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
<img src='opt_comp_ps.png'>
(2) Yield stress: x-processing temperature, y-Al and Cr content, wt%
<img src='opt_comp_ys.png'>
(3) Work to necking: x-processing temperature, y-Al and Cr content, wt%
<img src='opt_comp_WTN.png'>


