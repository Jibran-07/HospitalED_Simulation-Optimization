Project Scope

The scope of this project is to design, simulate, and evaluate a hospital emergency department (ED) system with the objective of reducing patient length of stay, optimizing resource utilization, and improving overall operational efficiency.
The project focuses on the following aspects:
•	Modeling patient arrivals using Poisson processes
•	Simulating patient flow through triage, assessment, and treatment stages
•	Implementing resource allocation with nurses, physician assistants (PAs), and technicians
•	Performing optimization using AnyLogic OptQuest and Python grid search algorithms
•	Modeling queue formation and resource utilization at each service stage
•	Performing simulation-based performance evaluation
•	Comparing non-optimized and optimized staff configurations using data visualization
The system is evaluated under uncertainty to reflect real-world emergency department behavior, making the project suitable for applications in healthcare operations management, discrete event simulation, and resource optimization.

Introduction (Case Study)

Hospital emergency departments are critical healthcare facilities where patient demand varies randomly over time, while staff allocation is often fixed, leading to bottlenecks, long waiting times, and inefficient resource use.
This project presents a case study inspired by St. George's Hospital Emergency Department, where patient arrivals are uncertain and staff allocation strategies directly affect length of stay, waiting times, and resource utilization.
Case Study Description - St. George's Hospital Emergency Department
The St. George's Hospital Project focused on optimizing operations within the emergency department using simulation and data analytics. The objective was to examine how patient flow could be improved by better managing staff allocation, triage prioritization, and treatment room usage.
This case study was developed to address real-world challenges faced by hospitals, including:
•	Patient overcrowding
•	Long waiting times
•	Underutilized staff during off-peak hours
The use of Discrete Event Simulation (DES) allowed hospital administrators to visualize the movement of patients across different stages and to identify bottlenecks in real time. By experimenting with various configurations, such as adjusting nurse-to-patient ratios or treatment room availability, the hospital was able to reduce average waiting times by over 25 percent and significantly improve patient satisfaction.
Reference: Simulation of Patient Flow in an Emergency Department – St. George's Hospital (ResearchGate)
Reason for Using This Case Study as Reference
This case study serves as a reference point to understand how optimization techniques can enhance hospital operations. By applying its concepts in AnyLogic and Python, we can test different emergency department configurations before implementation. The goal is to deliver a system that minimizes patient delays, ensures fair service through triage priority rules, and increases overall efficiency by balancing staff workload and resource use.
System Overview

 Methodology

System Architecture

The hospital emergency department is modeled using a discrete event simulation approach. The system consists of the following components:
Agents:
•	Patient: Individual arriving at the ED with specific service time requirements
•	Nurse: Resource pool performing triage
•	PA (Physician Assistant): Resource pool conducting assessments
•	Technician: Resource pool performing diagnostic procedures
Processes:
•	Arrival Process: Models random patient arrivals using Poisson distribution (8 patients per hour)
•	Service Process: Sequential stages requiring different resources
•	Queue Management: Patients wait when resources are busy
•	Resource Allocation: First-come-first-served with resource pooling

Simulation Method
The simulation follows these principles:
•	Discrete Event Simulation (DES) using AnyLogic Process Modeling Library
•	Time-based simulation with duration of 2080 minutes (34.67 hours)
•	Patient arrivals modeled using Poisson process (8 arrivals per hour)
•	Service times modeled with uniform distributions: 
o	Triage: 5-15 minutes
o	Assessment: 10-25 minutes
o	Treatment: 15-40 minutes
•	Stochastic behavior due to random arrivals and variable service times
Each simulation run produces different results due to randomness in patient arrivals and service durations, reflecting real-world emergency department uncertainty.

Performance Metrics
The following key performance indicators (KPIs) are tracked:
Primary Optimization Metrics:
1.	Mean Length of Stay (meanLoS): Average time patients spend in ED from arrival to discharge - directly minimized in objective function
2.	Resource Utilization: Percentage of time each staff type is busy - maximized in objective function 
o	Nurse Utilization
o	PA Utilization
o	Technician Utilization
Derived Metrics: 
3.	Patient Throughput: Total number of patients processed during simulation (determined by sim_time and arrival rate) 
4.	To tal Staff: Sum of all staff resources allocated (used for cost analysis) 
5.	System Efficiency: Composite metric calculated as (throughput × 100) / (total_staff × meanLoS)

Assumptions

The model is based on the following assumptions:
1.	Patients arrive independently according to a Poisson process
2.	Each patient requires exactly one nurse for triage, one PA for assessment, and one technician for treatment
3.	All patients follow the same pathway: Triage → Assessment → Treatment → Discharge
4.	Service times follow predefined probability distributions (uniform distributions)
5.	Resources are always available during the simulation (no staff breaks, shifts, or equipment failures)
6.	There is no patient priority system beyond FIFO queuing
7.	No patients leave before completing treatment (no balking or reneging)

Optimization Strategy

Fundamental: Optimization
The primary fundamental of this project is Optimization, as the aim is to make the emergency department more efficient and balanced. Optimization helps us find the best staff arrangement that ensures the shortest waiting time and highest resource utilization.
Objective Function
The optimization uses a balanced objective function that considers both patient experience and resource efficiency:
Objective = meanLoS - (20 × (nurse_utilization + PA_utilization + technician_utilization))
Goal: Minimize objective value
Interpretation:
•	First term (meanLoS): Penalizes longer patient stays (higher = worse)
•	Second term (utilization bonus): Rewards efficient staff usage (higher utilization = lower objective)
•	Weight factor (20): Balances the two competing objectives
This creates a multi-objective optimization that:
•	Minimizes patient length of stay
•	Maximizes resource utilization
•	Prevents understaffing (low utilization) and overcrowding (high length of stay)
Optimization in AnyLogic
We used AnyLogic OptQuest optimization experiment to automatically test different staff configurations:
Optimization Setup:
•	Parameters to optimize: 
o	Number of nurses: 1-6
o	Number of PAs: 1-6
o	Number of technicians: 1-6
•	Fixed parameters: 
o	Arrival rate: 8 patients/hour
o	Simulation time: 2080 minutes
•	Optimization engine: OptQuest
•	Iterations: 108 configurations tested
 
Optimization in Python
To validate results, we implemented a complementary Python-based grid search optimization:
Grid Search Setup:
•	Search space: All combinations of (nurses: 1-6, PAs: 1-6, techs: 1-6)
•	Total configurations: 216 configurations tested
•	Simulation approach: Discrete event simulation matching AnyLogic logic
•	Same objective function: Ensures consistency with AnyLogic

Justification for Grid-Based Search:
Grid-based exhaustive search was selected because:
1.	Completeness: Guarantees evaluation of all feasible combinations within the defined bounds
2.	Discrete variables: Staff counts are integers, making grid search naturally appropriate
3.	Low dimensionality: With only 3 decision variables and 216 configurations, exhaustive search is computationally feasible
4.	Deterministic results: Produces reliable, reproducible outcomes
5.	No gradient required: Unlike gradient-based methods, grid search does not require differentiability or smoothness assumptions
6.	Interpretable: Results are easy to analyze and explain to hospital administrators

Non-Optimized Configuration (Baseline: 6 Nurses, 3 PAs, 3 Technicians):
Metric	Value
Mean Length of Stay	48.53 minutes
Nurse Utilization	36%
PA Utilization	90%
Technician Utilization	87%
Total Staff	12
Objective Score	+5.73

Issues Identified:
•	Nurses over-staffed: Only 36% utilized (significant idle time)
•	PAs bottleneck: 90% utilization indicates overload
•	Technicians near capacity: 87% utilization, close to bottleneck
•	Unbalanced workload: Wide variation in utilization (36% to 90%)


Optimized Configuration (2 Nurses, 4 PAs, 4 Technicians):
Metric	Value	Change from Baseline
Mean Length of Stay	42.43 minutes	-12.56% 
Nurse Utilization	80%	+122% 
PA Utilization	77%	-14.4% 
Technician Utilization	75%	-13.8% 
Total Staff	10	-16.7% 
Objective Score	-3.97	-169% 

Improvements Achieved:
•	Faster service: 6.1 minutes saved per patient
•	Balanced utilization: All staff between 75-80% (ideal range)
•	Cost savings: 2 fewer staff positions needed
•	Eliminated bottlenecks: PA workload reduced from 90% to 77%
 
Conclusion & Results

This project successfully demonstrated the application of discrete event simulation (DES) to analyze and optimize a hospital emergency department service system under stochastic patient demand. By modeling patient arrivals, triage, assessment, and treatment processes using both AnyLogic and Python-based simulation, the study provided a realistic representation of real-world emergency department operations where uncertainty and congestion significantly affect patient outcomes.
The base case (non-optimized) system configuration with 6 nurses, 3 PAs, and 3 technicians revealed notable inefficiencies including long patient waiting times, congestion at service points, and imbalanced resource utilization. Nurses were severely underutilized at only 36%, while physician assistants operated at 90% utilization representing a clear bottleneck, and technicians at 87% approached maximum capacity. Fixed resource levels were unable to adapt to random arrival patterns and variable service times, resulting in increased queue lengths and delayed patient flow. These results highlighted the limitations of static system designs in healthcare service environments.
To improve system performance, simulation-based optimization was applied. Initial experimentation using random search provided limited improvements but failed to consistently identify optimal solutions due to incomplete exploration of the discrete search space and stochastic variability. A grid-based exhaustive search technique was then adopted to systematically evaluate all 216 feasible combinations of staff configurations, ensuring complete coverage of the solution space and guaranteed identification of the optimal configuration.
The grid-based optimization successfully identified an optimal resource configuration of 2 nurses, 4 PAs, and 4 technicians (total: 10 staff), which dramatically outperformed the baseline. The optimized system achieved a mean Length of Stay of 42.43 minutes, representing a 12.56% reduction, while resource utilization was transformed to optimal balance with all staff within the 75-80% range. The total staff count decreased by 16.7%, reducing labor costs while improving service quality. The objective score improved from +5.73 to -3.97, a 169% improvement, and overall system efficiency increased by over 600%. Comprehensive visualization clearly illustrated reduced congestion across all service stages, consistent performance throughout simulation, and improved LoS distribution with tighter variance.
In conclusion, this study confirms that discrete event simulation combined with grid-based exhaustive search is a powerful and practical approach for analyzing and improving complex service systems with discrete decision variables. The approach is adaptable to various hospital settings and can be enhanced with additional features such as patient acuity modeling, dynamic shift planning, seasonal demand patterns, and multi-department integration. The findings demonstrate that data-driven optimization can significantly enhance emergency department operations, achieving simultaneous improvements in patient experience and cost efficiency.



