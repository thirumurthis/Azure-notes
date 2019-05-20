
1. Creating a VM
2. Encrypting a VM (Bootlocker - Windows; DM-Crypt - Linux)
Lab:
3. Virtual Network creation, (range of IP Address, fire wall, etc).
4. Availablility set creation - Logical group of VMs, incase of failures.
        
        An Azure Availability Set is a logical grouping of virtual machines (VMs) in Azure. When you create VMs within an Availability Set, the Azure platform distributes the placement of those VMs across the underlying infrastructure. During planned maintenance on the Azure platform, or in the event of an unexpected fault in the underlying hardware/infrastructure, Availability Sets ensure that at least one VM remains operational.
        
       Fault Domain: Virtual machines in the same Fault domain share a common power source and physical network switch.
   
       Update Domain: Virtual machines in the same Update Domain will be restarted together during planned maintenance. Azure never restarts more than one Update Domain at a time.

       Use Managed Disk: (property) Azure Managed Disks simplifies disk management for Azure IaaS VMs by managing the storage accounts associated with the VM disks. You only have to specify the type (Premium or Standard) and the size of disk you need, and Azure creates and manages the disk for you.


Create VM option:

       <Network section> : Verify that the Public IP address field has a status that begins with (new)
        Note: Use a public IP address if you want to communicate with the virtual machine from outside the virtual network. For example, if you will need to RDP to the VM, you will need a public IP address.
        
                NIC Network security group: (Advanced option)
                  Note: A Network Security Group is a set of firewall rules that control traffic to and from your virtual machine.
       
                Accelerated Network :  Accelerated networking Enables low latency and high throughput on the network interface.
        
       <Management section> :
       Boot diagnosis:  
        Note: Azure Monitor enables you to consume telemetry to gain visibility into the performance and health of your workloads on Azure. The most important type of Azure telemetry data is the metrics (also called performance counters) emitted by most Azure resources.
        
       <Tag section> : 
       After you apply tags, you can retrieve all the resources in your subscription with that tag name and value. Tags enable you to retrieve related resources from different resource groups. This approach is helpful when you need to organize resources for billing or management.
       

Demo:

a. create a Key Vault, 
b. Add the key to the keyvault, called KEK (Key encryption key)
c. Enable the Access policy in the key vault advanced option (list below, and save it)
      Enable Acess to Azure Disk Encryption for volume encryption.
      Enable access to Azure Resource Manager for template deployment. 
      Enable access to Azure Virtual Machines for deployment.
d. Create a VM, in this case use a windows VM.

```
$keyVaultName = "<keyvalut name>"
$rgName = "<resource group name>"
$vmName = "<vmname>"
$keyVault = Get-AzKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzKeyVaultKey -VaultName $keyVaultName -Name aztimkeyEK01).Key.kid;
```

```
Set-AzVMDiskEncryptionExtension -ResourceGroupName $rgName `
-VMName $vmName `
-DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
-DiskEncryptionKeyVaultId $keyVaultResourceId `
-KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
-KeyEncryptionKeyVaultId $keyVaultResourceId
```

 5. Creating Recovery Services vault.
       -> All service -> recovery -> provide name, resource group
       -> attach to the VM, but clicking the VM -> operations -> backup select the created recovery
  
