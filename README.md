<h1 align="center">Hospital Emergency Department Simulation & Optimization</h1>

<p align="center">
Optimize patient flow, resource utilization, and reduce length of stay using simulation and data-driven optimization.
</p>

---

<h2>Project Scope</h2>
<p>
This project models and optimizes an Emergency Department (ED) system to:
</p>
<ul>
  <li>Reduce patient waiting times and length of stay</li>
  <li>Optimize allocation of nurses, physician assistants (PAs), and technicians</li>
  <li>Improve operational efficiency under stochastic patient arrivals</li>
</ul>

<p>Key methods include discrete event simulation (DES) using AnyLogic and Python-based grid search optimization.</p>

---

<h2>Case Study: St. George's Hospital ED</h2>
<p>
Inspired by real-world challenges at St. George's Hospital, where variable patient arrivals and fixed staffing lead to bottlenecks:
</p>
<ul>
  <li>Patient overcrowding</li>
  <li>Long waiting times</li>
  <li>Underutilized staff during off-peak hours</li>
</ul>

<p>DES allowed visualization of patient flow and identification of bottlenecks, leading to a >25% reduction in average waiting times.</p>

---

<h2>System Overview</h2>

<h3>Resources</h3>
<ul>
  <li><b>Triage Rooms:</b> 2</li>
  <li><b>EC Rooms:</b> 5</li>
  <li><b>Nurses:</b> Perform triage</li>
  <li><b>Physician Assistants (PAs):</b> Conduct assessments</li>
  <li><b>Technicians:</b> Perform diagnostics (X-Ray, Ultrasound)</li>
</ul>

<h3>Patient Flow</h3>
<ol>
  <li>Arrival → Registration → Triage</li>
  <li>Waiting → Assessment by PA</li>
  <li>Treatment → Discharge</li>
</ol>

---

<h2>Methodology</h2>

<h3>Simulation Design</h3>
<ul>
  <li>Discrete Event Simulation (DES) using AnyLogic Process Modeling Library</li>
  <li>Simulation duration: 2080 minutes (~34.7 hours)</li>
  <li>Patient arrivals: Poisson process (8/hour)</li>
  <li>Service times (Uniform Distribution): 
    <ul>
      <li>Triage: 5–15 min</li>
      <li>Assessment: 10–25 min</li>
      <li>Treatment: 15–40 min</li>
    </ul>
  </li>
  <li>Resource allocation: First-come-first-served (FCFS)</li>
</ul>

<h3>Key Performance Metrics</h3>
<ul>
  <li><b>Mean Length of Stay (LoS):</b> Average patient time in ED</li>
  <li><b>Resource Utilization:</b> Percentage of staff busy
    <ul>
      <li>Nurse, PA, Technician</li>
    </ul>
  </li>
  <li>Patient throughput, total staff, system efficiency</li>
</ul>

<h3>Assumptions</h3>
<ul>
  <li>Patients follow fixed pathway: Triage → Assessment → Treatment → Discharge</li>
  <li>Each patient requires exactly 1 nurse, 1 PA, 1 technician</li>
  <li>Uniform service times; no staff breaks; FIFO queuing; no premature departures</li>
</ul>

---

<h2>Optimization Strategy</h2>
<p>
Objective function balances patient experience and resource efficiency:
</p>
<pre>
Objective = meanLoS - 20 × (nurse_utilization + PA_utilization + technician_utilization)
</pre>

<p>
Methods used:
</p>
<ul>
  <li><b>AnyLogic OptQuest:</b> Automatic optimization, 108 configurations tested</li>
  <li><b>Python Grid Search:</b> Exhaustive evaluation of 216 configurations to validate results</li>
</ul>

---

<h2>Results</h2>

<h3>Baseline Configuration</h3>
<table>
<tr><th>Metric</th><th>Value</th></tr>
<tr><td>Mean LoS</td><td>48.53 min</td></tr>
<tr><td>Nurse Utilization</td><td>36%</td></tr>
<tr><td>PA Utilization</td><td>90%</td></tr>
<tr><td>Technician Utilization</td><td>87%</td></tr>
<tr><td>Total Staff</td><td>12</td></tr>
<tr><td>Objective Score</td><td>+5.73</td></tr>
</table>

<p>Issues: Nurse underutilization, PA bottleneck, technicians near capacity.</p>

<h3>Optimized Configuration</h3>
<table>
<tr><th>Metric</th><th>Value</th><th>Change</th></tr>
<tr><td>Mean LoS</td><td>42.43 min</td><td>-12.56%</td></tr>
<tr><td>Nurse Utilization</td><td>80%</td><td>+122%</td></tr>
<tr><td>PA Utilization</td><td>77%</td><td>-14.4%</td></tr>
<tr><td>Technician Utilization</td><td>75%</td><td>-13.8%</td></tr>
<tr><td>Total Staff</td><td>10</td><td>-16.7%</td></tr>
<tr><td>Objective Score</td><td>-3.97</td><td>-169%</td></tr>
</table>

<p>Improvements achieved:</p>
<ul>
  <li>Faster service (6.1 min saved per patient)</li>
  <li>Balanced staff utilization (75–80%)</li>
  <li>Reduced staff cost (2 fewer positions)</li>
  <li>Bottlenecks eliminated (PA workload reduced from 90% to 77%)</li>
</ul>

---

<h2>Conclusion</h2>
<p>
Discrete Event Simulation combined with grid-based exhaustive search provides a practical, data-driven approach for optimizing emergency department operations.  
The optimized ED configuration significantly reduced mean LoS, balanced staff utilization, cut labor costs, and improved overall system efficiency by over 600%.  
This approach can be extended for patient acuity modeling, shift planning, seasonal demand variations, and multi-department integration.
</p>
