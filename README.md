[Reference]
https://swiftotter.com/
CERTIFIED PROFESSIONAL DEVELOPER EXAM PREPARATION EBOOK
- JOSEPH MAXWELL
[11232019]
# Magento 2 Architechture

## Module base Architechture

### there are 5 area in magento
- adminhtml
- frontend
- base
- cron
- webapi
    - webapi_rest
    - webapi_soap

### Nessesory files
- registration.php
- etc/module.xml
- composer.json

### Module Location
- app/code/Namespace/Module
- vendor/vendor-name/module-name
- anywhere in project

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
- next call to etc/module.

```
<?php
use Magento\Framework\Component\ComponentRegistrar;
ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'Namespace_Modulename',
    __DIR__
);

```

#### etc/module.xml
- Specify setup version 
- Contain Loading sequence  
- database setup depend on module versions

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
 
[11252019]

##### Note: 
- Magento 2 All module files are contained within one directory. 
- vendor/magento/framework/Module/ModueList/Loader.php 
- The static list of module is stored in app/etc/config.php
- Sequence is use for events, plugins and preferences and layouts.
- if your module owerwrite other module layout but it will be load first then other module will overwrite your modules layout.
- vendor/magento/magento2-base/setup/src/Magento/Setup/Console/Command/AbstractModuleManageCommand.php command used for module enable

https://belvg.com/blog/magento-2-module-based-architecture.html

Modules in Magento 2 are implemented by means of MVVM architecture.


## Magento Directory Architechture
- Magento 2 core file found in vendor/magento or app/code/Magento
- Supportin css and js file found in lib 

#### /Api: Service Contracts
- this folder stores contract for module that contain specific action.
- the action can be used from different location in application.

#### /Api/Data: Data service contract
- this folder contain interfaces that represent data.
- concrete implementations of these interfaces usualy do getter and setter for data.

#### /Block: view Models
- Block perform or provide bussiness logic for templates.
- in MVVM methodology Block are View-model.
- inheriting template block is makes testing and reusablility difficult.
- while view model live in /Block it provide bussiness logic of block and not rendering functionality.
- block is responsible for rendering output and view model handels logic.

#### ex: 
- to create block with view model

```
<block name="demo.block" template="Bhaveshpp_Block::post.phtml">
    <arguments>
        <argument name="viewModel" xsi:type="object">
            Bhaveshpp\Block\Post
        </argument>
    </arguments>
</block>

```

#### /Console: Console Commands
- when running php bin/magento all commands are listed
- the code of command is define here

##### ex: vendor/magento/module-media-storage/Console/Command/ImagesResizeCommand.php
> php bin/magento catalog:images:resize

#### /Controller: web request handeler
- when page is requested, the parameter matched to parameter found in routes.xml file and find the file in /Controller.
- magento 2 found admin controller in /Controller/adminhtml.

#### /Cron: Cron job classes
- Standard place for store Cron job action classes.
- when cron is define in etc/crontab.xml it will specify action class are located here.

#### /etc: configuration
- it contain configuration files 
- module.xml, crontab.xml, di.xml, webapi.xml, config.xml
- any file is directly within the /etc/ are global

##### ex:
> /etc/di.xml

> /etc/frontend/di.xml

> /etc/adminhtml/di.xml

- Some files are placed wihtin target area ex: routes.xml, sections.xml
- Some file have global scoap ex: di.xml.

Note: To minimize the load on server, developers should specify which action (or request) updates which customer data section in etc/section.xml.

#### /Helper: used for small reuseable code
- this folder hase no longer nessesory.
- how ever magento core folder are use this folder.
- Every method should be capable of being declared static (whether or not it is).

#### /i18n: contain translation csv files (internationalization)
- modules all translation related csv files are located here
- csv file contain two columns: From, To

#### /Model: Data Hendeling and Structures
- in MVVM this folder contains all the Models.
- here all the database structure related file.

#### /Model/ResourceModel: database interactions
- it represent how data are save and represent.
- any direct database interaction should happen here.

##### ex: Product resource model [What is a resource model](https://magento.stackexchange.com/questions/190025/magento-2-what-is-a-resource-model-and-how-can-i-use-it "magento.stackexchange.com")
- you can get product, category, order colllection data.

```
...

public function __construct(
    \Magento\Backend\Block\Template\Context $context,        
    \Magento\Catalog\Model\ResourceModel\Product\CollectionFactory $productCollectionFactory,      
    \Magento\Catalog\Model\ResourceModel\Category\CollectionFactory $categoriesCollection,  
    \Magento\Sales\Model\ResourceModel\Order\CollectionFactory $orderCollectionFactory,
    array $data = []
)
{    
    $this->_productCollectionFactory = $productCollectionFactory;   
    $this->_categoriesCollection = $categoriesCollection;     
    $this->orderCollectionFactory = $orderCollectionFactory;
    parent::__construct($context, $data);
}
/*
* Product collection Data
*/
public function getProductCollection()
{
    $collection = $this->_productCollectionFactory->create();
    $collection->addAttributeToSelect('*');
    return $collection;
}
/*
* Category collection Data
*/
public function getCategoryCollection()
{
    $collection = $this->_categoriesCollection->create();
    $collection->addAttributeToSelect('*');
    return $collection;
}
/*
* Order collection Data
*/
public function getOrderCollection()
{
    $order = $orders = $this->orderCollectionFactory->create();    
    $order->addAttributeToSort('created_at', 'desc');
    return $order;
}
...

```


