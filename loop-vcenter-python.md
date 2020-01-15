# Loop recursively over vCenter

To get all VMs in a vCenter or on a ESX host, you can use the following Python code.
Please make sure to run a `pip3 install pyvmomi` to use this snippet.

```
#!/bin/python3
 
from pyVim import connect
from pyVmomi import vim

allVMs = []
 
def getVms(folder):
    if (isinstance(folder, vim.Folder)) == True:
        subfolder = folder.childEntity
        for s in subfolder:
            getVms(s)
    else:
        #print(folder.name)
        allVMs.append(folder.name)
        return 0
 
# set your ESX hosts or vCenter appliances in this array
hosts = ["vcenter1.domain.com", "vcenter2.domain.com"", "vcenter3.domain.com"]
 
for host in hosts:
    try:
    # Substitute this with your credentials
        si = connect.SmartConnect(host=host, user='youruser', pwd='yourpassword')
    except:
        print("Something is wrong with your connection or credentials")
 
    inv = si.RetrieveContent()
 
    datacenters = inv.rootFolder.childEntity
 
    for datacenter in datacenters:
        if (isinstance(datacenter, vim.Datacenter)) == True:
                rootFolder = datacenter.vmFolder.childEntity
 
                for subfolder in rootFolder:
                    getVms(subfolder)
    try:
        connect.Disconnect(si)
    except:
        print("could not disconnect properly")

print(allVMs)
```
