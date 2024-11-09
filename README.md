# CH5150: Optimization Techniques I

This project explores solving optimization problems for chemical engineering applications using deterministic and evolutionary algorithms.

## Problem 1 : Determining rate constants

The system involves parallel reactions happening in an isothermal batch reactor. The rate equations need to be solved to determine the rate constants k1 and k2. I lost the data for this problem but the data contained time, concentration of components CA, CB, and CC.


<p align=center>$\ce{A ->[k1] B}$

<p align=center>$\ce{A ->[k2] C}$

Rate equations:

<p align=center>$\frac{dC_{A}}{dt} = -(k_{1}C_{A} + k_{2}C_{A})$

<p align=center>$\frac{dC_{B}}{dt} = k_{1}C_{A}$

<p align=center>$\frac{dC_{C}}{dt} = k_{2}C_{A}$

This problem utilizes the following python libraries:

    import numpy # to do math
    import pandas # to import data
    import scipy # for scipy.integrate and scipy.optimize
    import timeit # for comparing runtimes

### Algorithms Used

* Nelder-Mead Method
* Powell Method
* Conjugate Gradient Method (CG)
* BFGS Method (Broyden-Fletcher-Goldfarb-Shanno)
* COBYLA Method (Constrained Optimization BY Linear Approximations)
* SLSQP Method (Sequential Least SQuares Programming)

### Results

| Method     | Convergence     | k1_opt             | k2_opt             | Error              | Execution Time  |
|------------|-----------------|--------------------|--------------------|--------------------|-----------------|
| Nelder-Mead| Converged       | 1.9998748692788715 | 3.9997615838621496 | 1.962460e-05       | 0.149742        |
| Powell     | Converged       | 1.9999018222782379 | 3.999807785445786  | 1.954439e-05       | 0.304135        |
| CG         | Did not converge| 1.9999017781607618 | 3.9998076688535855 | 1.954439e-05       | 0.846164        |
| BFGS       | Did not converge| 1.9999018263820614 | 3.9998077521324666 | 1.954439e-05       | 0.508273        |
| TNC        | Did not converge| 1.9857536272294474 | 3.9316821455453663 | 3.748240e-03       | 0.775833        |
| COBYLA     | Converged       | 1.9994226343894554 | 3.9990020736425738 | 3.684053e-05       | 0.258513        |
| SLSQP      | Converged       | 1.9998997663393545 | 3.999809061609218  | 1.954768e-05       | 0.132066        |


## Problem 2 : Himmelblau function optimization

Minimize the Himmelblau function:

<p align=center>$\min_{x, y} (x_{1}^2 + x_{2} - 11)^2 + (x_{1} + x_{2}^2 - 7)^2$

Subject to the constraint:

<p align=center>$x_{1}^2 + x_{2}^2 \geq 25$

With bounds on \( x_1 \) and \( x_2 \):

<p align=center>$-5 \leq x_{1}, x_{2} \leq 5$

### Algorithms

This problem utilizes the following python libraries:

    import numpy # to do math
    import scipy # for deterministic algorithms

    !pip install deap
    import deap # for genetic algorithms

Three deterministic optimization algorithms are implemented:

* Gradient Descent (using BFGS method)
* Nelder-Mead Method
* CG Method

Three variants of the genetic algorithms are explored

* eaSimple
* eaMuPlusLambda
* eaMuCommaLambda

### Results


| Method          | x1_opt       | x2_opt      | Minimum Value          |
|-----------------|--------------|-------------|------------------------|
| Gradient Descent| -3.779310265 | -3.283186   | 1.4142791614207676e-15 |
| Nelder-Mead     | -3.77929277  | -3.2832138  | 6.563218571685403e-08  |
| CG              | -3.77931029  | -3.28318601 | 5.833980405874394e-14  |
| eaSimple        | -3.779310253414729  | -3.2831859914210866 | 7.416028657579182e-19  |
| eaMuPlusLambda  | -3.779310253489113  | -3.2831859912216483 | 1.1076340901563927e-18 |
| eaMuCommaLambda | -3.779310253377747  | -3.283185991286169  | 7.888609052210118e-31  |

Genetic algorithms are far superior compared to deterministic methods and produce highly optmized solutions.

