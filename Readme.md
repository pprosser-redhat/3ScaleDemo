Pre Reqs

Install the 3Scale cli
Install OpenShift oc



Manual fix up for SSO

I haven't worked out how to add a client role via the crd for the client "3scale-admin"
To fix :

    Log in to SSO as the 3scale realm admin
    select the client "3scale-admin
    click on the "Service Account Roles" tab
    In the Client Roles box, type in "realm-management" 
    Choose the "available role" "manage-clients" and move it to Assigned Roles

Due to the environment we execute in, we have to use clear instead of ssl (demo env only)

Need to make a manual adjustmment to the 3scale realm setting in SSO
    click on realm settings
    click on realm settings and change "Require SSL" to none - this is highly not recommended, and is for a demo only

If you want to show the dev portal then manually add the pages required


Account not approved error message from sso, need to make sure the emailed_verified etc is added as a mapping to the client.

if zync isn't syncing client id's might need to generate a new client for zync to use

how to get openapi doc from apicurio

http://registry.registry.router-default.apps.cluster-7g6x5.dynamic.redhatworkshops.io/apis/registry/v2/groups/philorg/artifacts/customerapi/versions/1

curl -X POST -H "X-Registry-ArtifactId: customerapi" -H "X-Registry-Version: 1" -d '{"openapi":"3.0.3","info":{"title":"Customer Management API","description":"This API allows you to manage customers in the Saas Service","contact":{"name":"Phil Prosser","url":"https://www.redhat.com","email":"pprosser@redhat.com"},"license":{"name":"Apache 2.0","url":"http://www.apache.org/licenses/LICENSE-2.0.html"},"version":"1.0.0"},"tags":[{"name":"Customer Maintenance","description":"Customer Management"},{"name":"list","description":"Query Members"},{"name":"test","description":"Test the API"}],"paths":{"/membersweb/rest/members":{"get":{"tags":["list"],"summary":"list all members","operationId":"listAllMembers","responses":{"200":{"description":"OK"}},"security":[{"apikey":[]}]},"post":{"tags":["Customer Maintenance"],"summary":"Create new member","operationId":"createMember","requestBody":{"content":{"application/json":{"schema":{"$ref":"#/components/schemas/Member"}}}},"responses":{"200":{"description":"OK"}},"security":[{"apikey":[]}]}},"/membersweb/rest/members/hello":{"get":{"tags":["test"],"summary":"Say Hello!","operationId":"hello","responses":{"200":{"description":"OK","content":{"text/plain":{"schema":{"type":"string"}}}}},"security":[{"apikey":[]}]}},"/membersweb/rest/members/{email}":{"delete":{"tags":["Customer Maintenance"],"summary":"Delete a member","operationId":"deleteMember","parameters":[{"name":"email","in":"path","required":true,"schema":{"type":"string"}}],"responses":{"200":{"description":"OK"}},"security":[{"apikey":[]}]}},"/membersweb/rest/members/{id}":{"get":{"tags":["list"],"summary":"List Member by Member ID","operationId":"lookupMemberById","parameters":[{"name":"id","in":"path","required":true,"schema":{"format":"int64","type":"integer"}}],"responses":{"200":{"description":"OK","content":{"application/json":{"schema":{"$ref":"#/components/schemas/Member"}}}}},"security":[{"apikey":[]}]}}},"components":{"schemas":{"Member":{"required":["email","phoneNumber"],"type":"object","properties":{"id":{"format":"int64","type":"integer"},"name":{"type":"string"},"firstName":{"maxLength":25,"minLength":1,"pattern":"[^0-9]*","type":"string"},"lastName":{"maxLength":25,"minLength":1,"pattern":"[^0-9]*","type":"string"},"listNames":{"$ref":"#/components/schemas/StringJoiner"},"email":{"type":"string"},"phoneNumber":{"maxLength":12,"minLength":10,"pattern":"^\\d{1,12}$","type":"string"}}},"StringJoiner":{"type":"object","properties":{"prefix":{"type":"string"},"delimiter":{"type":"string"},"suffix":{"type":"string"},"elts":{"type":"array","items":{"type":"string"}},"size":{"format":"int32","type":"integer"},"len":{"format":"int32","type":"integer"},"emptyValue":{"type":"string"}}}},"securitySchemes":{"apikey":{"type":"apiKey","description":"Authentication required to use the customer API","name":"user-key","in":"header"}}}}'  http://registry.registry.router-default.apps.cluster-xmxfd.dynamic.redhatworkshops.io/apis/registry/v2/groups/philorg/artifacts

curl -X PUT -H "X-Registry-ArtifactId: customerapi" -H "X-Registry-Version: 2" -d '{"openapi":"3.0.3","info":{"title":"Customer Management API","description":"This API allows you to manage customers in the Saas Service","contact":{"name":"Phil Prosser","url":"https://www.redhat.com","email":"pprosser@redhat.com"},"license":{"name":"Apache 2.0","url":"http://www.apache.org/licenses/LICENSE-2.0.html"},"version":"1.0.0"},"tags":[{"name":"Customer Maintenance","description":"Customer Management"},{"name":"list","description":"Query Members"},{"name":"test","description":"Test the API"}],"paths":{"/membersweb/rest/members":{"get":{"tags":["list"],"summary":"list all members","operationId":"listAllMembers","responses":{"200":{"description":"OK"}},"security":[{"apikey":[]}]},"post":{"tags":["Customer Maintenance"],"summary":"Create new member","operationId":"createMember","requestBody":{"content":{"application/json":{"schema":{"$ref":"#/components/schemas/Member"}}}},"responses":{"200":{"description":"OK"}},"security":[{"apikey":[]}]}},"/membersweb/rest/members/hello":{"get":{"tags":["test"],"summary":"Say Hello!","operationId":"hello","responses":{"200":{"description":"OK","content":{"text/plain":{"schema":{"type":"string"}}}}},"security":[{"apikey":[]}]}},"/membersweb/rest/members/{email}":{"delete":{"tags":["Customer Maintenance"],"summary":"Delete a member","operationId":"deleteMember","parameters":[{"name":"email","in":"path","required":true,"schema":{"type":"string"}}],"responses":{"200":{"description":"OK"}},"security":[{"apikey":[]}]}},"/membersweb/rest/members/{id}":{"get":{"tags":["list"],"summary":"List Member by Member ID","operationId":"lookupMemberById","parameters":[{"name":"id","in":"path","required":true,"schema":{"format":"int64","type":"integer"}}],"responses":{"200":{"description":"OK","content":{"application/json":{"schema":{"$ref":"#/components/schemas/Member"}}}}},"security":[{"apikey":[]}]}}},"components":{"schemas":{"Member":{"required":["email","phoneNumber"],"type":"object","properties":{"id":{"format":"int64","type":"integer"},"name":{"type":"string"},"firstName":{"maxLength":25,"minLength":1,"pattern":"[^0-9]*","type":"string"},"lastName":{"maxLength":25,"minLength":1,"pattern":"[^0-9]*","type":"string"},"listNames":{"$ref":"#/components/schemas/StringJoiner"},"email":{"type":"string"},"phoneNumber":{"maxLength":12,"minLength":10,"pattern":"^\\d{1,12}$","type":"string"}}},"StringJoiner":{"type":"object","properties":{"prefix":{"type":"string"},"delimiter":{"type":"string"},"suffix":{"type":"string"},"elts":{"type":"array","items":{"type":"string"}},"size":{"format":"int32","type":"integer"},"len":{"format":"int32","type":"integer"},"emptyValue":{"type":"string"}}}},"securitySchemes":{"apikey":{"type":"apiKey","description":"Authentication required to use the customer API","name":"user-key","in":"header"}}}}'  http://registry.registry.router-default.apps.cluster-xmxfd.dynamic.redhatworkshops.io/apis/registry/v2/groups/philorg/artifacts/customerapi


Any Adoptium provided JDK