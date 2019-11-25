[11232019]
# Magento 2 Architechture

## Module base Architechture

### there are 5 area in magento
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
- app/etc/NonComposerComponentRegistration.php included by magento composer autoloader file
- Magento/Framework/Component/ComponentRegistrar class is use for register
- next call to etc/module.xml

#### etc/module.xml
- Specify setup version 
- Contain Loading sequence  
- database setup depend on module versions
 
##### Note: 
- vendor/magento/framework/Module/ModueList/Loader.php 
- The static list of module is stored in app/etc/config.php
- Sequence is use for events, plugins and preferences and layouts.
- if your module owerwrite other module layout but it will be load first then other module will overwrite your modules layout.

##### Ex:

```
<?xml version='1.0'?>
<config xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xsi:noNamespaceSchemaLocation='urn:magento:framework:Module/etc/module.xsd'>
   <module name='Namespace_Module' setup_version='1.0.0'>
        <sequence>
            <module name="Magento_Sales"/>
            <module name="Magento_Payment"/>
            <module name="Magento_Checkout"/>
            <module name="Magento_Quote"/>
        </sequence>
   </module>
</config>

```




