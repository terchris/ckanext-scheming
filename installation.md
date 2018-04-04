ckanext-scheming installation
=============================

This installation assumes you have followed the instructions 
[Installing CKAN from package] (http://docs.ckan.org/en/latest/maintaining/installing/install-from-package.html)

1. Become superuser
`
    sudo su
`    
2. Activate virtualenv
    . /usr/lib/ckan/default/bin/activate
3. Go to target install directory
    cd /usr/lib/ckan/default/src
4. Install from git
    pip install -e "git+https://github.com/ckan/ckanext-scheming.git#egg=ckanext-scheming"
5. Go to the ckanext-scheming dir
    cd ./ckanext-scheming
6. Install the requirements 
    pip install -r /usr/lib/ckan/default/src/ckanext-scheming/requirements.txt
7. Continue as superuser and edit the ckan config file
    vi /etc/ckan/default/production.ini
8. In the config file. Add to the end of ckan.plugins
    ckan.plugins = …….. scheming_datasets

We are now just going to test if the extension works. 
There are sample schemas are located in /usr/lib/ckan/default/src/ckanext-scheming/ckanext/scheming and we are going to use the one named ckan_dataset.json

9. To use this shema we need to set the following in the CKAN config file (production.ini)
    scheming.dataset_schemas = ckanext.scheming:ckan_dataset.json
    scheming.presets = ckanext.scheming:presets.json
    scheming.dataset_fallback = false
10. Save the config file and restart webserver so that the new config file is read.
    sudo service apache2 restart
11. Log in and open the page http://localhost/dataset/new
You should now see the dataset fields. Next we will try to edit them.

