### Do step 1 to 6 in installation.md

## configuration

`vi /etc/ckan/default/production.ini`

# add scheming_organizations extension
`ckan.plugins = stats text_view image_view recline_view scheming_organizations`

# configure sceming
Add the following lines

`
#add fields to orgaizations
scheming.organization_schemas = ckanext.scheming:urbalurba_organization_member.json
scheming.presets = ckanext.scheming:presets.json
scheming.organization_fallback = false
`


## restart
`sudo service apache2 restart`


### Reset the ckan database
Do this as root (sudo bash) on the server running ckan
. /usr/lib/ckan/default/bin/activate
cd /usr/lib/ckan/default/src/ckan

paster db clean -c /etc/ckan/default/production.ini
paster db init -c /etc/ckan/default/production.ini

paster user add terchris  fullname="Terje Christensen" email=terje@smartebyernorge.no -c /etc/ckan/default/production.ini
paster sysadmin add terchris -c /etc/ckan/default/production.ini



Do these as well
sudo service apache2 restart
sudo service nginx restart

the API key is changed every time you do this. so remember to update it in scripts

# Update 30oct

cd /usr/lib/ckan/default/src/ckanext-scheming/ckanext/scheming
sudo cp urbalurba_organization_member.json urbalurba_organization_member.json-backup30oct
sudo vi new-urbalurba.json
pasted the content of urbalurba_organization_member.json in this file
sudo chown www-data:www-data new-urbalurba.json
sudo rm urbalurba_organization_member.json
sudo mv new-urbalurba.json urbalurba_organization_member.json
sudo service apache2 restart
sudo service nginx restart


# update 16Jan19

Added two new fields locationData and urbalurbaData to the org scheme
This is how to update after logging in to the server running ckan

cd /usr/lib/ckan/default/src/ckanext-scheming/ckanext/scheming
sudo cp urbalurba_organization_member.json urbalurba_organization_member.json-backup16jan19
sudo vi new-urbalurba.json
pasted the content of urbalurba_organization_member.json in this file
sudo chown www-data:www-data new-urbalurba.json
sudo rm urbalurba_organization_member.json
sudo mv new-urbalurba.json urbalurba_organization_member.json
sudo service apache2 restart
sudo service nginx restart
