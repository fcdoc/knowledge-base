---
brief: Understand the scenarios and configuration methods for using custom operations
---

# Custom Operations

---

## Usage Scenarios
---

Custom operations are essentially Webhook calls. You can add custom operations for different collaboration space issues and manually trigger them in the fault details to facilitate rapid troubleshooting or information synchronization.

Common scenarios for using custom operations:
1. **Restart Host**: When the host's memory or CPU is maxed out, trigger a restart script to quickly reboot the host.
2. **Enrich Information**: When an issue occurs, callback your service to retrieve Tracing, Logging, topology, and other information based on the alert details. Proactively use the FlashDuty Open API to update fault information, such as adding tags or setting custom fields, to assist with troubleshooting.
3. **Rollback Changes**: If an issue is determined to be caused by a change, you can directly trigger a callback to your deployment platform to initiate the rollback process, accelerating recovery from the fault.
4. **Update Status Page**: When it is confirmed that a fault affects online services, trigger an update to an external Status Page to notify your customers or stakeholders promptly.

## Configure Custom Operations
---

1. Login to the console and navigate to **Integration Center > Webhook**
2. Click to add a **Custom Operation** integration
3. Configure the following information:
- **Operation Name**, which will be displayed as a button in the fault details.
- **Collaboration Spaces**, where multiple can be configured, but no more than three custom operations can be added per space.
- **Endpoint**, the HTTP(s) request address that is triggered when the custom operation button is clicked.
- **Custom Headers**, the custom headers included in the request to the Endpoint.
4. Save to complete the configuration

After creation, you can see the operation button under [Fault Details - More Operations] in the corresponding space. Click the button and the system will prompt you with the operation result. If the operation is successful, the system will write the operation record.

![custom-action-do.png](https://fcdoc.github.io/img/Sjr8pj4VrgWhgGHEdi8haXEXy1mEnsNuceGjfoDFeG8.avif)

### How to Implement Webhooks?

Visit [Webhook Getting Started](https://developer.flashcat.cloud/doc-2996930) for more information.