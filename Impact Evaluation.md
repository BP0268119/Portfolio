# Impact Evaluation 

## Executive Summary

The aim of this report is to demonstrate the impact that a piece of my work has had on my organisation. It exhibits some of the skills I have developed as a result of my learning on my Data Science apprenticeship. The piece I have selected is the creation of a dashboard which shows customers who have changed their contact details, called ‘Retailer Destination Number Changes’. 

The overall impact this work has had includes improved data quality and traceability for auditing purposes, a more streamlined process which has significantly reduced toil, enhanced insight into our customers’ behaviours, improved trust from consumers and reduced financial and reputational risk. 

## Project Background

The project was a result of a request raised by the Data Governance (DG) team because a concerning pattern of behaviour had been observed: customers who had yet to pay their bills, or who had been previously had their contract terminated by the organisation, were signing up for our services using false contact details to avoid being rejected or chased about their unpaid bills. Once they were signed up under these false details, they would then change those details back to their genuine contacts. 

This behaviour posed a financial and reputational risk to the organisation, as we aim to be a highly trusted and responsible organisation, which is only possible if those who sign up for our services are reputable and reliable. Therefore, addressing this issue was an urgent business priority. 

The project aimed to address several business challenges:

### Data Quality:
Initially, the DG team were manually searching through inconsistent and incomplete data, which reduced their capacity to find the offending customers as it was a long and laborious process, which also took time away from their other tasks. 

### Data Accessibility:
Data was siloed in various systems, making it challenging for teams to access and use data effectively.

### Analytics Efficiency:
The lack of streamlined data processes led to inefficiencies in the DG team’s workflows.

## Approach

### Data Infrastructure & Tools

#### Data Warehouse Implementation: 
Using DBT (data build tool), I built the structure (and accompanying) documentation to house the incoming data in a centralised data warehouse using cloud-based infrastructure (Google Cloud Platform), providing a single place for storing and accessing data.

#### ETL Pipeline: 
Developed an ETL (extract, transform, load) pipeline to ensure data from disparate sources (several different tables and internal applications) were cleaned, transformed, and loaded into the data warehouse.

#### Data Governance:
Implemented data governance policies and procedures to maintain data quality and consistency. The information being handled was personal identified information (PII), and so specific access requirements had to be applied and regular meetings with the DG team were arranged to ensure compliance with data governance and the Data Protection Act. 

### Data Engineering

#### Automation: 
Automated the ETL pipeline using Apache Airflow – a software which allows pipelines to be ran automatically – so that the data ingestion and transformations were ran automatically every day.

#### Scalability: 
The infrastructure and pipeline were built in such a way that they will be able to handle different amounts of data each day, and so will be able to scale with a growing data volume.

### Data Visualisation

#### Dashboard Development: 
Created a dashboard in Looker which met the strict requirements of the DG team and complied with data governance. It was designed to be functional and to produce reports.

#### Ad-Hoc Analysis: 
The dashboard had filters available (e.g., type of customer, how many days’ worth of data) so that users could explore and utilise the data themselves to perform ad-hoc analyses. 



