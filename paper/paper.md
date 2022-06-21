---
title: 'PyDDSBB: A Python Package for Simulation-Optimization using Data-Driven Branch-and-Bound Techniques'
tags:
  - Python
  - Data-Driven Optimization
  - Simulation Optimization
  - Multi-fidelity
authors:
  - name: Jianyuan Zhai
    orcid: 0000-0000-0000-0000
    affiliation: 1
  - name: Suryateja Ravutla
    affiliation: 1
  - name: Fani Boukouvala
    corresponding: true
    affiliation: "1, 2"
affiliations:
 - name: Department of Chemical and Biomolecular Engineering, Georgia Institute of Technology, Atlanta, GA
   index: 1
 - name: Corresponding Author
   index: 2
date: 20 June 2022
bibliography: pyddsbbJOSS.bib

---

# Summary

High-fidelity (HF) computer simulations are essential for quantitative analysis and decision-making (i.e., design or inverse optimization), however, often the objective functions and the constraints reliant on a simulation are only available as black-box functions [@McBride2019OverviewEngineering, @Rios2013Derivative-freeImplementations, @Boukouvala2016GlobalCDFO, @Bhosekar2018AdvancesReview]. Sample generation using HF simulations is often expensive due to computational cost and time. Most of the equation/derivative-based optimization solvers cannot be directly applied to optimize problems with embedded HF simulations due to lack of closed-form equations and gradient information. As an alternative, machine learning (ML) surrogate models are often employed to approximate HF simulation data and expedite the optimization search[@Bhosekar2018AdvancesReview]. However, training and building accurate models requires large amount of data model parameterizations are highly subjected to the available data.  The non-convexity of the ML models may lead to different optimal solutions upon re-initializing and slight changes in the data leads to a different surrogate model parameterizations. Finally, most derivative-free or black-box methods offer no information regarding the quality of the incumbent optimal solution (e.g., upper/lower bound on the optimum) [@Boukouvala2016GlobalCDFO, @Amaran2016SimulationApplications, @Larson2019Derivative-freeMethods, @Zhai2021Data-drivenOptimization, @Zhai2022Data-drivenOptimization]. To tackle these problems, we recently proposed a data-driven equivalent of the spatial branch-and-bound (DDSBB) algorithm based on the concept of constructing convex underestimators of HF data from simulations and low-fidelity (LF) data from ML model approximations [@Zhai2021Data-drivenOptimization, @Zhai2022Data-drivenOptimization].

# Statement of need

Black-box optimization is a challenging problem due to lack of analytic equations and derivatives. Such problems arise in many fields of science and engineering, such as chemical process design, oilfield operations, protein folding, aircract/vehicle design, and many more [@McBride2019OverviewEngineering]. Developing novel and improved data-driven approaches for efficient optimization of such systems will help in quantitative analysis and improved decision making. Although many methods exist, one drawback of many sampling- or ML-based optimization methods is the high dependency on initial sampling and selection of the ML model type. PyDDSBB is a Python package for the proposed Data-Driven Spatial Branch and Bound Algorithm[@Zhai2021Data-drivenOptimization, @Zhai2022Data-drivenOptimization]. Instead of only using samples, or directly relying on a single ML model fit, pyDDSBB develops convex underestimators as relaxations of data generated from HF models and/or ML surrogates. These relaxations are embedded into the branch and bound algorithm, and the search space is progressively partitioned by branching and pruning heuristics. This approach allows for estimation of upper and lower bounds on the optimum solution, which help in pruning spaces that have a very low probability of containing a better optimum. Samples are added adaptively in the non-pruned subspaces[@Rios2013Derivative-freeImplementations, @Zhai2021Data-drivenOptimization, @Zhai2022Data-drivenOptimization]. Through benchmarking of pyDDSBB on a large pool of problems with dimensions 1-10, we have shown that the solver can locate the global optimum for x of the problems with 2-3 dimensions and y of the problems with 4-10 dimensions. Most importantly pyDDSBB provides valid bounds for overall ~90% of the problems[@Zhai2022Data-drivenOptimization].

# Overview and Description

The PyDDSBB algorithm has been constructed using object oriented programming, with an intent of easier incorporation of further additions or extensions to the algorithm. The algorithm has the option of employing Support Vector Regression models (trained by HF data) to generate LF data that also inform the underestimators. The algorithm utilizes the Scikit-learn [@Pedregosa2011Scikit-learn:Python] package for constructing and optimizing the surrogate models for LF data generation and also offers the capability of user-based additions of new surrogate models. The algorithm utilizes the package – PYOMO[@Hart2011Pyomo:Python] to construct the convex quadratic underestimators and also provides an option for integration of other type of underestimators. Latin Hypercube Sampling (LHS) technique is used for generating the samples and the samples are generated adaptively in the non-pruned subspaces by utilizing the bounding information. An overview of the algorithm is shown in Figure \autoref{fig:MF}. While the objective function is assumed to be simulation-based (black-box), PyDDSBB allows the user to include simulation-based constraints (unknown or black-box) and equation-based (known) constraints into the formulation. A variety of branching techniques (e.g., equal bisection, longest side, ML-based prioritizing important variables, etc.) and branch-and-bound heuristics are considered, and default options are recommended for the case of box-constrained and general constrained problems. The HF simulation can be in the form of a python function, or any external platform that could be connected via an API. The ultimate goal of this software is to provide a user-friendly simulation-based optimization framework for both expert and non-expert users, benefiting from the high-level features of Python. PyDDSBB follows the object-oriented programming paradigm and is designed to allow easy extension of the core functionality by users and developers. The optimization of an example function and the visualization of the outputs in shown in Figure \autoref{fig:rO}



# Figures


![PyDDSBB overview. Solid red line shows the the HF path and dotted red line shows the path for MF approach.\label{fig:MF}](MF.jpg)
![Optimization of sample benchmark function and the visualizing the output.\label{fig:rO}](resultsOverview.jpg)

# Acknowledgements

This work was supported by.


# References





```python

```