# Hyper-V Troubleshooting
Steps and techniques that I use daily when Hyper-V networking remembers that it doesn't actually work in a desktop virtualization context.

These steps assume that Hyper-V networking is generally work for you and you've encountered a temporary issue. This is not intended as a guide for configuring Hyper-V Networking.

## VM is set to use the Default Switch but is not getting an IP address.
The VM is set to use the default switch. The host is connected to a network and may be able to access the internet. However, the VM cannot access the internet or any other network devices. If you run `ipconfig` in CMD, you can see that the VM has an APIPA address (169.254.\*.\*), meaning DHCP is not working.

### Step 1: disconnect and reconnect the host

  1) Disconnect the host from the network
  2) Reconnect the host to the network

Is it working? If not, continue to step 2.

### Step 2: restart the default switch

  1) Set the VM's network adapter to "Not connected"
  2) In "Network connections", disable the device "vEthernet (Default Switch)"
  3) Wait 30 seconds
  4) In "Network connections", enable the device "vEthernet (Default Switch)"
  5) Set the VM to use the default switch

Is it working? If not, try step 2 again, but connect the VM to an external network instead of setting its network adapter to "Not connected". Still not working? Continue to step 3.

### Step 3: use another network adapter on the host

  1) Disconnect the host from the network
  2) Connect the host to the network using another adapter (e.g. Ethernet if using WiFi before)
  3) Wait 30 seconds
  4) Disconnect the host from the network
  5) Connect the host to the network using the original adapter

Is it working? If not, continue to step 4.

### Step 4: restart the host
If the default switch is not working by this point, the last step I know is to restart the host computer.
