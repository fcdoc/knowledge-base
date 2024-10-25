---
brief: By integrating a third-party Slack application, the capability to receive and respond to alerts within Slack is achieved
---

# Slack Integration

---

By integrating a third-party Slack application, the capability to receive and respond to alerts within Slack is achieved.

## 1. Install the Application
---

1. Access the FlashDuty `Integration Center` - `Instant Messaging` - `Slack` - `Add`

2. The page will redirect to the Slack interface; select `Workspace` in the upper right corner, then click `Allow`

<img src="https://fcdoc.github.io/img/aXIi-nrANb2NC__s3jg6kIgcoh68NENKYDJb8xhf9Mk.avif" alt="drawing" width="400"/>

3. Enter the data source name and click `Save`


## 2. Common Issues
---

1. **The desired private channel is missing from the group chat list in the dispatch policy**
- To add the application to a channel, ensure that step one, `Install Application`, is completed without errors
- Enter the relevant Slack channel, execute `/invite @FlashDuty`, and if prompted with `Joined` or `Added by xx to xxx`, it indicates successful addition

2. **The desired public channel is missing from the group chat list in the dispatch policy**
- Add the app authorizer to the public channel
- Or refer to `FAQ 1` to add the application to the channel

3. **Error encountered when clicking the 'Allow' button in step 2 of the installation process**
- Retry the operation. There might be a communication issue between the server and Slack, leading to authorization problems. Return to the data source addition page and attempt again
- If the error persists after retrying, contact customer support

4. **Error encountered when clicking the 'Save' button in step 3 of the installation process**
- Retry the operation. There might be a communication issue between the server and Slack, causing an error in obtaining the permanent authorization code. Return to the data source addition page and attempt again
- If the error persists after retrying, contact customer support

5. **'not_authed' error within the Slack App**
- Retry the operation. There may be an issue with the Slack service
- If the error persists after retrying, contact customer support

6. **'Operation timed out' error within the Slack App**
- Retry the operation. There may be a timeout issue between the server and Slack, indicating a communication problem
- If the error persists after retrying, contact customer support

7. **'This app responded with Status Code 500' error within the Slack App**
- Retry the operation. There may be a service error, for instance, the data source might be closed
- If the error persists after retrying, contact customer support

8. **'Other questions' error within the Slack App**
- Retry the operation. An unrecorded issue has been encountered
- If the error persists after retrying, contact customer support