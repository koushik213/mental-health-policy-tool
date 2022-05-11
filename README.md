# Mental Health Policy Dashboard and Prediction Tool

### Link to Application/Dashboard: https://policy-pandas-web-app.herokuapp.com/

## Project Goals 
* Develop a self-service tool that policymakers and health agencies can use to identify factors that are affecting mental health in their county/state
* Help county officials adopt a data-driven approach towards implementing new policies and allocating funding/resources 

## Business Background

Alleghany County has a $109M budget for mental health resources each year. Many of these resources are used for early education about mental health or crisis intervention and treatment (Allegheny County Department of Human Services, 2019). But, are we certain that this budget is having an impact on the local community Research shows that there is an implementation gap for mental health policies where many individuals are not getting the help they need (Campion, 2018). This is one of the biggest challenges faced in improving public mental health. This is often due to a lack of local assessments conducted to identify local areas that suffer from the implementation gap. Therefore, the business problem we address is the ability to identify counties in the United States that are lagging in quality of mental health and identify key factors that contribute to their mental health levels. Our solution aims to help county officials prioritize mental health policies to make the necessary allocation and funding of health care resources that will improve their county’s gap in mental health. Our anticipated clients are county health officials in the United States. They are in the public health domain. They will be able to use our solution to compare their county to national averages and understand which areas are negatively impacting their county’s mental health. In addition, we expect our solution to contribute to public health knowledge for citizens concerned with the domain as a secondary outcome.

## Scope
* Solution - The data science solution we build will provide the following features:
  * Identify top health factors that impact mental health
  * Compare the factors to the national averages
  * Provide recommendations for county improvement areas

County officials will utilize these insights from our solution to drive positive changes in different counties and improve the overall mental health of the county.

* Project Activities - The project follows practices from CRISP-DM and Agile. Developed a data science solution for the business problem using Python’s data science libraries and deploy the solutions to Heroku (PaaS) as a web application using Tableau’s user-friendly visual presentations.
* Customer Channels - The customers will be able to access the solution through the Internet browser.


## Metrics
To measure the success of the project, we have defined both quantifiable and qualitative objectives.

* Quantifiable Objectives - The “mental health distress index” (0-1 range) is the primary indicator of the general mental health status of a county. A high value of this metric indicates that there is high mental distress in a particular county. This value will be our leading indicator to understand if policies developed from our product’s recommendations are, in fact, helping to reduce mental health distress in the county.
* Qualitative Objectives - The mental health distress index is driven by certain underlying health-related factors that we can uncover using exploratory data analysis and machine learning techniques. Identifying these top factors that contribute to driving the mental health distress index is essential in identifying the focus areas for implementing new policies to improve mental health at a county and state level.

The objective of the new policies implemented after identifying the top contributors to mental health is to reduce the mental health distress in a county. Observing a statistically significant decrease in the mental health distress index value prior to implementing new policies and observing the change in the mental health distress index over a time frame suggests that the implemented policies are effective. 

To measure the success of the policies, we plan to record the mental health distress values at a particular date as a baseline and re-evaluate the metric after policies have been implemented after a 6-month timeframe.

## Product Architecture

* Data Collection and Storage - The raw health factor values are collected from health providers in the form of comma-separated value (.csv) files and stored on premise.
* Data Transformation and Wrangling - Python libraries will be used for feature engineering, data aggregation, and exploratory data analysis to produce a final clean dataset. In particular, we will use the Pandas, NumPy, and SciPy libraries.
* Modeling - Again, python libraries will be used to build a prediction model and identify important features. In particular, the machine learning libraries Sklearn and Imblearn will be used.
* Business Intelligence Tool - The model will be connected to the visual analytics tool Tableau which will enable stakeholders to conduct self-serve analyses and arrive at data-driven policy decisions. Tableau will be embedded into our application.
* Deploying - Our model and Tableau-integrated app will be deployed to a Heroku server. The app will call the model and display the values in the Tableau dashboard.
* Customer Using the Product - Decision-makers will use the business intelligence tool to observe trends and narrow down the top contributors to mental distress in their respective communities to implement policy changes.

## Customer Benefits
Uncovering information on mental health levels and their contributing factors will help county officials prioritize mental health policies and allocate funding towards resources that will address the core factors impacting mental health. Our core metric to track the success is the change in the mental health distress level of a county over time. This metric will be impacted by new policies that are put in place by the policymakers who use the dashboard and prediction tool. While at this time it can not be quantified exactly the impact that our tool will have on mental distress, we can be certain that it will help save time in budget planning and allocation. We hope to see the impact of this tool within counties over the next year and see a significant decrease in mental health distress nationwide based due to more target policies and better allocated mental health resources.

## Project Learnings
This project was the first time our project team worked to operationalize a data science model. With the
first-time doing anything, there are many learnings which are listed below.

### Data Science/Engineering
* Build a lightweight model - Our model fits on training data when the web service is first loaded. Our first iteration of the model included some heavy cleaning and transformation tasks that caused issues when deploying the model to Heroku, which has some restrictions (detailed in the next bullet point). We learned that we need to connect as much cleaning and training prior to hosting the model to ensure that the production runs smooth and quickly for the user to get a prediction response.
* Deploying to Heroku - We faced challenges running the model on Heroku though it successfully ran locally within a virtual environment. As a result of research, we found that Heroku has the following rules: (1) a web process of Heroku, called “web dyno,” has to be launched within 60 seconds, and (2) web dyno has to respond to an HTTP request within 30 seconds. If the conditions are not met, Heroku forcibly kills the process and retries it, leading to repeated failure of the same process. In our design, data preparation and model training are coupled with starting a web dyno, and model prediction is coupled with the web dyno’s response to an HTTP request. Since our original model was relatively heavy, we breached the timeframe above, and the processes never got completed. To overcome these challenges, we made the model lighter to complete the web dyno’s processes within the timeframe. In addition, we found that Heroku runs two web dynos as default to secure redundancy, making the processes further heavier by performing data preparation, model training, and model prediction twice. Therefore, we changed the configuration so that Heroku runs only one web dyno. Our current design is acceptable as MVP but may not be scalable enough to be a production system. To address the bottleneck, we will need to decouple data preparation, model training, and model prediction from web dyno’s starting and response processes in the future. We can realize such design by making them back-end processes using a queuing mechanism.

* Staging/Integration - Our current pipeline does not benefit from a staging environment to test integration with the environment and get user feedback. We believe adding a staging environment would ensure smoother deployments to production and enable continuous delivery.

### Product
* Understand the customer - At the start of the project, we had a hard time understanding the goal. Discussing directly with the customer and conducting customer interviews would have helped to clarify the goal and gather user requirements.
* Visualize the flow - When discussing different product flows or software architectures, we found that it was useful to visualize the flow to ensure that the team was on the same page. We made use of Whimsical to build flow diagrams and wireframes to experiment with possible scenarios and draft dashboard designs before implementing them into the product.

## Next Steps

We hope this is not the end of this project. In the next steps, we plan to complete the following tasks.
* Testing & Feedback: Put our product in the hands of county officials to gather customer feedback and implement recommendations into further iterations of the product.
* Measure: Quantify the impact of our product overtime to ensure the continued investment in the project will deliver value to the counties and achieve project goals.
* Expand: Research possible expansion of the project into other domains. Potentially in education or transportation, where we can measure a county’s quality index and recommend factors to focus better on their budget and resources.

Overall, this is just the start of the project. We hope to see a quantifiable impact in a reduction of mental health distress at a county level within the next few years.

### References: 
* Allegheny County Department of Human Services. (2019). DHS Office of Behavioral Health.
  * https://www.alleghenycountyanalytics.us/wp-content/uploads/2020/08/Office-Profiles-OBH-2020.pdf
* Campion J. (2018). Public mental health: key challenges and opportunities. BJPsych Int.
  * https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6690256/
