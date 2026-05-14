# Windows DNS Troubleshooting Lab

## Overview
This home lab was built using Windows 11 and VMware Workstation to demonstrate core network and DNS troubleshooting skills, including:

- Using `ping` to test network and internet connectivity
- Using `ipconfig /all` to check network adapter settings
- Troubleshooting DNS issues caused by an incorrect DNS server
- Using `nslookup` to test DNS resolution
- Using `ipconfig /release` and `ipconfig /renew` to refresh network settings
- Using `ipconfig /flushdns` to clear the DNS cache
- Identifying the difference between internet issues and DNS issues
- Troubleshooting connectivity problems using Windows PowerShell
- Working through problems step-by-step to find the root cause

## Tools Used
- Windows 11
- Windows PowerShell
- VMware Workstation
- Windows Network & Internet Settings
- Network Adapter Configuration

## Lab Objectives
- Simulate a real-world DNS/Network connectivity issue
- Troubleshoot internet and DNS problems using Windows PowerShell
- Identify the difference between connectivity issues and DNS resolution issues
- Diagnose incorrect network adapter configuration settings
- Restore network connectivity by correcting DNS settings
## Preface
A client submitted a ticket detailing they had internet connectivity issues.  Their PC appeared to be connected to the internet, but they were unable to visit any webpages.  When they attempted to do so, a ‘This site can’t be reached’ message appeared within their browser.

***To simulate this lab for demonstration purposes, I went into Network Settings and changed automatic DNS to static and manually changed the DNS server to an incorrect IP address (192.168.1.250).*** 


![Static DNS Configuration](https://i.ibb.co/wN3RjyyL/Prefix.png)
<br>
<br>
<br>

## Walkthrough

### 1. Testing Local Network Connectivity
First, I needed to acquire the ‘Default Gateway’ address to test its connection with the PC.  I opened Windows PowerShell with Administrator privileges and used `ipconfig`.

![Acquiring Default Gateway](https://i.ibb.co/PZNPbbRq/Acquiring-Default-Gateway.png)
<br>
<br>
<br>
Once I had acquired the ‘Default Gateway’ IP address, I used `ping` to test the local network connectivity to the ‘Default Gateway’.

![Default Gateway Connectivity Test](https://i.ibb.co/mr3CQ35m/Ping-Default-Gateway.png)
<br>
### Result
- Replies received successfully
### Troubleshooting Summary
- The network adapter was working <br>
- The PC was connected to the local network  

---

### 2. Testing Internet Connectivity
Next, I tested the external internet connectivity by pinging Google's public DNS server (8.8.8.8).

![Internet Connectivity Test](https://i.ibb.co/KjjyQSvR/Ping-8-8-8-8.png)
<br>
### Result
- Replies received successfully
### Troubleshooting Summary
- Internet access was still available <br>
- The issue was likely DNS related rather than a general connectivity issue 

---

### 3. Testing DNS Resolution
Based on this, I then attempted to ping a website using its domain name.

![DNS Resolution Test]( https://i.ibb.co/sdc5wh0D/Ping-google-com.png)
<br>
### Result
- Request could not find host
### Troubleshooting Summary
- The PC could reach the internet but DNS resolution was failing 

---

### 4. Checking Network Configuration
Since the PC was able to connect to the internet but the DNS resolution was failing, I next checked the ‘Network Configuration’ to investigate which DNS server the PC was attempting to connect with using `ipconfig /all`. <br>

![Network Configuration Inspection](https://i.ibb.co/rfT1xgxD/ipconfig-all.png)
<br>
### Result
- The PC was attempting to use the DNS server 192.168.1.250
### Troubleshooting Summary
- I needed to test the DNS server directly to confirm whether it was causing the issue

---

### 5. Testing DNS Directly
To confirm this theory, I used `nslookup google.com`. <br>

![Testing the DNS Configuration](https://i.ibb.co/ymgWQ2MH/nslookup-google-com.png)
<br>
### Result
- The DNS request timed out/server failed
### Troubleshooting Summary
- This further confirmed the DNS configuration was causing the connection issue

---

### 6. Correcting the DNS Configuration
After I identified the DNS configuration was the likely issue, I changed the adapter settings back to obtain DNS automatically. <br>

![Configuring DNS](https://i.ibb.co/S47LhbQF/DNS-Configured-Automatic.png)
<br>
<br>
<br>

---

### 7. Refreshing and Retesting the Connection
Once I had corrected the DNS settings, I refreshed the network configuration and retested connectivity. <br>
I first used `ipconfig /flushdns` to clear any cached entries before refreshing the network connection.

![Clearing Cached DNS Entries](https://i.ibb.co/LdM8Bhnn/ipconfig-flushdns.png)
<br>
<br>
<br>
I then used `ipconfig /release` and `ipconfig /renew` to refresh the network connection and ensure the PC was pulling the correct settings from the router.

![Refreshing Network Connection](https://i.ibb.co/vvfMnhFn/ipconfig-release.png)

![Refreshing Network Connection](https://i.ibb.co/zVwT7dNc/ipconfig-renew.png)
<br>
<br>
<br>
Finally, I tested the DNS resolution again to confirm the issue was resolved by pinging ‘google.com’.

![DNS Confirmation Test](https://i.ibb.co/1f504y9n/ping-google-com-success.png)
<br>
### Result
- Successful replies received <br>
- Websites began working normally again
### Troubleshooting Summary
- The DNS server had been manually configured to an incorrect static IP address and was failing to resolve.


---

## Summary and Skills Learned
This lab helped strengthen my understanding of Windows network troubleshooting, DNS resolution, network adapter configuration and step-by-step troubleshooting using Windows PowerShell within a Windows 11 environment. <br>
### Skills Demonstrated:
- DNS Troubleshooting
- Network Connectivity Testing
- Windows PowerShell
- Windows 11 Networking
- VMware Workstation
- Network Adapter Configuration
- DNS Resolution Testing
- Windows Networking Commands (`ping`, `ipconfig`, `nslookup`)

