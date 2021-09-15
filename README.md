# WLC, eWLC certificate_issue

证书问题是造成Assurance no data原因之一。

如何恢复WLC/eWLC 上的DNAC证书，参考步骤如下：

### 1. Log into CLI of DNAC: 

ssh maglev@< DNAC appliance IP> -p 2222

### 2. Run this curl command to get token to get member id:

curl -X POST -u admin:<admin user password> -H -V https://<CLUSTER-IP>/api/system/v1/identitymgmt/token

```
curl -X POST -u atxadmin:password -H -V https://1.1.1.1/api/system/v1/identitymgmt/token
{"Token":"eyJ0eX...(token)...WCdSRYA"}
[Tue Sep 14 23:53:12 UTC] maglev@1.1.1.1 (maglev-master-100-1-1-10) ~

```
  
- curl -u 后面紧跟的是 DNAC GUI 的用户名（默认是admin）和密码，如果密码有特殊字符，则需在该字符前加“\“。
- 1.1.1.1 为DNAC IP 地址  
  
  
### 3. Run this command to Re Provision the certificate for WLC:

curl -X GET -H "Content-Type: application/json" -H "X-Auth-Token:<PROVIDE THE TOKEN HERE>" -k https://1.1.1.1/api/v1/wireless-telemetry/provision/wlc/2.2.2.2

```curl -X POST -H "X-Auth-Token:eyJ0eX...(token)...WCdSRYA" -H "Content-Type:application/json" -k  https://10.124.38.150/api/v1/wireless-telemetry/provision/wlc/100.1.1.21

```
- 2.2.2.2 为 WLC IP 地址    
- Note: Include X_Auth-Token in the command above without quotes.

###  4. You should get a response like this with task ID:

{"Task ID for WLC Network Assurance provision":"4fa56353-b7d0-41e5-b5d9-f622e7a07616"}  

显示OK。
