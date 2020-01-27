# Hyper-V Troubleshooting
Steps and techniques that I use daily when Hyper-V networking remembers that it doesn't actually work in a desktop virtualization context.

These steps assume that Hyper-V networking is generally work for you and you've encountered a temporary issue. This is not intended as a guide for configuring Hyper-V Networking.

## VM is set to use the Default Switch. It does not have internet access while the host does.
### Step 1: disconnect and reconnect the host

  1) Disconnect the host from the internet
  2) Reconnect the host to the internet

Is it working? If not, continue to step 2.

### Step 2: connect the VM to an external network
I have encountered numerous situations where the VM refuses to use the default switch until after it is permitted to connect directly to an external network. You may be able to get this step to work by using "Not connected" as the VMs network adapter, but I have not had a lot of luck with that.

  1) Set the VM to use a virtual switch of type "External network" (and allow it to connect to the internet)
  2) Wait 30 seconds
  3) Set the VM to use the default switch

Is it working? If not, continue to step 3.

### Step 3: connect the VM to an external network and restart the default switch
This is the same as step 2, but you disable the default switch device in between.

  1) Set the VM to use a virtual switch of type "External network" (and allow it to connect to the internet)
  2) In "Network connections", disable the device "vEthernet (Default Switch)"
  3) Wait 30 seconds
  4) In "Network connections", enable the device "vEthernet (Default Switch)"
  5) Set the VM to use the default switch

Is it working? If not, continue to step 4.

### Step 4: restart the host
If the default switch is not working by this point, the last step I know is to restart the host computer.
