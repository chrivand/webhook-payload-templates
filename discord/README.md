# Discord


Send an alert message to a Discord channel

<hr>

<img src="alert-critical.png" width="400"/>

<img src="alert-warning.png" width="400"/>

<img src="alert-informational.png" width="400"/>

<hr>


## Setup

### Discord

Add an **Integration** to your Discord server. 

You can do this by selecting the **settings** option for your channel. 

<img src="webhook-setup-settings.png" width="200">

Then select **Integrations**

<img src="webhook-setup-integrations.png" width="400">

Create a **New Webhook**

<img src="webhook-setup-create.png" width="400">

**Copy Webhook URL** to be used by Meraki as the HTTP Server URL

[Discord Webhooks](https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Webhooks)

[API Docs](https://discord.com/developers/docs/intro)


## Template 

- [body.liquid](body.liquid)
- HTTP Server URL:  `https://discord.com/api/webhooks/<channel id>/<token>`

```body.liquid
{
  "type": 1,
  "embeds": [{
      "title": "{{alertType}}",
      "color": "{% if alertLevel == "critical" %}13632027{% elsif alertLevel == "warning"  %}16098851{% else %}8311585{% endif %}",
      "description": "Occured at: {{occurredAt | slice: 0,10}} {{occurredAt | slice: 11,8}}",
      "fields": [
        {
        "name": "Organization",
        "value": "[{{organizationName}}]({{organizationUrl}})",
        "inline": true
      },
      {
        "name": "Network",
        "value": "[{{networkName}}]({{networkUrl}})",
        "inline": true
      },
      {
        "name": "Device",
        "value": "{{deviceName}}"
      },
      {
        "name": "Alert Data",
        "value": "{{alertData | json_markdown}}"

      }
      ]
  }]
}
```