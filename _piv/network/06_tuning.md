---
layout: page
collection: piv
title: Network Tuning
permalink: piv/network/tuning/
sticky_sidenav: true
sidenav: pivnetwork

subnav:
    - text: Cached Logon Credential Limit
      href: '#cached-logon-credential-limit'
    - text: CRL Retrieval Timeout Settings
      href: '#crl-retrieval-timeout-settings'
    - text: OCSP Response Caching Behavior
      href: '#ocsp-response-caching-behavior'
---

You can tune the network domain settings to help you and your users have a better experience and reduce errors.  This section highlights some of the _common_ tuning configurations for network domain logon.  There are additional tuning configurations and we encourage you to start with these first and contribute others.      

You can also send questions to the ICAM Technology listserve (email to ICAM-COMMUNITY-TECH at listserv.gsa.gov) to ask your government colleagues for their additional tips and tricks!

### Cached Logon Credential Limit
When a user authenticates to a Windows system, their logon credentials are cached to enable logon in the event the domain controller is unavailable. The [United States Government Configuration Baseline (USGCB) for Windows 7](https://usgcb.nist.gov/usgcb/microsoft/download_win7.html){:target="_blank"}{:rel="noopener noreferrer"} specifies that ***Interactive logon: Number of previous logons to cache (in case domain controller is not available)*** should be set to ***2***. 

There are no required USGCB settings for _Windows 8_ or _Windows 10_.  

You should configure the cached logon credential limit to be at least "2" and _possibly more_ depending on the mission needs.  

The ***Number of previous logons to cache*** can be modified in local or group policy in the following location
***Computer Configuration\Windows Settings\Security Settings\Local Policies\Security options***

More information is available on [Microsoft TechNet](https://technet.microsoft.com/en-us/library/jj852209%28v=ws.11%29.aspx){:target="_blank"}{:rel="noopener noreferrer"}

### CRL Retrieval Timeout Settings
By default, Windows will time out when downloading Certificate Revocation List(s) after 15 seconds. A number of CRLs in the government environment are large, greater than 20 MB in size, which will lead to the timeout happening.  This example scenario can be common and a source of frustration to you and your users:  

- The first or the 51st user will attempt to log on in the morning in a region 
- The validity period and cache of the previous CRL will have expired on the domain controller
- The domain controller will attempt to download the large CRL file and will hit the timeout limit
- The user will receive an authentication failure (unable to log on) 
- The user will be able to try again and be successful
- You will try to determine the root cause to diagnose the failures (i.e., chasing ghosts on the network)
- This process will repeat

You want to tune _both_ the OCSP Response Caching Behavior setting and the CRL Retrieval Timeout Settings.  

The default timeout value can be modified using local or group policy by modifying the ***Default URL retrieval timeout*** value found in the ***Certificate Path Validation Settings***, ***Network Retrieval***  tab, located in ***Computer Configuration\Windows Settings\Security Settings\Public Key Policies***

Consult these step-by-step instructions:&nbsp; [Manage Network Retrieval and Path Validation](https://technet.microsoft.com/en-us/library/cc771429%28v=ws.11%29.aspx){:target="_blank"}{:rel="noopener noreferrer"}

### OCSP Response Caching Behavior
By default, Microsoft Windows will retrieve and cache 50 OCSP Responses for any one issuing CA before switching to CRL mode. Depending on the size of the CRL, this may be a poor performance decision. For environments where workstations routinely interact with large CRLs, a large value may signficantly reduce network bandwidth consumption.  This value can be increased by setting the ***CryptnetCachedOcspSwitchToCrlCount*** DWORD value in the following registry key:
***HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\SystemCertificates\ChainEngine\Config***

Source:&nbsp; [Optimizing the Revocation Experience](https://technet.microsoft.com/en-us/library/ee619783%28v=ws.10%29.aspx){:target="_blank"}{:rel="noopener noreferrer"}
