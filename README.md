# ThermalAI
"Machine Learning for Smarter Alarm Systems in Thermal Power Plants."
**Enhancing Alarm Management in a Thermal Power Plant Through Machine Learning**

**Introduction**

Thermal power plants are critical to global energy production, but their complex operations often lead to challenges in managing alarm systems. On a typical day in 2023, a thermal power plant in Southeast Asia experienced a sudden surge in alarms, overwhelming operators and threatening plant stability. This case study explores how machine learning was used to address alarm flooding and improve operational efficiency.

**Problem Statement**

Thermal power plants rely on Distributed Control Systems (DCS) to monitor and control equipment such as boilers, turbines, and condensers. However, minor deviations in process parameters (e.g., temperature, pressure, or steam flow) can trigger a flood of alarms, many of which are repetitive or non-critical. On the day in question, the plant experienced over **700 alarms** in a 24-hour period, with only **40 unique alarms**. Operators struggled to prioritize critical issues, leading to delayed responses and potential equipment damage.

The key challenges were:

1. **Alarm Flooding**: Hundreds of alarms triggered simultaneously, overwhelming operators.
2. **Chattering Alarms**: Repetitive alarms distracted operators from addressing critical issues.
3. **Downtime Risk**: Delayed responses to critical alarms increased the risk of plant downtime and financial losses.

 In this project, we evaluated KNN, Logistic Regression, and Decision Trees to predict critical alarms in a thermal power plant. While KNN achieved the highest accuracy (91%), Logistic Regression had a lower false negative rate (0.16), making it the better choice for minimizing risks in high-stakes environments. Learn more in the [analysis](/analysis) folder.
