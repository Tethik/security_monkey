Google SSO Setup Guide
======================

This document describes how to set up the Google SSO. There are two authentication
methods made available, a "People" and a "Directory" method. The former uses
just a normal oauth login to sign your user in. The latter uses an oauth login
and a service account, it is a bit trickier to set up but offers a bit more 
flexibility. 

If you want to restrict access to just your own hosted domain, the "People" option
will be good enough. However if you want to only authorize users within a certain
group, and users for example do not have permission to read groups, then the
"Directory" option will work for you. 

Essentially the "Directory" option set up it's own api key as a service, and you
authorize it as it's own account. No oauth scopes necessary. With the "People" 
option you use the users' own `access_token` to call the APIs.

## TODO
revert People group scope
pictures!

People Setup
------------

```
GOOGLE_AUTH_API_METHOD = 'People' 
GOOGLE_DEFAULT_ROLE = "View" # anonymous, View, Comment, Justify, and Admin are valid roles.
GOOGLE_IS_MANAGING_ROLES = True

GOOGLE_CLIENT_ID = '<id>.apps.googleusercontent.com'
GOOGLE_AUTH_ENDPOINT = ''
GOOGLE_SECRET = '<secret from >'
GOOGLE_HOSTED_DOMAIN = 'example.org'
```



Directory Setup
---------------


```
GOOGLE_AUTH_API_METHOD = 'People' 
GOOGLE_DEFAULT_ROLE = "View" # anonymous, View, Comment, Justify, and Admin are valid roles.
GOOGLE_IS_MANAGING_ROLES = True

GOOGLE_CLIENT_ID = '<id>.apps.googleusercontent.com'
GOOGLE_AUTH_ENDPOINT = os.getenv('SECURITY_MONKEY_GOOGLE_AUTH_ENDPOINT', '')
GOOGLE_SECRET = os.getenv('SECURITY_MONKEY_GOOGLE_SECRET', '')
GOOGLE_HOSTED_DOMAIN = os.getenv('SECURITY_MONKEY_GOOGLE_HOSTED_DOMAIN', '') # Verify that token issued by comes from domain

GOOGLE_ADMIN_ROLE_GROUP_NAME = '' # Google group name which should map to security-monkey role Admin
GOOGLE_DOMAIN_WIDE_DELEGATION_KEY_PATH = "/usr/local/src/security_monkey/env-config/secret.json" 
# GOOGLE_DOMAIN_WIDE_DELEGATION_KEY_JSON = # alternatively you can set the JSON as a string directly.
GOOGLE_DOMAIN_WIDE_DELEGATION_SUBJECT = 'service.account@example.com' # perform google directory api calls with this as the subject
```



