# Network dynamics


### AmariWilsonCowan Model
With:
$$f(x)=\tanh(gx)$$
Model expression:
$$\frac{dV_i}{dt} = -\frac{V_i(t)}{\tau} +\sum_{j=1}^NJ_{ij}f(V_j(t))+\epsilon \xi_i(t)$$
Vector form
$$\frac{dV_i}{dt} = -\frac{\textbf{V(t)}}{\tau}+\textbf{J}f(\textbf{V})+\textbf{S}(t)$$
Observable:
$$m(t) = \frac{1}{N}\sum_i^N V_i$$

#### System's Jacobian $(i,k)=(row, column)$ being $Fi=F(V_i(t))$ and $\delta$ Kronecker delta:
$$\frac{\partial F_i}{\partial V_k} = -\frac{1}{\tau}\frac{\partial V_i}{\partial V_k} + \sum_{j=1}^N J_{ij}\frac{\partial f(V_j)}{V_k}$$
$$\frac{\partial F_i}{\partial V_k} = -\frac{\delta{ik}}{\tau} + \sum_{j=1}^N J_{ij} f'(V_j)\frac{\partial f(V_i)}{V_k}$$
$$\frac{\partial F_i}{\partial V_k} = -\frac{\delta{ik}}{\tau} + \sum_{j=1}^N J_{ij} f'(V_j)\delta{jk}$$
$$\frac{\partial F_i}{\partial V_k} = -\frac{\delta{ik}}{\tau} +J_{ik}f'(V_k)$$
$$f'(x) = \tanh(gx) = g(1-\tanh^2(gx))$$

Given that $J_{ii} \forall i = 0$, the Jacobian matrix is:
$$\frac{\partial F_i}{\partial V_k} = -\frac{\delta{ij}}{\tau} +J_{ik}g(1-\tanh^2(gV_k))$$

Matrix form:
$$\Lambda(V)_{ik} = f'(V_k)\delta_{ik} \rightarrow \Lambda(V) = \text{Diag}(g*(1-\tanh^2(gV)))$$
$$DF_V = \frac{-\textbf(I_N)}{\tau} + J\Lambda(V)$$
#### Prelude to susceptibility

Adding a perturbation $\xi$ of $\omega$ frequency, to the simulation with $\epsilon ~ 10^{-2}$
2 Cases are needed, $V^{(*)}$ represents the potential with the $\xi$ replaced.
$$V^{(1)} = \xi_i(t) = \xi_i^{(1)}(t) = \imath\cos(\omega t) \delta_{ii_0} $$
$$V^{(2)} = \xi_i(t) = \xi_i^{(2)}(t) = -\sin(\omega t)\delta_{ii_0} $$

#### Obtaining the Susceptibility matrix $\chi$:
$$\chi_{ii_0} = \frac{1}{\tau\epsilon} \sum_{t=0}^Te^{\imath\omega t}[V_{i}^{(1)}(t) + \imath V_i^{2}(t)] $$
$$\chi_{ii_0}(\omega) = \chi_{ii_0}^{(r)}(\omega) + \imath \chi_{ii_0}^{(\imath)}(\omega) \rightarrow |\chi_{ii_0}(\omega)|^2$$

Expected results for a fixed $i,i_0$ and variable $\omega$:
* Peak of FFT of susceptibility on the $\omega$ frequency with varying amplitude based on the node selected.

Conditions:
* Periodical system status

# TODO
### Notes
* Use the J matrix "J2" for tests with the g parameter being (0.15 **P**eriodic | 0.45 **Q**uasi **P**eriodic | 0.8 **C**haotic)
## Lyapunov
* Find a viable code
* Show the spectrum (3-5 coefs) as a function of g
* Ideal plot: lyapunovs v/s g (long) and 4 attractors (columns) below each with M and fft with shared X
## FFT
* Compute and save the FTT for each state, with high T for better resolution (Crop at 50Hz)
## Chi Matrix $\chi$
* Compute and save the $\chi$ matrix with a finer $\omega$ resolution to match FTT plot.
* Compare the peaks obtained (Expected: P and QP to be same peaks and extra peaks from $\chi$ in C)
* Compute the matrix $C$ (Correlations between FTT's) from FTT without stimulus and compare to $\chi$
