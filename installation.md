ckanext-scheming installation
=============================

This installation assumes you have followed the instructions
[Installing CKAN from package](http://docs.ckan.org/en/latest/maintaining/installing/install-from-package.html)

# Install it

1. Become superuser

   `sudo su`

2. Activate virtualenv

   `. /usr/lib/ckan/default/bin/activate`

3. Go to target install directory

   `cd /usr/lib/ckan/default/src`

4. Install from git

   `pip install -e "git+https://github.com/ckan/ckanext-scheming.git#egg=ckanext-scheming"`

5. Go to the ckanext-scheming dir

   `cd ./ckanext-scheming`

6. Install the requirements

   `pip install -r /usr/lib/ckan/default/src/ckanext-scheming/requirements.txt`

7. Continue as superuser and edit the ckan config file

   `vi /etc/ckan/default/production.ini`

8. In the config file. Add to the end of ckan.plugins

   `ckan.plugins = …….. scheming_datasets`

We are now just going to test if the extension works.
There are sample schemas are located in /usr/lib/ckan/default/src/ckanext-scheming/ckanext/scheming and we are going to use the one named ckan_dataset.json

9. To use this shema we need to set the following in the CKAN config file (production.ini)
```
    scheming.dataset_schemas = ckanext.scheming:ckan_dataset.json
    scheming.presets = ckanext.scheming:presets.json
    scheming.dataset_fallback = false
 ```
 
10. It was done with root user. So set access rights to www-data

 `sudo service apache2 restart`

11. Save the config file and restart webserver so that the new config file is read.

   `chown -R www-data:www-data /usr/lib/ckan/`

12. Log in and open the page http://localhost/dataset/new

   You should now see the dataset fields. Next we will try to edit them.

# Test it

1. Open the schema file that defines the fields

   `sudo vi /usr/lib/ckan/default/src/ckanext-scheming/ckanext/scheming/ckan_dataset.json`

2. Change the form_placeholder so you have something like this:
```
  "dataset_fields": [
    {
      "field_name": "title",
      "label": "Title",
      "preset": "title",
      "form_placeholder": "I EDITED THIS eg. A descriptive title"
    },
```
3. Save, restart the webserver and open http://localhost/dataset/new again.
   You should now see the “I EDITED THIS…” in the Title placeholder.


# Verify it

The shema ckan_dataset.json has all the fields that are defined for a dataset by default. No new fields and all fields corresponds with default field names.

Do this simple test to verify:

1. Create a dataset without the ckan_dataset.json schema
2. Create a dataset with the ckan_dataset.json schema
3. Verify that updating fields with or without the schema has the same result.

OK. So now it works. Edit the ckan_dataset.json and put it back to the way it was.



# Notes

When you use the API to read the object you will get the field names in the schema. as keypairs.
When you remove the field definition:
- The fields are still there
- when using the API you will see a key called "extras". In this arrayyou will find the filelds like this
   {key:myemail, value:"myemail@somedomain.com"}