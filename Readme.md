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