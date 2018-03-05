## Benjamin Gassaway
<div class="alert alert-block alert-info">
Grade: 0.9/1
</div>
Prelab Question Form for Lab 3: Acid Rain

Question:

1. How many grams of NaHCO3 would be required to keep the ANC levels in a lake above 50 µeq/L for 3 hydraulic residence times given an influent pH of 3.0 and a lake volume of 4 L, if the current lake ANC is 0 µeq/L?

Given:

  1. 50 µeq/L
  2. 3 residence times (theta)
  3. pH = 3.0
  4. Volume (V) = 4L
  5. ANCo = 0 µeq/L

Solution:

ANCo = [ANCout - ANCin (1-e^-(t/theta)]e^(t/theta)

ANCout = 0.00005, ANCin = -0.001

theta = 3, t = 1

ANCo = [0.00005 - (-0.001)(1-(e^-3))]e^3 = 20.0898 meq/L

[NaHCO3]o = ANCo = (20.0898 meq/L) * (84 mg/mmol) * 4L = 6750.17 mg

<div class="alert alert-block alert-danger">
Good job! Answer in gram (unit) was expected, but this is fine. Please check your significant figures next time. And try to do your prelab in python codes. 
</div>
