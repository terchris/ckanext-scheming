ckanext-scheming installation
=============================

This installation assumes you have followed the instructions 
[Installing CKAN from package] (http://docs.ckan.org/en/latest/maintaining/installing/install-from-package.html)

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
 
10. Save the config file and restart webserver so that the new config file is read.

   `sudo service apache2 restart`

11. Log in and open the page http://localhost/dataset/new

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

OK. So now it works. Edit the ckan_dataset.json and put it back to the way it was.

