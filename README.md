# WLC, eWLC certificate_issue

证书问题是造成Assurance no data原因之一。

如何恢复WLC/eWLC 上的DNAC证书，参考步骤如下：

### 1. Log into CLI of DNAC: 

ssh maglev@< DNAC appliance IP> -p 2222

### 2. Run this curl command to get token to get member id:

curl -X POST -u admin:<admin user password> -H -V https://<CLUSTER-IP>/api/system/v1/identitymgmt/token

Note: For admin password, please use a back slash in your password where a special character starts if there is any special character. Example password – admin:Test!23$ will be admin:Test\!23$)
Screen Shot 2019-09-13 at 2.01.48 PM.png

  
### 3. Run this command to get member id:

curl -X GET -H "X-Auth-Token:<PROVIDE THE TOKEN HERE>" -k http://telemetry-agent.maglev-system.svc.cluster.local:8011/api/telemetry-agent/v1/membership/info

Note: Include X_Auth-Token in the command above without quotes.
Screen Shot 2019-09-13 at 2.01.33 PM.png

###  4. You should get a response like this which contains the memberID:

{"version": "x.x.x", "response": {"member_id": "5b8eb1d2dcc4be000f1ef6af"}}

