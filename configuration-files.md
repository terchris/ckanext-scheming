ckanext-scheming configuration files
====================================

ckanext-scheming has several configuration files and parameters that relate to eachother. This is how it works.

# Walkthrugh of the config used in the installation (dataset)

It starts with the CKAN config file production.ini. Here we added scheming_*datasets* to the end of the ckan.plugins:


ckan.plugins = …….. scheming_*datasets*

The scheming_*datasets* tells CKAN that we are going to use scheming on the *datasets*. This has ckanext-scheming looking for the config line that tells it what shema to use for a **dataset**.


scheming.**dataset**_schemas = ckanext.scheming:ckan_dataset.json

The above line tells ckanext-scheming that when a **dataset** is edited or displayed it will use the schema defined in the file ckan_dataset.json

Explanation of the different parts: 
```
scheming.dataset_schemas = ckanext.scheming:ckan_dataset.json

scheming. -> config parameter belonging to ckanext-scheming
dataset_schemas = -> the schema is for datasets and mot groups or organizations
ckanext.scheming: => (no idea, ??)
ckan_dataset.json => the schema file that will be used for datasets
```

The file ckan_dataset.json located in /usr/lib/ckan/default/src/ckanext-scheming/ckanext/scheming/

And  looks like this:
```
{
  "scheming_version": 1,
  "dataset_type": "dataset",
```

The dataset_type is set to “dataset” this means that the schema will be used on all /dataset url’s eg https://data.gov.uk/dataset/national-statistics-postcode-lookup-uk/resource/3206f3b9-854a-46ec-8fd2-a6823e836b65


In the CKAN production.ini there are two more lines.
```
scheming.presets = ckanext.scheming:presets.json
scheming.dataset_fallback = false
```
TODO: Explain what they do



# Configuration for organization

To do scheming on a organization we must tell ckanext-scheming that we are doing so. This is done by adding scheming_*organizations* to ckan.plugins.


ckan.plugins = …….. scheming_datasets scheming_*organizations*

The scheming_*organizations* tells CKAN that we are going to use scheming on the *organizations*. This has ckanext-scheming looking for the config line that tells it what shema to use for a **organization**.


scheming.**organization**_schemas = ckanext.scheming:org_with_dept_id.json

The above line tells ckanext-scheming that when a **organization** is edited or displayed it will use the schema defined in the file org_with_dept_id.json

Explanation of the different parts: 
```
scheming.organization_schemas = ckanext.scheming:org_with_dept_id.json

scheming. -> config parameter belonging to ckanext-scheming
organization_schemas = -> the schema is for organization and mot groups or datasets
ckanext.scheming: => (no idea, ??)
org_with_dept_id.json => the schema file that will be used for organizations
```

The file org_with_dept_id.json located in /usr/lib/ckan/default/src/ckanext-scheming/ckanext/scheming/

And  looks like this:
```
{
  "scheming_version": 1,
  "organization_type": "organization",
```

The organization_type is set to "organization" this means that the schema will be used on all /organization url’s eg http://localhost/organization/new


In the CKAN production.ini there are two more lines.
```
scheming.presets = ckanext.scheming:presets.json
scheming.organization_fallback = false
```
TODO: Explain what they do






# Configuration for group

To do scheming on a group we must tell ckanext-scheming that we are doing so. This is done by adding scheming_*groups* to ckan.plugins.


ckan.plugins = …….. scheming_*groups*

The scheming_*groups* tells CKAN that we are going to use scheming on the *groups*. This has ckanext-scheming looking for the config line that tells it what shema to use for a **group**.


scheming.**group**_schemas = ckanext.scheming:custom_group_with_status.json

The above line tells ckanext-scheming that when a **group** is edited or displayed it will use the schema defined in the file custom_group_with_status.json

Explanation of the different parts: 
```
scheming.group_schemas = ckanext.scheming:custom_group_with_status.json

scheming. -> config parameter belonging to ckanext-scheming
group_schemas = -> the schema is for group
ckanext.scheming: => (no idea, ??)
custom_group_with_status.json => the schema file that will be used for groups
```

The file custom_group_with_status.json located in /usr/lib/ckan/default/src/ckanext-scheming/ckanext/scheming/

And  looks like this:
```
{
  "scheming_version": 1,
  "group_type": "theme",
```
TODO: I don't understand why the group_type is theme and not group ... yet

In the CKAN production.ini there are two more lines.
```
scheming.presets = ckanext.scheming:presets.json
scheming.group_fallback = false
```
TODO: Explain what they do



# Configuration for user
It is not **not** possible to use schema on a user