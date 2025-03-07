---
title: Prepare Microsoft Defender for Endpoint deployment
description: Prepare stakeholder approval, timelines, environment considerations, and adoption order when deploying Microsoft Defender for Endpoint
keywords: deploy, prepare, stakeholder, timeline, environment, endpoint, server, management, adoption
search.product: eADQiWindows 10XVcnh
search.appverid: met150
ms.prod: m365-security
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
ms.author: macapara
author: mjcaparas
localization_priority: Normal
manager: dansimp
audience: ITPro
ms.collection: 
  - M365-security-compliance
  - m365solution-endpointprotect
  - m365solution-scenario
ms.topic: article
ms.technology: mde
---

# Prepare Microsoft Defender for Endpoint deployment

[!INCLUDE [Microsoft 365 Defender rebranding](../../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint](https://go.microsoft.com/fwlink/p/?linkid=2154037)
- [Microsoft 365 Defender](https://go.microsoft.com/fwlink/?linkid=2118804)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://www.microsoft.com/microsoft-365/windows/microsoft-defender-atp?ocid=docs-wdatp-exposedapis-abovefoldlink)

Deploying Defender for Endpoint is a three-phase process:

| ![deployment phase - prepare](images/phase-diagrams/prepare.png)<br>Phase 1: Prepare | [![deployment phase - setup](images/phase-diagrams/setup.png)](production-deployment.md)<br>[Phase 2: Setup](production-deployment.md) | [![deployment phase - onboard](images/phase-diagrams/onboard.png)](onboarding.md)<br>[Phase 3: Onboard](onboarding.md) |
| ----- | ----- | ----- |
|*You are here!* | ||


You are currently in the preparation phase.


Preparation is key to any successful deployment. In this article, you'll be guided on the points you'll need to consider as you prepare to deploy Defender for Endpoint.


## Stakeholders and approval
The following section serves to identify all the stakeholders that are involved
in the project and need to approve, review, or stay informed.

Add stakeholders
to the table below as appropriate for your organization.

-   SO = Approve project

-   R = Review this project and provide input

-   I = Informed of this project

| Name                 | Role                                                                                                                                                                                                          | Action |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|
| Enter name and email | **Chief Information Security Officer (CISO)** *An executive representative who serves as sponsor inside the organization for the new technology deployment.*                                                  | SO     |
| Enter name and email | **Head of Cyber Defense Operations Center (CDOC)** *A representative from the CDOC team in charge of defining how this change is aligned with the processes in the customers security operations team.*       | SO     |
| Enter name and email | **Security Architect** *A representative from the Security team in charge of defining how this change is aligned with the core Security architecture in the organization.*                         | R      |
| Enter name and email | **Workplace Architect** *A representative from the IT team in charge of defining how this change is aligned with the core workplace architecture in the organization.*                             | R      |
| Enter name and email | **Security Analyst** *A representative from the CDOC team who can provide input on the detection capabilities, user experience, and overall usefulness of this change from a security operations perspective.* | I      |


## Environment 


This section is used to ensure your environment is deeply understood by the
stakeholders, which will help identify potential dependencies and/or changes
required in technologies or processes.

| What                                  | Description |
|---------------------------------------|-------------|
| Endpoint count                        |             |
| Server count                          |             |
| Management engine                     |             |
| CDOC distribution                     |             |
| Security information and event (SIEM) |             |


## Role-based access control

Microsoft recommends using the concept of least privileges. Defender for Endpoint leverages built-in roles within Azure Active Directory. Microsoft recommends
[review the different roles that are
available](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)
and choose the right one to solve your needs for each persona for this
application. Some roles may need to be applied temporarily and removed after the
deployment has been completed.

| Personas                     | Roles | Azure AD Role (if necessary) | Assign to |
|------------------------------|-------|-----------------------------|-----------|
| Security Administrator       |       |                             |           |
| Security Analyst             |       |                             |           |
| Endpoint Administrator       |       |                             |           |
| Infrastructure Administrator |       |                             |           |
| Business Owner/Stakeholder   |       |                             |           |

Microsoft recommends using [Privileged Identity
Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure)
to manage your roles to provide additional auditing, control, and access review
for users with directory permissions.

Defender for Endpoint supports two ways to manage permissions:

-   **Basic permissions management**: Set permissions to either full access or
    read-only. In the case of basic permissions management users with Global
    Administrator or Security Administrator role in Azure Active Directory have
    full access while the Security reader role has read-only access.

-   **Role-based access control (RBAC)**: Set granular permissions by defining
    roles, assigning Azure AD user groups to the roles, and granting the user
    groups access to device groups. For more information. see [Manage portal access using role-based access control](rbac.md).

Microsoft recommends leveraging RBAC to ensure that only users that have a
business justification can access Defender for Endpoint.

You can find details on permission guidelines
[here](https://docs.microsoft.com/microsoft-365/security/defender-endpoint/user-roles#create-roles-and-assign-the-role-to-an-azure-active-directory-group).

The following example table serves to identify the Cyber Defense Operations
Center structure in your environment that will help you determine the RBAC
structure required for your environment.

| Tier   | Description                                                                                                                                                                                                 | Permission Required |
|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|
| Tier 1 | **Local security operations team / IT team**<br>This team usually triages and investigates alerts contained within their geolocation and escalates to Tier 2 in cases where an active remediation is required.                                              |                     |
| Tier 2 | **Regional security operations team**<br>This team can see all the devices for their region and perform remediation actions.                                                                                                                        |        View data               |
| Tier 3 | **Global security operations team**<br>This team consists of security experts and is authorized to see and perform all actions from the portal. | View data <br>  Alerts investigation Active remediation actions <br> Alerts investigation Active remediation actions <br> Manage portal system settings <br> Manage security settings |



## Adoption Order
In many cases, organizations will have existing endpoint security products in
place. The bare minimum every organization should have been an antivirus solution. But in some cases, an organization might also have implanted an EDR solution already.

Historically, replacing any security solution used to be time intensive and difficult
to achieve due to the tight hooks into the application layer and infrastructure
dependencies. However, because Defender for Endpoint is built into the
operating system, replacing third-party solutions is now easy to achieve.

Choose the component of Defender for Endpoint to be used and remove the ones
that do not apply. The table below indicates the order Microsoft recommends for
how the endpoint security suite should be enabled.

| Component                               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Adoption Order Rank |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|
| Endpoint Detection & Response (EDR)     | Defender for Endpoint endpoint detection and response capabilities provide advanced attack detections that are near real-time and actionable. Security analysts can prioritize alerts effectively, gain visibility into the full scope of a breach, and take response actions to remediate threats. <br> [Learn more.](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/overview-endpoint-detection-response)                                                                                                                                                                                                                                             | 1                   |
|Threat & Vulnerability Management (TVM)|Threat & Vulnerability Management is a component of Microsoft Defender for Endpoint, and provides both security administrators and security operations teams with unique value, including: <br> - Real-time endpoint detection and response (EDR) insights correlated with endpoint vulnerabilities <br> - Invaluable device vulnerability context during incident investigations <br> -  Built-in remediation processes through Microsoft Intune and Microsoft System Center Configuration Manager <br> [Learn more](https://techcommunity.microsoft.com/t5/Windows-Defender-ATP/Introducing-a-risk-based-approach-to-threat-and-vulnerability/ba-p/377845).| 2 |
| Next-generation protection (NGP)        | Microsoft Defender Antivirus is a built-in antimalware solution that provides next-generation protection for desktops, portable computers, and servers. Microsoft Defender Antivirus includes: <br> -Cloud-delivered protection for near-instant detection and blocking of new and emerging threats. Along with machine learning and the Intelligent Security Graph, cloud-delivered protection is part of the next-gen technologies that power Microsoft Defender Antivirus.   <br> -  Always-on scanning using advanced file and process behavior monitoring and other heuristics (also known as "real-time protection"). <br> - Dedicated protection updates based on machine-learning, human and automated big-data analysis, and in-depth threat resistance research. <br> [Learn more](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-antivirus/microsoft-defender-antivirus-in-windows-10).                                                                                                                                                                                                                                                                                                                                                                       |3                   |
| Attack Surface Reduction (ASR)          | Attack surface reduction capabilities in Microsoft Defender for Endpoint help protect the devices and applications in the organization from new and emerging threats. <br> [Learn more.](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/overview-attack-surface-reduction)                                                                                                                                                                                                                                                                                                                                                                                       | 4                   |
| Auto Investigation & Remediation (AIR)  | Microsoft Defender for Endpoint uses Automated investigations to significantly reduce the volume of alerts that need to be investigated individually. The Automated investigation feature leverages various inspection algorithms, and processes used by analysts (such as playbooks) to examine alerts and take immediate remediation action to resolve breaches. This significantly reduces alert volume, allowing security operations experts to focus on more sophisticated threats and other high value initiatives. <br>[Learn more.](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/automated-investigations-windows-defender-advanced-threat-protection) | Not applicable      |
| Microsoft Threat Experts (MTE)          | Microsoft Threat Experts is a managed hunting service that provides Security Operation Centers (SOCs) with expert level monitoring and analysis to help them ensure that critical threats in their unique environments don't get missed. <br>[Learn more.](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/microsoft-threat-experts)                                                                                                                                                                                                                                                                                                                     | Not applicable      |

## Next step
|||
|:-------|:-----|
|![Phase 2: Setup](images/setup.png) <br>[Phase 2: Setup](production-deployment.md) | Set up Microsoft Defender for Endpoint deployment

