# strongSwan.configurations
Basic strongSwan server end configurations for Apple devices

# Function
Set up a client-server mode IPsec connection.

# Parameter interpretation
Refer the official website of storngSwan for more information.

# Contents
1) `ipsec.conf.roadwarrior` file is the most simple configration for roadwarrior mode. 
2) `ipsec.conf.roadwarrior.certificate.mode` is the configration for roadwarrior mode, but additionaly to authorize clients via certificates. 
3) `ipsec.conf.site2site.certificate.mode` is the configuration for site-to-site (gateway-to-gateway) IPsec mode, with the authernticatio based on certificates.
4) `ipsec.conf.passthrough` is the configuration to exlcude some traffics from the tunnel (especially under site-to-site mode), called passthrough policy.
5) `private.key.generation` file is the syntax to create private keys for strongSwan. 
6) `public.key.generation` file is the syntax to create public keys for strongSwan. 
7) `public.key.request` file is the syntax to create a public key issueing request for strongSwan.
8) Other mode is to be update in future.

# Notice
1) Make sure the proper privileges of related files for security considerations. 
2) Make appropriate modifications to the original code based on your needs.
3) To be able to create private and public keys, install `strongswan-pki` package first.
4) To use the eap-tls authentication, the eap-tls plugin must be installed and enabled. To install and enable this plugin, run command `apt install libcharon-extra-plugins`.

# Appendixes
```
# Diffie-Hellman Groups
```
|Diffie-Hellman Group Number|Diffie-Hellman Group Name|RFC|Predefined|
| - | - | - | - |
|Group 1 |768-bit modulus MODP Group                           |RFC 7296|Yes|
|Group 2 |1024-bit modulus MODP Group                          |RFC 7296|Yes|
|Group 5 |1536-bit modulus MODP Group                          |RFC 3526|Yes|
|Group 14|2048-bit modulus MODP Group                          |RFC 3526|Yes|
|Group 15|3072-bit modulus MODP Group                          |RFC 3526|No |
|Group 16|4096-bit modulus MODP Group                          |RFC 3526|No |
|Group 17|6144-bit modulus MODP Group                          |RFC 3526|No |
|Group 18|8192-bit modulus MODP Group                          |RFC 3526|No |
|Group 19|256-bit random Elliptic Curve Group                  |RFC 5903|Yes|
|Group 20|384-bit random Elliptic Curve Group                  |RFC 5903|Yes|
|Group 21|521-bit random Elliptic Curve Group                  |RFC 5903|Unknown|
|Group 24|2048-bit MODP Group with 256-bit Prime Order Subgroup|RFC 5114|No |

```
# Supported RDN Types
```
|Identifier|OID|Description|Example|
| - | - | - | - |
|**1) Defined by X.520 and also described in RFC 4519**|
|CN|2.5.4.3|Common Name|vpn.strongswan.org or John Smith|
|S|2.5.4.4|Surname|Smith|
|SN, serialNumber|2.5.4.5|Serial Number|ZX52376|
|C|2.5.4.6|Country (ISO 3166 two-letter code)|CH|
|L|2.5.4.7|Locality|Rapperswil|
|ST|2.5.4.8|State or Province|St. Gallen|
|street|2.5.4.9|Street Address|Oberseestrasse 10|
|O|2.5.4.10|Organization|strongSwan Project|
|OU|2.5.4.11|Organizational Unit|Research|
|T|2.5.4.12|Title|Software Engineer|
|D|2.5.4.13|Description|Main VPN gateway|
|postalAddress|2.5.4.16|Postal Address|Oberseestrasse 10 8640 Rapperswil Switzerland|
|postalCode|2.5.4.17|Postal Code|8640|
|N|2.5.4.41|Name (should not be used directly)||
|G|2.5.4.42|Given Name|John|
|I|2.5.4.43|Initials|J. T.|
|ID|2.5.4.45|Unique Identifier||
|dnQualifier|2.5.4.46|DN Qualifier (e.g. a timestamp or serial number)|20190214115113Z or 51314E|
|dmdName|2.5.4.54|DMD Name||
|pseudonym|2.5.4.65|Pseudonym||
|**2) Originally defined by RFC 1274 now described in RFC 4519**|
|UID|0.9.2342.19200300.100.1.1|User ID|jsmith|
|DC|0.9.2342.19200300.100.1.25|Domain Component (label of a DNS domain name)|strongswan or org but not strongswan.org|
|3) Defined by RFC 2798|
|EN|employeeNumber|2.16.840.1.113730.3.1.3|Employee Number|42|
|**4) Defined in PKCS#9 and described in RFC 2985**|
|E, email, emailAddress|1.2.840.113549.1.9.1|Email Address (deprecated according to RFC 5280, use SAN instead)|alice@strongswan.org|
|UN, unstructuredName|1.2.840.113549.1.9.2|Unstructured Name||
|UA, unstructuredAddress|1.2.840.113549.1.9.8|Unstructured Address||
|**5) Defined by "Zertifikatsformate im Zertifizierungsbereich PKS II"**|
|ND|0.2.262.1.10.7.20|Name Distinguisher (Number incremented for equal CNs)||
|**6) Unknown origin (was added with FreeS/WAN 0.9.9)**|
|TCGID|1.3.6.1.4.1.1201.1.1.2.2.75|Siemens Trust Center Global ID||
