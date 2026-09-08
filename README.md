# DNS Troubleshooting Lab

**Scenario:** A Windows 11 domain client was unable to resolve the domain controller by hostname. I investigated the client's network configuration, identified an incorrect DNS server, corrected the configuration, and verified that DNS resolution and network connectivity were restored.

## 1. Verify the Working DNS Baseline

I used `ipconfig /all` to review the Windows 11 client's network configuration and establish the working DNS configuration. The client was configured to use the domain DNS server at `10.1.10.2`.


<img width="1672" height="941" alt="01-working-dns-baseline (1)" src="https://github.com/user-attachments/assets/713714a3-362f-4ec5-a2a0-f00d49cbf5a7" />


## 2. Identify the Incorrect DNS Configuration

I reviewed the client's network configuration after the DNS issue occurred and found that the DNS server was incorrectly set to `10.1.10.99` instead of the domain DNS server at `10.1.10.2`.


<img width="1744" height="592" alt="02-working-dns-baseline" src="https://github.com/user-attachments/assets/4853b894-501a-4dbe-ab00-43aeb95521ca" />


## 3. Confirm the DNS Resolution Failure

I ran `nslookup NY-DC-01` to test hostname resolution. The client attempted to query `10.1.10.99` and failed to resolve the domain controller hostname, confirming a DNS resolution problem.

<img width="636" height="590" alt="03-dns-resolution-failure-annotated" src="https://github.com/user-attachments/assets/a95fe719-add2-4e94-b81b-33290a079cb5" />


## 4. Correct and Verify DNS Resolution

I corrected the DNS server configuration back to `10.1.10.2` and ran `ipconfig /flushdns` to clear the DNS resolver cache. I then used `nslookup NY-DC-01` to confirm that the domain controller resolved successfully and `ping NY-DC-01` to verify connectivity with 0% packet loss.


<img width="1248" height="864" alt="04-working-dns-baseline (4)" src="https://github.com/user-attachments/assets/53602936-d94c-4c58-a9f1-c6020518ff95" />


**Tools used:** `ipconfig /all` • `nslookup` • `ipconfig /flushdns` • `ping` • Windows 11 • Windows Server • Active Directory DNS

**Result:** Successfully diagnosed a DNS resolution failure caused by an incorrect DNS server configuration, corrected the issue, and verified that hostname resolution and network connectivity were restored.

## What I Learned

I learned how important DNS is in an Active Directory environment and how an incorrect DNS server can prevent a domain client from resolving domain resources by hostname.

This lab also reinforced the importance of checking the client's network configuration first, testing DNS resolution with `nslookup`, correcting the root cause, and verifying the solution instead of assuming the issue is resolved.

**Baseline → Identify → Test → Correct → Verify**
