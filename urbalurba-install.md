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

the API key is changed every time you do this. so remember to update it in scripts