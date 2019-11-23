[11232019]
# Magento 2 Architechture

## Module base Architechture

### there are 5 area
- adminhtml
- frontend
- base
- webapi_rest
- webapi_soap
- cron

### Nessesory files
- registration.php
- etc/module.xml
- composer.json

### Module Location
- app/code/Namespace/Module
- vendor/vendor-name/module-name
- anywhere

#### vendor/vendor-name/module-name
- installed and Update using composer
- removed when magento will be update vendor folder
- you can not manage version directly
- composer can update version
- no need technical knowladge

#### app/code/Namespace/Module
- usualy developer prefers this way

#### anywhere
- you can place your module at any where in your project

#### registration.php
