```python
from aide_design.play import*
import Environmental_Processes_Analysis as EPA
import importlib
importlib.reload(EPA)
```

#Lab Report 5
## Jonathan Harris, Erica Marroquin, Sung Min Kim

### Introduction
Write a paragraph on the goals of the experiment. Why did you decide to do this experiment? Introduce your approach by explaining what needs to be done to meet your goal for your real world project. Explain what you hoped to learn through this research. How did you expect this experiment to guide your decisions about the real world project that you are working on?

In nature and engineered systems, reactors are particularly important to observe chemical, biological and physical processes. Reactors are defined by a real or imaginary boundary that physically confines the processes and most experience continuous flow in and out.

The Reactors Characteristics Lab addresses the importance of knowing the mixing level and residence time in reactors, especially with regard to chlorine contact tanks. The mixing level and residence time are crucial in understanding the degree of process reaction that occurs while the fluid and its components pass through the reactor.

The goal of this lab is to experiment with different reactor designs with the design objective of maximizing the contact time. Maximizing contact time between chlorine and pathogens is essential for chlorine contact tanks and disinfection contact tanks. This report attempts to obtain accurate estimates of the effective contact time and determine hydraulic characteristics of reactors.

### Objectives
This is the section where you can present the equations that you will be using. Format the equations using Latex to create a beautiful report.

The objective of this lab is to experiment with 5 different designs (list) and analyze tracer design through measuring tracer concentration and time.

### Procedures

```python
#analysis

def CMFR_Analysis(time,concentration,Q,V,plotnumber):
  guessedtheta = (V/Q).to(u.min)
  Cbarguess = np.max(concentration)
  CMFR= EPA.Solver_CMFR_N(time, concentration, guessedtheta, Cbarguess)
  CMFR_model = CMFR.C_bar * EPA.E_CMFR_N((time/CMFR.theta).to_base_units(),CMFR.N)
  CMFRgraph = 'Reactors/CMFRplot'
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

  saved = 'Reactors/reactorplot'
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




Week1file = 'Reactors/CMFRJonathansGroup.xls'
Week2file = 'Reactors/Reactor28.xls'
Week3file = 'Reactors/Reactor37.xls'

data_file_pathCMFR = 'Reactors/CMFRJonathansGroup.xls'


#I eliminate the beginning of the data file because this is a CMFR and the first data was taken before the dye reached the sensor.
firstrowCMFR = 5
timeCMFR = EPA.ftime(data_file_pathCMFR,firstrowCMFR,-1)
CMFR_data = EPA.Column_of_data(data_file_pathCMFR,firstrowCMFR,-1,1,'mg/L')
V_CMFR = 1.5*u.L
Q_CMFR = 380 * u.mL/u.min
CMFRplotnumber = 'CMFRplot'
CMFR_Analysis(timeCMFR,CMFR_data,Q_CMFR,V_CMFR,CMFRplotnumber)
CMFR_N = 1
timeCMFR


#Baffles
#--------------------------------------------------

V_Baffles = 2*u.L
Q_Baffles = 380 * u.mL/u.min

#Week 2


w2e1time = EPA.ftime(Week2file,276,459)
w2e1dye = EPA.Column_of_data(Week2file,276,459,1,'mg/L')
w2e1plot='w2e1'
Baffles_Analysis(w2e1time,w2e1dye,Q_Baffles,V_Baffles,'w2e1')
# N = 2.8595
# Pe = 3.569

w2e2time = EPA.ftime(Week2file,631,710)
w2e2dye = EPA.Column_of_data(Week2file,631,710,1,'mg/L')
Baffles_Analysis(w2e2time,w2e2dye,Q_Baffles,V_Baffles,'w2e1')
# N = 1.436
# Pe = 0.5494
w2e3time = EPA.ftime(Week2file,1193,-1)
w2e3dye = EPA.Column_of_data(Week2file,1193,-1,1,'mg/L')
Baffles_Analysis(w2e3time,w2e3dye,Q_Baffles,V_Baffles,'w2e3')
# N = 1.3767
# Pe = 0.289

#Week 3

w3e1time=EPA.ftime(Week3file,453,589)
w3e1dye=EPA.Column_of_data(Week3file,453,589,1,'mg/L')
Baffles_Analysis(w3e1time,w3e1dye,Q_Baffles,V_Baffles,'w3e1')
# N = 1
# Pe = 8.865

w3e2time=EPA.ftime(Week3file,903,1060)
w3e2dye=EPA.Column_of_data(Week3file,903,1060,1,'mg/L')
Baffles_Analysis(w3e2time,w3e2dye,Q_Baffles,V_Baffles,'w3e2')
# N = 1
# Pe = 6.9845


plt.plot(w2e1time.to(u.min),w2e1dye.to(u.mg/u.L), label ="First Experiment")
plt.plot(w2e2time.to(u.min),w2e2dye.to(u.mg/u.L), label="Second Experiment")
plt.plot(w2e3time.to(u.min),w2e3dye.to(u.mg/u.L), label="Third Experiment")
plt.plot(w3e1time.to(u.min),w3e1dye.to(u.mg/u.L), label="Fourth Experiment")
plt.plot(w3e2time.to(u.min),w3e2dye.to(u.mg/u.L), label="Fifth Experiment")
plt.xlabel('Time (min)')
plt.ylabel('Concentration (mg/L)')
plt.legend()
#plt.savefig('Experimentsplots.png')
plt.show()
```


### Results and Discussions

1. Use multivariable nonlinear regression to obtain the best fit between the experimental E curve and model E curves by minimizing the sum of the squared errors. Minimize the error by varying the values of either N or Pe (depending on the model).
-done

2. Generate a plot showing the experimental data as points and the model results as thin lines for each of your experiments. Explain which model fits best and discuss those results based on your expectations.
-done

3. Compare the trends in the estimated values of N and Pe across your set of experiments. How did your chosen reactor modifications effect dispersion?


4. Report the values of t<super>* at F= 0.1 for each of your experiments. Do they meet your expectations?


5. Evaluate whether there is any evidence of "dead volumes" or "short circuiting" in your reactor.


6. Make a recommendation for the design of a full scale chlorine contact tank. As part of your recommendation discuss the parameter you chose to vary as part of your experimentation and what the optimal value was determine to be.

A well performing chlorine contact chamber maximizes the contact time between chlorine and pathogens in the incoming water before being distributed to consumers. The more time that water spends in the tank before distribution, the better the contact time.
