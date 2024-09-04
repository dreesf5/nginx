# Security Policy

This document provides an overview of security concerns related to NGINX deployments, focusing on confidentiality, integrity, availability, and the implications of configurations and misconfigurations.

## Latest Versions

We advise users to run the most recent mainline or stable release of nginx.

## Reporting a Vulnerability

Please report any vulnerabilities via one of the following methods
(in order of preference):

1. [Report a vulnerability](https://docs.github.com/en/code-security/security-advisories/guidance-on-reporting-and-writing-information-about-vulnerabilities/privately-reporting-a-security-vulnerability)
within this repository. We are using the Github workflow that allows us to
manage vulnerabilities in a private manner and to interact with reporters
securely.

2. [Report directly to F5](https://www.f5.com/services/support/report-a-vulnerability).

3. Report via email to security-alert@nginx.org.
This method will be deprecated in the future.

## Vulnerability Disclosures

### Private Disclosure Processes

The NGINX Community requests that all suspected vulnerabilities be reported privately via [Reporting a Vulnerability](SECURITY.md#reporting-a-vulnerability) guidelines above.

### Public Disclosure Processes

If you are aware of a publicly released vulnerability please immediately report this via the [Reporting a Vulnerability](SECURITY.md#reporting-a-vulnerability) guidelines above.  We may ask the reporter if the issue can be handled according to the private disclosure process.  If the reporter agrees, then the issue will be handled following that process.

### Confidentiality and Integrity

Vulnerabilities that compromise data Confidentiality or Integrity are considered the highest priority. Any issue leading to the loss of data confidentiality or integrity will trigger the security release process. This includes unauthorized data access, data leaks, or data manipulation through NGINX vulnerabilities.

### Availability

Availability issues must meet the following criteria to trigger the security release process:

- A core or critical module is affected (see the section on [Modules Under Scope](/SECURITY.md#modules-under-scope) for details).
- The issue must arise from traffic that the module is designed to handle. For example, a module built to secure against untrusted client traffic failing when exposed to such traffic.

- A resource exhaustion issue needs to meet these additional criteria:
  - It is not mitigated by existing timeout configurations, or applying short timeout values is impractical.
  - The issue results in highly asymmetric, extreme resource consumption.

**Note**: It is the operator's responsibility to configure NGINX according to best practices, including setting appropriate timeouts, rate limits, and resource-related features to ensure robust confidentiality, integrity, and availability.


## Trusted Configurations

In NGINX, configuration files, modules, certificate/key pairs, and NGINX JavaScript are all considered trusted sources. This means that any security issues or vulnerabilities that arise due to the loading or execution of these trusted components within NGINX are not considered vulnerabilities. Operators must ensure the security and integrity of these trusted sources.

### Risks of Misconfigurations

While NGINX considers these components trusted, misconfigurations within these files can create significant security vulnerabilities. It is the responsibility of the operator to implement configurations according to best practices, regularly review them, and apply security updates as necessary.

### Data Plane vs Control Plane
In the context of NGINX, the data plane and control plane serve distinct but complementary roles.

The data plane is responsible for handling the actual traffic that flows through NGINX, including processing client requests, routing them to the appropriate backend servers, and returning responses. This plane directly interacts with user data, making it critical for performance, security, and reliability. NGINX inherently trusts the content and instructions provided by upstream servers. If an upstream server issues a command NGINX is designed to support, NGINX will execute that command, relying on the integrity and security of the upstream server’s content.

The control plane, on the other hand, is concerned with the configuration, management, and orchestration of NGINX itself. The control plane does not directly handle traffic but instead governs how the data plane operates. Misconfigurations or vulnerabilities in the control plane can lead to improper behavior in the data plane, potentially exposing the system to attacks or mismanagement.

## Modules Under Scope
This applies to all default, standard and recommended modules. For each module, detailed security considerations and potential attack vectors will be identified, alongside recommended configurations to mitigate risks.

## Debug Logging and Core Files
Debug logs and core files produced by NGINX may contain un-sanitized data, including sensitive information like client requests, server configurations, and private key material. These artifacts are useful for troubleshooting and  must be handled with care to avoid exposing confidential data.

## Fix and Release Process

When an issue is reported it is immediately triaged.  This often takes some time and we will communicate with the reporter as needed.  

Fixes are created and tested by the core team using a Github private fork for security.  If needed, we will invite the reporter to contribute to the fork and help the team solve and validate the solution.

### Released Versions

All security fixes will be applied to all supported stable releases as well as main, as applicable.  See [releases.md]

## Vulnerability Fix Disclosure Processes

NGINX is committed to responsibly disclosing information that contains sufficient detail about the vulnerability in question, such as the CVSS score and vector.

### Embargo Policy

All privately disclosed vulnerabilities are embargoed by default.  All communications and fixes are kept private until the fix is released and made public.

Because NGINX is a project supported by F5, we also generally follow the policy as documented in [K4602: Overview of the F5 security vulnerability response policy](https://my.f5.com/manage/s/article/K4602)

## Fix and Disclosure SLOs

The following Service Level Objectives (SLOs) 

* All vulnerability disclosures will be responded to within one (1) business day.

* Fixes will be developed and released within 90 days from the date of disclosure.  If the fix is difficult such that an extension will be needed, the core team will work with the disclosing person for that extension.

* Publicly disclosed (i.e. Zero-Day vulnerabilities) will be addressed ASAP.

