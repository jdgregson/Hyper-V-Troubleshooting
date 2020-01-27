# Hyper-V Troubleshooting
Steps and techniques that I use daily when Hyper-V networking remembers that it doesn't actually work in a desktop virtualization context.

These steps assume that Hyper-V networking is generally work for you and you've encountered a temporary issue. This is not intended as a guide for configuring Hyper-V Networking.

## VM is set to use the Default Switch but is not getting an IP address.
The VM is set to use the default switch. The host is connected to a network and may be able to access the internet. However, the VM cannot access the internet or any other network devices. If you run `ipconfig` in CMD, you can see that the VM has an APIPA address (169.254.\*.\*), meaning DHCP is not working.

### Step 1: disconnect and reconnect the host

  1) Disconnect the host from the network
  2) Reconnect the host to the network

Is it working? If not, continue to step 2.

### Step 2: connect the VM to an external network
I have encountered numerous situations where the VM refuses to use the default switch until after it is permitted to connect directly to an external network. You may be able to get this step to work by using "Not connected" as the VMs network adapter, but I have not had a lot of luck with that.

  1) Set the VM to use a virtual switch of type "External network"
  2) Wait 30 seconds
  3) Set the VM to use the default switch

Is it working? If not, continue to step 3.

### Step 3: connect the VM to an external network and restart the default switch
This is the same as step 2, but you disable the default switch device in between.

  1) Set the VM to use a virtual switch of type "External network"
  2) In "Network connections", disable the device "vEthernet (Default Switch)"
  3) Wait 30 seconds
  4) In "Network connections", enable the device "vEthernet (Default Switch)"
  5) Set the VM to use the default switch

Is it working? If not, continue to step 4.

### Step 4: use another network adapter on the host
If the host is connected to the network via WiFi, turn off WiFi and connect via Ethernet instead, etc.

  1) Disconnect the host from the network
  2) Connect the host to the network using another adapter (e.g. Ethernet if using WiFi before)
  3) Wait 30 seconds
  4) Disconnect the host from the network
  5) Connect the host to the network using the original adapter

Is it working? If not, continue to step 5.

### Step 5: restart the host
If the default switch is not working by this point, the last step I know is to restart the host computer.
