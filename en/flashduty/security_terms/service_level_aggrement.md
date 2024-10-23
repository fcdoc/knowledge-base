---
brief: Learn about the SLA commitments of Flashduty from Kuaimao Nebula Technology Co., Ltd
---

# Flashduty Service Level Aggrement

---

Last updated: 2024-04-28

This Service Level Agreement (hereinafter referred to as "SLA") outlines the service availability metrics and compensation plan for the Flashduty service provided to you by Kuaimao Nebula.

Please note that, unless otherwise specified, this agreement does not apply to the public beta, invite-only beta, free features and versions, or the privatized versions of Flashduty.

## How We Ensure the SLA
---

1. **Same-City Multi-Active**: The infrastructure is built across multiple data centers, with stateful components designed to be multi-active within the same city
2. **Asynchronous Processing**: After an alert is reported, it immediately enters an asynchronous process, with retries for errors to minimize the risk of alert loss
3. **Redundant Alerts**: For critical alerts, a redundant notification mechanism is provided, allowing you to select multiple channels for cyclic notifications to ensure reachability
4. **Global Acceleration**: Global acceleration is enabled for the api.flashcat.cloud domain to ensure stable reporting links worldwide
5. **Continuous Monitoring**: Comprehensive system metrics are collected, regular stress tests are conducted, and system issues are identified promptly or proactively.

## Our SLA Commitments
---

- **Function Availability (Error Rate)**: Core functions are available 99.9% of the time
- **Delivery Timeliness (Delay Rate)**: 99.9% of alerts are delivered within 5 minutes of being triggered

### Calculation Method

**A cycle is every 5 minutes; if the error rate or delay rate in any cycle reaches 0.1%, that cycle is deemed not to meet the availability commitment.**

Specific Definitions Are As Follows:

- **Service Cycle**: A complete service cycle consists of 30 days (not calendar months).
- **Total Minutes in Service Cycle**: The total number of days in the service cycle multiplied by 24 (hours) multiplied by 60 (minutes).
- **Monthly Service Fee**: The total amount you pay for the Flashduty service under a specific Kuaimao Nebula account in one cycle. If you pay for multiple months in advance, the monthly service fee will be calculated based on the number of months or usage purchased.
- **Failed Requests**: Failed requests include the following scenarios:
- Requests to the Flashduty API that return status codes of 500/502 due to Flashduty system issues.
- Requests that fail to reach the Flashduty API server due to Flashduty failures. When a Flashduty service failure occurs and the number of failed requests cannot be determined, the average number of API service calls per minute over the previous 7 natural days will be calculated, and this average will be multiplied by the duration of the failure to estimate the number of failed requests.
- **Valid Total Requests**: All requests received by the Flashduty API server are considered valid total requests.
- **Failed Notifications**: Failed notifications include the following scenarios:
- Notifications that fail to be delivered due to Flashduty system issues
- Notifications that are delayed in delivery due to Flashduty system issues, with a delay exceeding 5 minutes.
- **Valid Total Notifications**: All alerts triggered by Flashduty are considered valid total notifications.
- **Error rate** : Number of failed requests every 5 minutes / Total number of valid requests every 5 minutes × 100 %
- **Latency rate** : number of failed notifications every 5 minutes / Total number of valid notifications every 5 minutes × 100 %


### Exceptions

The duration of service unavailability due to the following reasons will not be counted towards the unavailability time:

- Unavailability caused by system maintenance performed by Kuaimao Nebula after advance notice, including cutover, maintenance, upgrades, and simulated fault drills
- Unavailability caused by network or equipment failures or configuration adjustments external to Kuaimao Nebula's equipment
- Unavailability caused by hacker attacks on your applications or data
- Unavailability caused by your improper maintenance or confidentiality practices, resulting in the loss or leakage of data, passwords, or other credentials
- Unavailability caused by your negligence or actions authorized by you
- Unavailability caused by your failure to follow Kuaimao Nebula's product documentation or recommendations
- Delays in push notifications caused by carrier or terminal signal issues
- Unavailability caused by force majeure events.


## How to Apply for Compensation
---

### Compensation Standards

Compensation is calculated based on the service availability of Flashduty under one of your Kuaimao Nebula accounts, according to the standards in the table below. Compensation is limited to gift funds for purchasing Flashduty products and does not exceed the monthly service fee paid for the month in which the service availability commitment was not met (excluding any discounts from gift funds).

```
赔偿赠送金金额 = 未达到SLA的分钟数 * 月度服务费用每分钟金额 * 10
```

### Application Deadline

You may submit a compensation claim for Flashduty's failure to meet service availability commitments in the previous month after the fifth (5th) working day of each calendar month.

Compensation claims must be submitted no later than two (2) months after the end of the month in which Flashduty failed to meet its service availability commitments.

## Additional Information
---

Kuaimao Nebula reserves the right to modify the terms of this SLA.

If any changes are made to the SLA terms, Kuaimao Nebula will notify you 30 days in advance through a website announcement or by email. If you do not agree with the modifications to the SLA, you have the right to cease using Flashduty. If you continue to use Flashduty, it will be deemed that you accept the modified SLA.