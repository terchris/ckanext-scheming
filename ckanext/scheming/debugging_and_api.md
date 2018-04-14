ckanext-scheming debugging
==========================

When you add fields to a dataset, organization or group it is nessesary to see what the field names are.


# List all organizations and their fields

The API for listing organizations is [ckan.logic.action.get.organization_list(context, data_dict)](http://docs.ckan.org/en/latest/api/index.html#ckan.logic.action.get.organization_list)

This curl does the magic:
```
    curl -X POST http://localhost/api/3/action/organization_list \
-d '{"all_fields": "True", "include_extras": "True", "include_users": "True"}'

 ```

 This is another API sor displaying info about an organization
 http://docs.ckan.org/en/latest/api/index.html#ckan.logic.action.get.organization_show


 API for displaying user info
 http://docs.ckan.org/en/latest/api/index.html#ckan.logic.action.get.user_show
 
