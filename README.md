# Company App: Azure Static Web Apps + Google Apps Script Integration

This repository demonstrates a serverless solution for a company application that integrates Azure Static Web Apps with a Google Apps Script function and Google Sheets for data storage and email notifications. The system collects user data via Quote and Contact forms and processes submissions using a serverless function, all while operating within free-tier limits.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Setup and Configuration](#setup-and-configuration)
  - [GitHub Repository](#github-repository)
  - [Google Apps Script Configuration](#google-apps-script-configuration)
  - [Google Sheets Setup](#google-sheets-setup)
  - [Azure Static Web Apps Configuration](#azure-static-web-apps-configuration)
- [Deployment Process](#deployment-process)
- [Usage](#usage)
- [CI/CD Pipeline](#cicd-pipeline)
- [Limitations and Considerations](#limitations-and-considerations)
- [License](#license)

## Overview

This project is built to provide a fully serverless application where:
- **Frontend:** A static website hosted on Azure Static Web Apps collects user inputs.
- **Backend:** A Google Apps Script web application processes POST requests to send email notifications and log data into Google Sheets.
- **Data Storage:** Google Sheets serves as a lightweight database, automatically managing data across multiple sheets if a row limit is exceeded.
- **CI/CD:** The entire solution is maintained in a GitHub repository with GitHub Actions automating deployment.

## Features

- **User Data Collection:**  
  - Two forms are provided: one for Quote requests and one for general Contact.
  - Each form gathers necessary information such as name, email, (optionally phone), and message.

- **Serverless Data Processing:**  
  - Form submissions are sent via HTTP POST to a Google Apps Script endpoint.
  - The script sends email notifications and logs each submission with a timestamp.

- **Dynamic Data Management:**  
  - Records are timestamped.
  - If a sheet exceeds a set row limit (e.g., 1000 rows), a new sheet is automatically created.
  - Custom headers are added automatically, and a dropdown list is configured for status updates on a specific field.

- **Email Notifications:**  
  - Designated recipients are alerted by email upon each new submission.

- **User Interface Enhancements:**  
  - The frontend prevents duplicate submissions by disabling the submit button during processing.

## Architecture

1. **Front-End (Azure Static Web Apps):**  
   A static website built with HTML, CSS, and JavaScript collects form data and sends it to the backend.

2. **Back-End (Google Apps Script):**  
   The Apps Script function receives and processes POST requests, handles email notifications, and logs data to Google Sheets.

3. **Data Storage (Google Sheets):**  
   Submitted data is stored in Google Sheets, with logic to create new sheets automatically when a row limit is reached.

4. **CI/CD (GitHub & GitHub Actions):**  
   The project is maintained in a GitHub repository with automated deployments to Azure Static Web Apps via GitHub Actions.

## Setup and Configuration

### GitHub Repository

- The project source code is managed in a GitHub repository.
- The repository contains all frontend assets and configuration files.
- GitHub Actions workflows are used to automate builds and deployments to Azure Static Web Apps.

### Google Apps Script Configuration

- Create a new project in Google Apps Script.
- Implement a serverless function to handle POST requests, send email notifications, and log data in Google Sheets.
- Deploy the script as a web application, ensuring proper access settings (e.g., "Anyone, even anonymous" or "Anyone with a Google account").
- Update the frontend configuration with the deployed web app URL.

### Google Sheets Setup

- Create a Google Sheets document to serve as the data store.
- Note the document's identifier, which is used in the Apps Script configuration.
- The Apps Script automatically adds header rows and manages data across multiple sheets if a set row limit is exceeded.
- A dropdown list is configured for a specific column to allow status updates.

### Azure Static Web Apps Configuration

- Develop the frontend application (HTML/CSS/JavaScript) including Quote and Contact forms.
- Configure the application to send form data to the Google Apps Script endpoint.
- Set up an Azure Static Web App resource and connect it to the GitHub repository for continuous deployment.

## Deployment Process

1. **Commit and Push:**  
   All project files are committed and pushed to the GitHub repository.

2. **Automated Build & Deployment:**  
   GitHub Actions workflows detect changes and automatically build and deploy the project to Azure Static Web Apps.

3. **Google Apps Script Deployment:**  
   The Apps Script is deployed as a web application and its URL is updated in the frontend configuration.

4. **Monitoring:**  
   Deployment and runtime logs are monitored via the dashboards in Azure and Google Apps Script.

## Usage

- **User Interaction:**  
  End users fill out the Quote or Contact forms on the website.

- **Data Submission:**  
  Form data is sent via POST to the Google Apps Script endpoint.

- **Processing and Notification:**  
  The Apps Script function processes the data, sends email notifications to designated recipients, and logs the submission in Google Sheets with a timestamp.

- **Review:**  
  Administrators can review logged data in Google Sheets and update statuses using the provided dropdown.

## CI/CD Pipeline

- The CI/CD pipeline is managed using GitHub Actions.
- Workflow configuration files are stored in the `.github/workflows` directory.
- The pipeline automates the build and deployment process for Azure Static Web Apps upon every push to the main branch.

## Limitations and Considerations

- **CORS Handling:**  
  The frontend uses a no-CORS mode to avoid cross-origin issues, which may limit response details.

- **Quota Limits:**  
  The solution operates within the free-tier quotas for Google Apps Script and email sending. Exceeding these limits may affect functionality.

- **Duplicate Submission Prevention:**  
  UI measures are implemented to disable the submit button during processing, reducing the risk of duplicate submissions.

