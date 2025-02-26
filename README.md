# cloud-basics

A primer for running data science workloads on cloud resources.

> [**Slide Deck**](DS6051-Cloud-Computing.pdf)

## AWS Service Catalog

A UVA-managed catalog of prepackaged solutions and services. Provides self-service provisioning of cloud resources.

Sign in here using your UVA credentials:

> **https://eservices-uva.awsapps.com/start/#/?tab=accounts**

## SSH Keys and Access

### Keys
Using a terminal either create or us an existing SSH keypair. To create a new pair:

```bash
ssh-keygen -t rsa
```
You can specify a name if you like, or accept the defaults. Note the public key and private key. (The latter must be `chmod 600` for security purposes.)

Do not share your private key with anyone. Rotate keys at least 1x a year.

**COPY** and paste your public key into the AWS Service Catalog when you provision a Keypair.

### SSH Connections

Once your EC2 instance has been created (following the steps below) you will use your SSH keypair as a means of authentication. Cloud instances tend not to have system usernames/passwords, as SSH keys are more secure.

To connect to your instance, you need to know (1) the default username to connect as, and (2) the public IP address of your new instance. Together with your private key you can establish a connection:

```
ssh -i ~/.ssh/my_key ubuntu@12.34.56.78
```

## Launch your instance

Once you have signed into the AWS Access Portal above, complete the following steps to create a new EC2 instance:

1. Find the **AWS-SDS-Agarwal** account and expand the box.
2. Click into the `ServiceCatalogReadOnly` account, which will open up the AWS Console home page.
3. In the upper-right corner, be sure you are in the "United States (N. Virginia) region.
4. Using the search box at the top, enter "Service Catalog" and click into it. You can also click the star next to the service name to bookmark it in the top of your browser.
5. Within the Service Catalog, select "Products" under the "Provisioning" section in the left hand navigation.

**Provision an SSH Keypair**

6. First select the Keypair and then launch the product.
7. We suggest you provision the product name as "uva-xxxx-keypair" where you replace `xxxx` with your computing ID. For the keyname, we suggest `uva-xxxx` where you replace `xxxx` with your computing ID.
8. In the `PublicKey` field, paste in the single line contents of your SSH public key.
9. Finally, click "Launch product" to complete the task.

**Provision an EC2 Instance**

10. From the Service Catalog list of "Products" select the "Ec2 Ml" product, then Launch Product.
11. For Provisioned Product Name, we suggest naming it `xxxx-ds6051-instance` where you replace `xxxx` with your computing ID.
12. Leave the Instance Type as `t1.micro`.
13. Select your keypair from the list of available keys.
14. Select either subnet in the `SubnetId` field.
15. Under "Manage Tags" we suggest you add a custom tag. Click the "Add new item" button, and create a field with a key `Name` and a value of your computing ID (i.e. `mst3k`, `nem2p`, etc.)
16. Finally, click "Launch Product". Your new instance will be provisioned in 1-2 minutes. You can refresh the page using the refresh (circular arrow) button. Once complete, near the bottom click into the "Outputs" tab to see your instance attributes. The most important attribute is the `PublicIp` which you will need to connect. 

## Stop/Start your instance

Assuming you just created your instance, and you are still on your provisioned product details page, note the "Actions" dropdown in the upper-right corner.

To stop your instance, select:

- Actions -->
- Service Actions -->
- EC2-Stop

To start or restart your instance, select:

- Actions -->
- Service Actions -->
- EC2-Start / EC2-Restart

**For cost management purposes it is important that you turn off your instance whenever you are not using it.**

## Resize your instance

To resize or re-type your instance, i.e. extend or reduce its CPU/MEM/GPU resources, do the following:

1. Stop your instance. Confirm this action.
2. Next, select the "Update" option from the Actions menu.
3. Change the InstanceType as necessary.
4. Click Update and wait for the change to propagate.
5. Finally, start your instance again from the Actions menu.

**BE SURE if you resize up to a `trn1.2xlarge` instance type to resize your instance back down to a `t1.micro` after you are done.**

## Basic Sysadmin Tasks

- `sudo`
- `apt`
- `htop`
- `cron`
- `df -h`
- `du -sh`

## More information

- [Data Science Essentials](https://www.youtube.com/playlist?list=PLxBq1F-c5mHq5r89REM7STJaq360VjuVo) (Youtube)
- [AWS EC2 On-Demand Pricing](https://aws.amazon.com/ec2/pricing/on-demand/)
- [AWS Training & Certification](https://aws.amazon.com/training/)
- [Infrastructure as Code](https://docs.aws.amazon.com/whitepapers/latest/introduction-devops-aws/infrastructure-as-code.html)
