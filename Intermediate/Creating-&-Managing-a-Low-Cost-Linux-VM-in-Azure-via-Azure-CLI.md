Creating & Managing a Low-Cost Linux VM in Azure via Azure CLI (Cloud Shell)

1. Environment
- Using Azure Cloud Shell (no installation needed, already logged in to your Azure account).
- Cloud Shell runs `az` (Azure CLI) commands directly.
--------------------------------------------------------------
2. Create Resource Group

```bash
az group create \
  --name demo-rg \
  --location eastus
```
- demo-rg → your resource group name.
- eastus → region (choose closest and cheapest).
--------------------------------------------------------------
3. Create Low-Cost Linux VM

```bash
az vm create \
  --resource-group demo-rg \
  --name demo-vm \
  --image Ubuntu2204 \
  --size Standard_B1s \
  --admin-username azureuser \
  --generate-ssh-keys \
  --public-ip-sku Standard \
  --authentication-type ssh
```
Important:
- `Standard_B1s` → cheapest burstable VM size.
- `-public-ip-sku Standard` is required (Basic SKU may not be allowed in new subscriptions).
- SSH keys are generated and stored in `~/.ssh`.
--------------------------------------------------------------
4. Get Public IP of VM

```bash
az vm show \
  --resource-group demo-rg \
  --name demo-vm \
  --show-details \
  --query publicIps \
  --output tsv
```
--------------------------------------------------------------
5. Connect to VM

```bash
ssh azureuser@<PUBLIC_IP>
```
Replace `<PUBLIC_IP>` with the output from step 4.
--------------------------------------------------------------
6. Install Apache (Inside VM)

```bash
sudo apt update
sudo apt install apache2 -y
sudo systemctl enable apache2
sudo systemctl start apache2
```
Note: On Ubuntu/Debian, the package is called `apache2` (not `apache`) because it’s Apache HTTP Server v2.x.
--------------------------------------------------------------
7. Open Port 80 in Azure (From Cloud Shell, Not Inside VM)

If still connected to VM, exit:

```bash
exit
```

Then run:

```bash
az vm open-port \
  --resource-group demo-rg \
  --name demo-vm \
  --port 80
```
--------------------------------------------------------------
8. Test Apache

In browser:

```
http://<PUBLIC_IP>
```

You should see Apache’s default page.
--------------------------------------------------------------
9. VM States — Stopped vs Stopped (Deallocated)

- Stopped → VM powered off but compute hardware still reserved → still paying for compute.
- Stopped (deallocated) → VM powered off and hardware released → no compute charges (still pay for storage and static IPs).
- To deallocate:

```bash
az vm deallocate --resource-group demo-rg --name demo-vm
```

- To start:

```bash
az vm start --resource-group demo-rg --name demo-vm
```
--------------------------------------------------------------
10. Delete Resource Group

Wait until complete (blocking):

```bash
az group delete --name demo-rg --yes
```

Delete in background & monitor:

```bash
az group delete --name demo-rg --yes --no-wait
watch -n 5 az group show --name demo-rg --query "properties.provisioningState" -o tsv
```

When it says `ResourceGroupNotFound`, deletion is done.

--------------------------------------------------------------

✅ Tips for cost control in demos:

- Always `deallocate` when not using the VM.
- Consider setting up an auto-shutdown policy to avoid forgetting.
- Use `Standard_B1s` in a low-cost region for minimum expense.
--------------------------------------------------------------
