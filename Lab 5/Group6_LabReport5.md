```python
from aide_design.play import*
import Environmental_Processes_Analysis as EPA
import importlib
importlib.reload(EPA)
```


### Group 6 (Ben Gassaway, Christopher Galantino, Anna Lawrence,)
## Laboratory 3 Lab Report


#####1) *Use multivariable nonlinear regression to obtain the best fit between the experimental data and the two models by minimizing the sum of the squared errors. Use EPA.Solver_AD_Pe and EPA.Solver_CMFR_N. These functions will minimize the error by varying the values of average residence time, (mass of tracer/reactor volume), and either the number of CMFR in series or the Peclet number.*

```python
#CMFR Calculation for CMFR Solver
def Solver_CMFR_N(t_data, C_data, theta_guess, C_bar_guess):
file = pd.read_csv('CMFR.csv')
array = np.array(file)
#t_data : Array of times with units
t_data = array[1:133,1]*(u.sec)
#C_data : Array of tracer concentration data with units
C_data = array[1:134,2]*(u.mg/u.L)
#theta_guess : Estimate of time spent in the total reactor with units.
theta_guess =
#C_bar_guess : Estimate of (Mass of tracer)/(volume of the total reactor)
C_bar_guess =

## plotting
plt.figure()
plt.plot(time,concentration)
plt.xlabel('Hydraulic Residence Time', fontsize=15)
plt.ylabel('pH', fontsize=15)
plt.savefig('./Photos/HydraulicResTimevspH.png')
plt.show()
#AD Calculation for AD_Pe Solver_N
#def Solver_AD_Pe(t_data, C_data, theta_guess, C_bar_guess):

#t_data : Array of times with units

#C_data : Array of tracer concentration data with units

#theta_guess : Estimate of time spent in one CMFR with units.

#C_bar_guess : Estimate of (Mass of tracer)/(volume of one CMFR) with units.
```
#####2) *Generate a plot showing the experimental data as points and the model results as thin lines for each of your experiments. Explain which model fits best and discuss those results based on your expectations.*


#####3) *Compare the trends in the estimated values of N and Pe across your set of experiments. How did your chosen reactor modifications effect dispersion?*

#####4) *Report the values of $t^\star$ at F = 0.1 for each of your experiments. Do they meet your expectations?*

#####5) Evaluate whether there is any evidence of “dead volumes” or “short circuiting” in your reactor.

#####6) Make a recommendation for the design of a full scale chlorine contact tank. As part of your recommendation discuss the parameter you chose to vary as part of your experimentation and what the optimal value was determined to be.  

``` python
def CMFR_Analysis(time,concentration,Q,V,plotnumber):
  guessedtheta = (V/Q).to(u.min)
  Cbarguess = np.max(concentration)
  CMFR= EPA.Solver_CMFR_N(time, concentration, guessedtheta, Cbarguess)
  CMFR_model = CMFR.C_bar * EPA.E_CMFR_N((time/CMFR.theta).to_base_units(),CMFR.N)
  CMFRgraph = 'Reactors/images/CMFRplot'
  CMFRgraph+= plotnumber
  CMFRgraph+='.png'

  plt.plot(time.to(u.min), concentration.to(u.mg/u.L))
  plt.plot(time.to(u.min), CMFR_model,'b')
  plt.xlabel(r'$time (min)$')
  plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
  plt.legend(['Measured dye','CMFR Model'])

  plt.savefig(CMFRgraph)
  plt.show()
  print(CMFR.N)

def Baffles_Analysis(timeB,concentrationB,Q_B,V_B,plotnumber_B):

  theta_guessB = (V_B/Q_B).to(u.min)
  C_bar_guess_B = np.max(concentrationB)
  CMFR_B = EPA.Solver_CMFR_N(timeB,concentrationB,theta_guessB,C_bar_guess_B)
  CMFR_Model_B = CMFR_B.C_bar* EPA.E_CMFR_N((timeB/CMFR_B.theta).to_base_units(),CMFR_B.N)

  AD = EPA.Solver_AD_Pe(timeB, concentrationB, theta_guessB, C_bar_guess_B)
  AD_model = (AD.C_bar*EPA.E_Advective_Dispersion((timeB/AD.theta).to_base_units(), AD.Pe))

  saved = 'Reactors/images/reactorplot'
  saved+= plotnumber_B
  saved+='.png'
  plt.scatter(timeB.to(u.min), concentrationB.to(u.mg/u.L))
  plt.plot(timeB.to(u.min), CMFR_Model_B.to(u.mg/u.L),'b')
  plt.plot(timeB.to(u.min), AD_model.to(u.mg/u.L),'g')
  plt.xlabel(r'$time (min)$')
  plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
  plt.legend(['CMFR Model', 'AD Model','Measured dye'])

  plt.savefig(saved)
  plt.show()
  print(CMFR_B.N,AD.Pe)
  ```
