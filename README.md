# Job Application Tracker

Track and manage your job applications using GitHub Issues![^1]
- Add labels to each issue when you move to the next stage (e.g. `Applied`, `Interview`, `Offer`)
- View your job search progress with an automatically generated Sankey diagram
- Get optional email reminders when applications open/close

## Get Started

Clone this repo or click on `Use this template` and then `Create a new repository`. Follow the next step in your own repository.

### Configure Labels

Manually run the `Setup Labels` workflow in the [Actions tab](../../actions/workflows/setup-labels.yml). This deletes all existing labels and adds the custom labels found in [labels.yml](.github/labels.yml). The default ones are:

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
> The order is used in generating the Sankey diagram. Importantly, any "terminal stage" label (e.g. `Offer`, `Rejected`, `Accepted`, and `Declined`) should go at the end, but the ordering within this group doesn't really matter as it's assumed that only one of these labels will be added to an issue. If you edit the `labels.yml` file, the `Setup Labels` workflow will run automatically.

### Usage

Create a `New issue` for each new job application. The custom issue template will ask for some optional details, including application open/close dates and notification reminders.

Reminders are done via an automated comment on the issue (which will trigger an email notification). By default, the [reminder workflow](./github/workflows/send-reminders.yml) checks if a comment needs to be posted each day at UTC+00:00.

Once there's progression on a job application (two or more labels on an issue), the [Sankey workflow](.github/workflows/generate-sankey.yml) will update changes in [sankey.md](sankey.md).

> [!IMPORTANT]
> Labels can be applied (or unapplied) as per normal, however, they should only ever be modified via the `labels.yml` file. This ensures that the Sankey diagram is generated correctly.

> [!TIP]
> New job applications with just an "Applied" label won't be considered (as there's no source-to-target "flow" to visualise). To get around this, you can add an "In Progress" label at the end of the [labels.yml](.github/labels.yml) file. You can then apply the "In Progress" label to relevant issues (remember to unapply it when you have an outcome)!

[^1]: You're already on GitHub, why not? 😄
