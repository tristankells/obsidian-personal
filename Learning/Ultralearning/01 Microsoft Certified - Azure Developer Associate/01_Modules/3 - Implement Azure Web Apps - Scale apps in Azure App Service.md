# Summary
In this module you will...
- Identify the uses cases for Azure App Service autoscaling.
- Create autoscaling rules for Azure App Service.
- Monitor the effects of autoscaling.
# Links
# Module assessment
> [!question] Question 1
> Which of these statements best describes autoscaling?
> - Autoscaling requires an administrator to actively monitor the workload on a system.
> - Autoscaling is a scale out/scale in solution.
> - Scaling up/scale down provides better availability than autoscaling.
> 
> > [!success]- Answer
> > Autoscaling is a scale out/scale in solution.

> [!question] Question 2
> Which of these scenarios is a suitable candidate for autoscaling?
> - The number of users requiring access to an application varies according to a regular schedule.
> - The system is subject to a sudden influx of requests that grinds your system to a halt.
> - Your organization is running a promotion and expects to see increased traffic to their web site for the next couple of weeks.
> 
> > [!success]- Answer
> > The number of users requiring access to an application varies according to a regular schedule.
# Notes
-  App Service Plan
	- Instance limit
		- ...no scaling on Free
- 2 Methods
	- Not free... >= Standard.
	- Azure _autoscale_.
		- Rules.
			- Metrics
				- CPU
				- Memory
				- Disk Queue
				- HTTP Queue
				- Incoming Bytes
				- Outgoing Bytes
				- Collection
					- Time Grain
						- Stats captured over time
					- Duration
						- Condition true for the time trigger scale.
			- Time Based
			- Conditions -> Multiple Rules
				- Scale In
					- + all rules met
				- Scale Out
					- + single rule met
		- Schedule Based
		- No maximum.
	- Azure App Service _automatic scaling_.
		- NO Complex Rules
			- HTTP Calls.
		- Prewarmed
		- Set a maximum.
- "Scale in / scale out"
	- Increase replicas.
- "Scale up / scale down"
	- Increase CPU size.
- Monitor
	- *Run History* tab
		- How many instances?
		- Which rule?
	- Activity Log
		- 
- Best practice
	- Min != max
	- Correct statistics
		- Probably just average.
	- Careful consideration to avoid flapping
	- Safe minimum
		- Metrics might go down.
# Flashcards
Q: What is a "scale in/scale out" solution?
A: Increase the number of replicas.
Q: What is a "scale up / scale down" solution?
A: Increase resources on the machines.
Q: Under which conditions should you prefer a "scale in/scale out" solution?
A: If your services have intermittent traffic (more on holidays), "scale in/scale out" provides eleacity to save on running compute.
Q: Give one example for why you might prefer Azure App Service automatic scaling over Azure Autoscale?
A:   
- Don't want to setup resource based rules
- Rely on separately scaling backend, need to set maximum
- Apps in the same plan scale independently. 
Q: Name 4 of the metrics you can use in your rules for Azure Autoscale?
A: 				
- CPU
- Memory
- Disk Queue
- HTTP Queue
- Incoming Bytes
- Outgoing Bytes
# 🛠 Practice Exercises
**Objective:** Understand and configure autoscale settings for an Azure App Service to automatically adjust capacity based on performance metrics or a schedule.
**Note:** Autoscaling is available on Standard tier or higher, so this may incur costs.

- [ ] **1. Metric-Based Scaling:**
    - [ ] **Goal:** Configure an App Service to scale out when CPU usage is high and scale back in when it's low.
    - [ ] Deploy a simple web app to an App Service Plan (Standard tier or above).
    - [ ] In the App Service, navigate to the "Scale out (App Service plan)" settings.
    - [ ] Create a new autoscale rule based on a metric.
    - [ ] **Scale-out rule:** If "CPU Percentage" is greater than 70% for 10 minutes, increase the instance count by 1.
    - [ ] **Scale-in rule:** If "CPU Percentage" is less than 30% for 10 minutes, decrease the instance count by 1.
    - [ ] Set the minimum and maximum instance counts (e.g., min: 1, max: 4).
    - [ ] **(Optional)** Use a load testing tool (like Azure Load Testing or a simple script) to generate traffic and trigger the scale-out rule. Monitor the "Run history" to see the scaling events.
- [ ] **2. Schedule-Based Scaling:**
    - [ ] **Goal:** Configure the App Service to have more instances during peak business hours and fewer instances overnight and on weekends.
    - [ ] In the autoscale settings, create a new scale condition with a specific schedule.
    - [ ] **Weekday Schedule:** For Monday to Friday, from 9:00 AM to 5:00 PM, set the instance count to a minimum of 2.
    - [ ] **Default Schedule:** For all other times, let the instance count default to 1.
    - [ ] This demonstrates how to prepare for predictable traffic patterns without relying on metrics.
- [ ] **3. Avoid "Flapping":**
    - [ ] **Goal:** Understand and prevent rapid scaling in and out.
    - [ ] Review your metric-based rules. Notice that the scale-out threshold (70%) and scale-in threshold (30%) are far apart.
    - [ ] Consider what would happen if the thresholds were very close (e.g., scale out at 70%, scale in at 65%). The system could "flap" by constantly adding and removing instances. This exercise is to recognize the importance of having a significant margin between scale-out and scale-in rules.