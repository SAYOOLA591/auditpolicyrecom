# Baseline Microsoft Security Auditing with Group Policy Management

By default, Windows systems only log a limited set of events, resulting in significant visibility gaps. For example, many environments are not following the recommendations, and default auditing may miss critical actions, such as privilege escalation, Kerberos abuse, or lateral movement. I'll show you what you can enable to follow Microsoft's Audit Policy recommendations, and I'll also include the link below.

To address this, Microsoft provides recommended audit policy baselines that can allow administrators within the domain to just simply update a single policy and push it out to multiple computers within that domain saving a lot of time because you can imagine how long it would take to manually configure a workstation one by one especially if you have let's say 500 workstations so instead of doing that manually we can use GPO policy to push it across devices to do that we want to click on the Start menu and search for a group Policy Management.

[Policy Recommendation](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/security-best-practices/audit-policy-recommendations)

# Why It Matters

- Enhanced visibility - Detects brute force, privilege escalation, and Kerberoasting.
- Incident response ready - Analysts have the necessary logs to investigate attacks.
- Compliance alignment - Meets security standards (CIS, NIST, ISO).

# Key Categories to Enable

- Logon/Logoff (4624, 4625, 4634)
- Account Management (4720–4726, 4728)
- Directory Service Access (4662)
- Policy Changes (4739, 4719)
- Process Creation (4688)

# Takeaway

Organizations should move away from default Windows auditing and adopt Microsoft’s baseline GPO for security logging. ensuring their SIEM and SOC teams have the correct data at the right time, closing detection gaps and strengthening their defenses.
# 

# Recommended System Audit Policy by operating system

We will review the recommended audit policies by operating system and categorise them accordingly. To proceed, access our Active Directory Domain Controller (ADDC) and open the Group Policy Management console. Under the forest containing our domain name, navigate to the domain section. From there, create a new policy. Right-click on the new policy and select "Edit." Name the new policy "Audit Policy - Endpoint."

Next, go to the policies section, choose Windows Settings, then Security Settings, and finally select Advanced Audit Policy Configuration. This is where we will configure all our baseline settings.

![gpo-recomm1](https://github.com/user-attachments/assets/82e195cc-c509-4ba7-8e2d-379c01765290)

![gpo-recom2](https://github.com/user-attachments/assets/b1071f1f-8202-425d-b32c-058a21069ab8)

Account Logon Tracking

![account-logon1](https://github.com/user-attachments/assets/21181873-af40-4901-b2cf-0b6287a2a25e)

![account-logon2](https://github.com/user-attachments/assets/6acd060c-9820-4baf-96f3-357bdc555602)

Account Management Tracking

![account-managem1](https://github.com/user-attachments/assets/e2c88296-bd25-48c8-93f7-f7708e5088aa)

![account-managem2](https://github.com/user-attachments/assets/74d12112-5269-49f2-a81b-0b796e7739aa)

Detailed Tracking

![details-tracking1](https://github.com/user-attachments/assets/5d164bd2-a189-44f2-acb0-20ce00ee717f)

![details-tracking2](https://github.com/user-attachments/assets/09135ccc-2816-4175-bd46-76e2e2a0637f)

Logon and Logoff Tracking

![logon-logof1](https://github.com/user-attachments/assets/cc6058da-d6fe-4805-94be-9783c517b8d2)

![logon-logof1](https://github.com/user-attachments/assets/212bb5d0-23e9-4597-a76c-64271af8f26b)

Policy Change Tracking

![policy-change1](https://github.com/user-attachments/assets/e9685810-45c2-4963-bb75-7c26d1a6f223)

![policy-change12](https://github.com/user-attachments/assets/6ba862a1-1684-4a6e-a20a-56b7d4411a05)

System Tracking

![system-track](https://github.com/user-attachments/assets/3dafb84b-7254-4187-8787-66d1b5c73a62)

![system-track2](https://github.com/user-attachments/assets/5fc6e494-89af-4fa1-9820-755a79f80745)
#

In addition to enabling all the baseline recommendations, we must also allow process tracking, because without process tracking, event ID 4688 is not as effective as it should be.

For example, let me go ahead and search up Event ID 4688, so by default, if we enable 4688, it will log the process name, but take a look at the process command line it's empty so without enabling process tracking you essentially miss out on a lot of information that is why we must allow process tracking.

By Default

![default-tracking](https://github.com/user-attachments/assets/f9f42e4b-77f8-427e-b0f0-5ca34f29d8f1)

After Process Logging

![after-tracking](https://github.com/user-attachments/assets/ec393f62-381a-4234-bbff-fa316a5c5ee0)

So now we have everything pretty much good to go and just remember that we should enable Powershell logging as well just in case and to do that I'll Scroll down and expand Windows Components what we want to look for is Windows Powershell which is right here and we have Turn Module Logging Script Block Logging this one is the Event ID 4104 I'll click on enabled. I'll log the start and stop event and apply OK.

![powershel-log](https://github.com/user-attachments/assets/b729b754-2422-4b89-b076-1b0fe4f23f6e)

# Advanced Audit Policy Configuration Settings

The final crucial step involves ensuring that the audit force audit policy is enabled when using advanced audit policy configuration settings. Since we utilized these advanced configurations, we manually set up the specific items we want to audit. This means we need to enable the audit force audit policy setting. 

To locate this setting, navigate to Local Policy and then select Security Options. Look for the "Audit Force" option. Once you find it, double-click on it to access the policy settings, and select "Enabled."

![audit-policy1](https://github.com/user-attachments/assets/985a3b7b-6ff6-412c-9429-ad1107915829)
![audit-policy](https://github.com/user-attachments/assets/a996610b-d46f-427a-b29e-067dbd52fb41)

#
We need to link our Baseline Security Auditing GPO to our OU. By enabling this, all our workstations/endpoints will automatically collect the update.

![gpo-OU](https://github.com/user-attachments/assets/867db7d3-f7db-4e44-917a-42ae4f1c1356)

---

# Conlusion

In this lab, we successfully demonstrated the importance of applying Microsoft Security Baselines within an enterprise environment. By reviewing the recommendations, we gained a deeper understanding of their significance and identified the key audit categories that need to be enabled for proper oversight and comprehensive event logging.

To enhance visibility, we manually configured and enforced the Advanced Audit Policy, ensuring that critical security events are captured without any gaps. As a final step, we linked the Baseline Security Auditing Group Policy Object (GPO) to our target Organizational Unit (OU). This allows for policy updates to be automatically deployed across all domain-joined endpoints and workstations, thereby maintaining a consistent and centralized security posture.







































