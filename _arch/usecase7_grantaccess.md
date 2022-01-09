---
layout: page
title: 7. Grant Access
collection: arch
permalink: /arch/grantaccess/
sidenav: archusecases
sticky_sidenav: true
---

[![This use case corresponds to the Authentication and Authorization service areas of Access Management.]({{site.baseurl}}/assets/arch/usecases/Access-AuthnAuthz.png){:align="right" style="padding-left:15px"}]({{site.baseurl}}/assets/arch/usecases/Access-AuthnAuthz.png){:target="_blank"}{:rel="noopener noreferrer"}

This use case describes the steps to authenticate individuals and authorize access to agency services. Agency services can be anything from applications and files to physical facilities.

---

## Use Case

In this use case, an Access Control System (ACS) Administrator needs to grant access to an employee or contractor who has an enterprise identity and active credential and needs to access a logical or physical resource. These steps assume the employee or contractor already has credentials to support authentication as well as the access entitlements to support authorization decisions.

- *Authentication* - I want to verify the claimed unique identity of a given employee or contractor  so that the system can verify the right individual is attempting to access an agency service. 
- *Authorization* - I want to allow access for only employees and contractors that meet established requirements so that only the people who should have access do have access.

[![Icon Key for the diagrams that follow.]({{site.baseurl}}/assets/arch/usecases/7-IconKey.png)]({{site.baseurl}}/assets/arch/usecases/7-IconKey.png){:target="_blank"}{:rel="noopener noreferrer"}

<style>

td {
  font-family: "Cambria", "Georgia", "Times New Roman", "Times", serif;
  vertical-align:top;
}

</style>

<table>
  <tr>
    <td style="width:250px;border:0px;"><strong>1. Access Attempt</strong> <br> <a href="{{site.baseurl}}/assets/arch/usecases/7-1.png" target="_blank" rel="noopener noreferrer"><img src="{{site.baseurl}}/assets/arch/usecases/7-1.png" width="250" alt="A diagram showing an employee or contractor attempting to access a agency service through an access control system."></a></td>
    <td style="border:0px;">An employee or contractor attempts to access an agency service.</td>
  </tr>
  <tr>
    <td style="width:250px;border:0px;"><strong>2. Authenticate the employee or contractor</strong> <br> <a href="{{site.baseurl}}/assets/arch/usecases/7-2.png" target="_blank" rel="noopener noreferrer"><img src="{{site.baseurl}}/assets/arch/usecases/7-2.png" width="250" alt="A diagram showing an employee or contractor presenting either an IAL2 or IAL3 authenticator to an access control system."></a></td>
    <td style="border:0px;">The employee or contractor presents an authenticator to the ACS that meets the protected resource’s minimum assurance requirements:<ul><li><strong>AAL2</strong> (two-factor) - Something you know + something you have, like a one-time passcode.</li><li><strong>AAL3</strong> (two-factor + hardware) - Something you know + something you have, like a one-time passcode generated by a hardware-based authenticator; or a PIV credential. For more information about AAL values, see <a href="https://pages.nist.gov/800-63-3/sp800-63b.html#sec5" target="_blank" rel="noopener noreferrer">NIST SP 800-63B Section 5: Authenticator and Verifier Requirements</a>.</li></ul></td>
  </tr>
  <tr>
    <td style="width:250px;border:0px;"><strong>3. Determine the access entitlements and access requirements</strong> <br> <a href="{{site.baseurl}}/assets/arch/usecases/7-3.png" target="_blank" rel="noopener noreferrer"><img src="{{site.baseurl}}/assets/arch/usecases/7-3.png" width="250" alt="A diagram showing an access control system determining the access entitlements and access requirements."></a></td>
    <td style="border:0px;">Upon successful authentication, the ACS identifies 1) The employee or contractor's access entitlements associated with the protected resource, and 2) The protected resource's access requirements.</td>
  </tr>
  <tr>
    <td style="width:250px;border:0px;"><strong>4. Process the access information</strong> <br> <a href="{{site.baseurl}}/assets/arch/usecases/7-4.png" target="_blank" rel="noopener noreferrer"><img src="{{site.baseurl}}/assets/arch/usecases/7-4.png" width="250" alt="A diagram showing an access control system processing the employee or contractor access entitlements to the protected resources's access requirements."></a></td>
    <td style="border:0px;">The ACS compares the employee or contractor’s access entitlements to the protected resource’s access requirements to decide whether to authorize access.</td>
  </tr>
  <tr>
    <td style="width:250px;border:0px;"><strong>5. Grant access</strong> <br> <a href="{{site.baseurl}}/assets/arch/usecases/7-5.png" target="_blank" rel="noopener noreferrer"><img src="{{site.baseurl}}/assets/arch/usecases/7-5.png" width="250" alt="A diagram showing an access control system granting access to an employee or contractor."></a></td>
    <td style="border:0px;"> If the employee or contractor meets the protected resource’s access requirements, the ACS grants access to the protected resource.<br><br>The ACS logs the access attempt and decision for auditing purposes.</td>
  </tr>
</table>

## Example

An employee on the financial review team attempts to access a government financial application that is secured by a single sign-on (SSO) solution. The employee clicks a link to the financial application and is redirected to the SSO portal. The employee authenticates using his/her provided credential, which the SSO determines to be valid. The SSO solution or the financial application system finds the employee’s enterprise identity account and compares the roles assigned to those allowed by the financial application. The resulting determination is that the employee has authenticated to the required assurance level and has the appropriate entitlements to access the system and is subsequently logged on.