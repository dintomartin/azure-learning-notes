Azure Virtual Network + Two Linux VMs

Objective -
Learn how Azure Virtual Network works by creating two Linux VMs, placing them in the same subnet, and testing connectivity (ping + SSH).
----------------------------------------

Step-by-Step Demo Procedure

1. Create a Virtual Network

- In Azure Portal → Create resource → Virtual Network
- Example address space: `10.0.0.0/16` (Subnet mask: `255.255.0.0`)
- Default subnet: `10.0.0.0/24` → IP range `10.0.0.0 – 10.0.0.255`
- No need to create extra subnet for this demo — default subnet is fine.
----------------------------------------

2. Network Security Group (NSG) Rules

By default, an NSG has:
- `AllowVnetInBound` — allows all VM↔VM traffic in same VNet (so Rule B not required).
- `AllowSSH` — only if you check “Allow SSH” at creation.
- `DenyAllInBound` — blocks everything else.

For external SSH:
- Rule A: Allow SSH from your IP
    - Protocol: TCP, Port 22
    - Source: My IP
    - Action: Allow
----------------------------------------

3. Create Two Linux VMs

- Place both VMs in:
    - Same resource group (e.g., `rg-demo-vnet`)
    - Same Virtual Network
    - Same subnet (default)
- Use Username + Password authentication (simpler for demo).
- Enable Allow SSH (22) when creating.
- Use B1s or B1ms size to keep cost minimal.
----------------------------------------

4. Test Connectivity

From your laptop → VM1

```bash
ssh <username>@<vm1-public-ip>
```

From VM1 → VM2 (private IP)

```bash
ping -c 4 <vm2-private-ip>
ssh <username>@<vm2-private-ip>
```

From VM2 → VM1 (private IP)

```bash
ping -c 4 <vm1-private-ip>
```
----------------------------------------

5. Using Azure CLI

```bash
az login
az extension add --name ssh   # if needed

# SSH to VM1
az ssh vm --resource-group rg-demo-vnet --name vm1
```

From VM1:

```bash
ssh <username>@<vm2-private-ip>
```
----------------------------------------

6. Ping from Laptop to VM1

- Why it fails by default:
    
    ICMP (ping) is blocked in NSG + possibly VM firewall.
    
- To allow ping:
    1. NSG inbound rule: Protocol = ICMP, Source = My IP, Action = Allow
    2. On VM:
        
        ```bash
        sudo ufw allow icmp
        # or disable firewall for demo:
        sudo ufw disable
        ```
        
    3. Then:
        
        ```bash
        ping <vm1-public-ip>
        ```
----------------------------------------

Key Concept Answers - 

Why subnets are required:

A VNet is just an address space. Azure assigns IPs from subnets — you cannot attach a VM directly to the VNet without a subnet.

Difference between `10.0.0.0 – 10.0.255.255` and `10.0.0.0 – 10.0.0.255`:

- `/16` (`255.255.0.0`) → `10.0.0.0 – 10.0.255.255` (65,536 IPs)
- `/24` (`255.255.255.0`) → `10.0.0.0 – 10.0.0.255` (256 IPs)

Why port 22 for SSH:

SSH runs on TCP port 22 by default — used for remote terminal access.

Why Rule B isn’t needed for same subnet:

`AllowVnetInBound` default rule already allows VM↔VM traffic in the same VNet.

Where “VirtualNetwork” source option is:

It’s under Service Tag in NSG rules.

Why ping public IP from VM2 fails:

Azure doesn’t allow “hairpin” routing (public IP to same VNet). Always use private IP inside VNet.

Why `NetworkWatcherRG` appears:

Azure auto-enables Network Watcher in a region when you create networking resources for the first time. Cost is negligible.
----------------------------------------

✅ Minimal Cost Tips

- Use B1s size for VMs
- Use same region + resource group
- Delete VMs, VNet, and NICs when demo is done to avoid charges
----------------------------------------
