# Assignment

### Blue Ocean

1. From the administrator account, move to Manage Jenkins -> Manage Plugins.
2. Install Blue Ocean (BlueOcean Aggregator) plugin from the list of Available plugins.
3. Install Blue Ocean along with the required dependencies.
4. Restart Jenkins. Type in terminal  sudo service jenkins restart
5. Upon restart, enable the Blue Ocean option from the GUI.

### Private repository as FreeStyle Project

1. Setup a new freestyle project - New Item -> Freestyle project.
2. Set Source Code Management to Git.
3. Provide the private repository link in Repository URL.
4. To permit Jenkins to access the Private Github repository, please update the credentials. Add -> Credentials -> Jenkins and update.
5. Set this as the Credentials.
6. Update the branch (if required) - Default : */master.

### Git SCM Poll

1. Map the [Jenkins URL](http://localhost:8080/) to a public IP address.
  
  - Map a Public IP to your [Jenkins URL](http://localhost:8080/) using ngrok.
  - Download and setup ngrok from [here](https://ngrok.com/download).
  - Run ./ngrock http 8080 map your Jenkins port (8080) to a public IP. The public URL http://<foo>.ngrok.io should be used as the Webhook.

2. Setup
  
  - Navigate Settings -> Webhooks -> Add webhook in the repository.
  - Update the Payload URL to the Public IP http://<foo>.ngrok.io/github-webhook/.
  - Set Content type as application/json.
  - Update Which events would you like to trigger this webhook? as per requirement.
  - Ensure that the Active option is selected.

## Post-build Actions

1. Select the project and navigate Configure -> Post-build Actions
2. In Add post-build action choose Archive the artifacts.
3. Mention the files to archive ( * to archive all the files).
4. In the Advanced tab, enable Archive only if build is successful and Use default excludes.

