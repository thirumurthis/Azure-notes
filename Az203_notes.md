
1. Creating a VM
2. Encrypting a VM (Bootlocker - Windows; DM - Locker - Linux)
Lab:
3. Virtual Network creation, (range of IP Address, fire wall, etc).
4. Availablility set creation - Logical group of VMs, incase of failures.
        
        An Azure Availability Set is a logical grouping of virtual machines (VMs) in Azure. When you create VMs within an Availability Set, the Azure platform distributes the placement of those VMs across the underlying infrastructure. During planned maintenance on the Azure platform, or in the event of an unexpected fault in the underlying hardware/infrastructure, Availability Sets ensure that at least one VM remains operational.
        
       Fault Domain: Virtual machines in the same Fault domain share a common power source and physical network switch.
   
       Update Domain: Virtual machines in the same Update Domain will be restarted together during planned maintenance. Azure never restarts more than one Update Domain at a time.
'

