# Job Application Tracker

Track and manage your job applications using GitHub Issues![^1]

[![Add New Application](https://img.shields.io/badge/Add_New_Application-%230A69DA?style=plastic)](../../issues/new?template=job-application.yml)
[![View Sankey Diagram](https://img.shields.io/badge/View_Sankey_Diagram-%231B7F37?style=plastic)](sankey.md)
[![Setup Labels](https://img.shields.io/badge/Setup_Labels-%23E0E6EA?style=plastic)](../../actions/workflows/setup-labels.yml)

## Features

<img src="https://github.com/tfle/job-application-tracker/blob/main/.github/images/sankey-example.png" width="50%" align="right"/>

- **Stage tracking:** Add labels to each issue when you move to the next stage (e.g. `Applied`, `Interview`, `Offer`)
- **Visual pipeline:** View your job search progress with an automatically generated Sankey diagram
- **Email reminders:** Get optional notifications when applications open/close

## Get Started

### 0. Create Repository

Create a new repository based on this template (Use this template > Create a new repository). Follow the remaining steps in your own repository.

> [!TIP]
> Make your repository private to keep your job search confidential!

### 1. Setup Labels

Click on [Setup Labels](../../actions/workflows/setup-labels.yml) and manually run the workflow. This configures your application stages from [.github/labels.yml](.github/labels.yml). The default label names are:

```yaml
- name: "Applied"
- name: "Phone Interview"
- name: "Online Assessment"
- name: "Assessment Centre"
- name: "Interview"
- name: "Final Interview"
- name: "Offer"
- name: "Rejected"
- name: "Accepted"
- name: "Declined"
```

> [!NOTE]
> The order is used in generating the Sankey diagram. Importantly, any "terminal stage" label (e.g. `Offer`, `Rejected`, `Accepted`, and `Declined`) should go at the end, but the ordering within this group doesn't really matter as it's assumed that only one of these labels will be added to an issue. If you edit [.github/labels.yml](.github/labels.yml), the Setup Labels workflow will run automatically.

### 2. Add Applications

Click on [Add New Application](../../issues/new?template=job-application.yml) to create an issue for each job. You can enter the opening/closing dates and enable reminders in the issue template.

### 3. Track Progress

Add labels as you move through application stages. Click on [View Sankey Diagram](sankey.md) to see an overview of your application pipeline.

> [!IMPORTANT]
> Labels can be applied (or unapplied) to issues as per normal, however, they should only ever be modified through editing [.github/labels.yml](.github/labels.yml). This ensures that the Sankey diagram is generated correctly.

## How This Works

### Reminders

The [send reminders workflow](.github/workflows/send-reminders.yml) runs daily at UTC+00:00 and posts automated comments (triggering an email notification) for any applications that have valid opening/closing dates and reminders enabled. Issues with the `Applied` label are skipped.

### Sankey Diagram

The [generate Sankey workflow](.github/workflows/generate-sankey.yml) will update changes in [sankey.md](sankey.md) when there's progression on a job application (issues are opened/closed or labelled/unlabelled). Only issues with 2 or more labels will appear in the Sankey diagram.

> [!TIP]
> New job applications with just an `Applied` label won't be considered (as there's no source-to-target "flow" to visualise). To get around this, you can add an `In Progress` label at the end of [.github/labels.yml](.github/labels.yml). You can then apply the `In Progress` label to all your active applications (remember to remove it when you receive a final outcome)!

[^1]: You're already on GitHub, why not? 😄
