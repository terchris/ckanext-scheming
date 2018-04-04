ckanext-scheming configuration
==============================

ckanext-scheming has several configuration files and parameters that relate to eachother. This is how it works.

# Walkthrugh of the config used in the installation

It starts with the CKAN config file production.ini. Here we added scheming_datasets to the end of the ckan.plugins:

`ckan.plugins = …….. scheming_*datasets*`

The scheming_*datasets* tells CKAN that we are goiing to use scheming on the *datasets*. This has ckanext-scheming looking for the config line that tells it what shema to use for a **dataset**.

`
scheming.**dataset**_schemas = ckanext.scheming:ckan_dataset.json
`
