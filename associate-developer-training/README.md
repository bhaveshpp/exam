## 1 Magento Architecture and Customization Techniques

### 1.1 Describe the Magento module-based architecture
- Describe module architecture. What are the significant steps to add a new module? 
    - registration.php
        - Magento\Framework\Component\ComponentRegistrar::register();
    - module.xml, theme.xml, language.xml
        - version and name declaratioin
    - Api
        - data / service contracts
        - geter and seter interface
    - Block
        - provide logic to render templates
        - define in layoutes
        - MVVM ViewModel
        - contain view-model and block
    - Contorller
        - Handel Requests.
        - adminhtml, frontend controler.
    - Helper
        - contain common functionality.
    - Model
        - contain database interaction
        - model, resourceModel, collection
    - etc
        - contain configuration .xml files
        - di.xml, routes.xml, system.xml, menu.xml, config.xml, dbSchema.xml, etc
    - view
        - contain the templates, layouts, page_layout, web / knockout js templates ,js ,css , etc
        - also contain the UiComponent layout declaration .xml files
        - require-config.js file that define the js
    - console
        - declaration of the cli commands
    - Plugin
        - contain the plugin action classis
    - i18n
        - contain .csv files of language translation.
    - Observer
        - containthe event observer classis that declare in etc/event.xml
    - cron 
        - contain shedule job classis that declared in the etc/crontab.xml 
    - UI/Component
        - contain ui_component data provider and modifier
    - Setup 
        - containthe statment that generate/Modify database table.
        - installSchema.php generate tables.
        - installData.php update default magento Existiing Tables ex: add record,column, etc
        - Recurring.php after all modification done this will run
        - when module version are change then this files will be executed
        - updateSchema.php ,updateData.php

- What are the different Composer package types? 
    - metapackages
    - module
    - theme
    - language packages

- When would you place a module in the app/code folder versus another location?
    - app/code/Vendor/Module
        - module local development
    - vendor/vendor-name/module-name
        - composer packages
        - uncatchable

### 1.2 Describe the Magento directory structure
- Describe the Magento directory structure. 
- What are the naming conventions, and how are namespaces established?
    - Namespace_Modulename
    - ex
        Magento\Framework\Viwe\Element\Template
        vendor/magento/framework/view/element/Template.php
- How can you identify the files responsible for some functionality?
    - find controller 
        - copy the first keyword after the base url and find in project

### 1.3 Utilize configuration and configuration variables scope
- Determine how to use configuration files in Magento. 
    - di.xml - for dependency injection
    - system.xml - for generate system config fields
    - routes.xml - for create routes
    - config.xml - for set default config value
    - module.xml - for module declaration and dependency sequence
    - crontab.xml - for setting sheduled tasks
    - event.xml - for register the events
    - acl.xml - for add the module resource to resource tree.
    - widget.xml - for storing widget settings
    - indexer.xml - declare new index
    - mview - track database changes
    - product_type.xml - declare new product type
    - view.xml - theme settings
    - webapi.xml - service declaration
    - product_option.xml - 

- Which configuration files are important in the development cycle?
    - di.xml
    - config.php
    - env.php

- Describe development in the context of website and store scopes.
    - How do you identify the configuration scope for a given variable?
        - from the top-left cornne we will find the socpe dropdown in the store configuration settings.
        - select the specific store and save the store wise config.

    - How do native Magento scopes (for example, price or inventory) affect development and decision-making processes?
        - store -> configuration -> catalog -> price -> catalog price scop. 
        - set it to global or website

    - Demonstrate an ability to add different values for different scopes. 
        - from the top-left corner set the scop to storeview
        - set the value using command
            - php bin/magento config:set
            - php bin/magento config:sensitive:set   
            ex : sudo /opt/lampp/bin/php bin/magento config:set web/unsecure/base_url http://192.168.0.172/magento/demo1/
    - How can you fetch a system configuration value programmatically? 
            - const SCOPE_STORES = 'stores';
            - const SCOPE_WEBSITES = 'websites';
            - const SCOPE_STORE = 'store';
            - const SCOPE_GROUP = 'group';
            - const SCOPE_WEBSITE = 'website';
            - $this->scopeConfig->getValue($field,\Magento\Store\Model\ScopeInterface::SCOPE_STORES);
            - php bin/magento config:show
    - How can you override system configuration values for a given store using XML configuration?
        - there is tree structure where all the leef node depend on his parent 
        - Website
          |_Store
             |_Store view
        - here for store view store and website is parant.
        - if there is parant value is available for the store view then tik uew website or use default settings
        $_ENV['CONFIG__DEFAULT__CATALOG__SEARCH__ELASTICSEARCH_SERVER_HOSTNAME'] = 'http://search.example.com';

### 1.4 Demonstrate how to use dependency injection (DI) [Object Manager & di]
- Demonstrate the ability to use the dependency injection concept in Magento development.
    - in magento one class can use the method of another class by injecting it.
    - we can inject dependency using the constructor argument or by object manager.

- How are objects realized in code?
    - by using object manager or dependency injection [di.xml]
    - $objectManager->create();
    - declare di.xml in etc/[area]/di.xml or etc/di.xml in module and inject class.

- Why is it important to have a centralized object creation process?
    - application become more flaxible and easy to test
    - use class using object manager any where. $objectManager->get('class');
    - inject code inside the existing code.
    - inject class dependency in constructor using di.xml

- Identify how to use DI configuration files for customizing Magento. 
    - preference
    - plugins
    - virtual type
    - constructor argument

- How can you override a native class, inject your class into another object, and use other techniques available in di.xml (for example, virtualTypes)?
    - override a native class
        - by using preference
    - inject your class into another object
        - by using type > arguments > argument node
    - other 
        - plugins, virtual type etc

- Given a scenario, determine how to obtain an object using the ObjectManager object.
- How would you obtain a class instance from different places in the code?
```
    $objectManager =  \Magento\Framework\App\ObjectManager::getInstance();
    $appState = $objectManager->get('\Magento\Framework\App\State');
    $appState->setAreaCode('frontend');
    $customerObj = $objectManager->create('Magento\Customer\Model\Customer')->getCollection();
```


### 1.5 Demonstrate ability to use plugins
- Demonstrate an understanding of plugins. 
    - before, after and around plugin
    - before plugin
        - can change input argument
    - after plugin
        - can change return value
    - around plugin
        - can change input argument and also return value

- How are plugins used in core code? 
    - 
- How can they be used for customizations?
    - 


### 1.6 Configure event observers and scheduled jobs
Demonstrate how to create a customization using an event observer. How are observers registered? How are they
scoped for frontend or backend? How are automatic events created, and how should they be used? How are scheduled
jobs configured?


### 1.7 Utilize the CLI
Describe the usage of bin/magento commands in the development cycle. Which commands are available? How
are commands used in the development cycle?

### 1.8 Describe how extensions are installed and configured
How would you install and verify an extension by a customer’s request?

## 2 Request Flow Processing

### 2.1 Describe how to use Magento modes
Understand the pros and cons of using developer mode or production mode. How do you enable/disable maintenance
mode?

### 2.2 Demonstrate the ability to create a frontend controller with different response types
(HTML / JSON / redirect)
How do you identify which module/controller corresponds to a given URL? What would you do to create a given URL?

### 2.3 Demonstrate how to use URL rewrites for a catalog product view to a different URL
How is the user-friendly URL of a product or category defined? How can you change it? How do you determine which
page corresponds to a given user-friendly URL?

## 3 Customizing the Magento UI


### 3.1 Demonstrate the ability to customize the Magento UI using themes
Demonstrate the ability to customize the Magento UI using themes. When would you create a new theme? How do
you define theme hierarchy for a project?

### 3.2 Demonstrate an ability to create UI customizations using a combination of a block and
template
How do you assign a template to a block? How do you assign a different template to a native block?

### 3.3 Identify the uses of different types of blocks
When would you use non-template block types?
Topics and Objectives
4 Magento 2 Certified Associate Developer Exam Study Guide © 2019 Magento, Inc.

### 3.4 Describe the elements of the Magento layout XML schema, including the major XML
directives
How do you use layout XML directives in your customizations? How do you register a new layout file?

### 3.5 Create and add code and markup to a given page
How do you add new content to existing pages using layout XML?

### 4 Working with Databases in Magento

### 4.1 Describe the basic concepts of models, resource models, and collections
What are the responsibilities of each of the ORM object types? How do they relate to one another?

### 4.2 Describe how entity load and save occurs
How do you use the native Magento save/load process in the development process?

### 4.3 Describe how to filter, sort, and specify the selected values for collections and repositories
How do you select a subset of records from the database?

### 4.4 Demonstrate an ability to use declarative schema
How do you add a column using declarative schema? How do you modify a table added by another module? How do you
delete a column? How do you add an index or foreign key using declarative schema? How do you manipulate data using
data patches? What is the purpose of schema patches?

## 5 Developing with Adminhtml

### 5.1 Create a controller for an admin router
How would you create an admin controller? How do you ensure the right level of security for a new controller?

### 5.2 Define basic terms and elements of system configuration, including scopes, website,
store, store view
How would you add a new system configuration option? What is the difference in this process for different option types
(secret, file)?

### 5.3 Define / identify basic terms and elements of ACL
How would you add a new ACL resource to a new entity? How do you manage the existing ACL hierarchy?
Topics and Objectives
Magento 2 Certified Associate Developer Exam Study Guide © 2019 Magento, Inc. 5

### 5.4 Set up a menu item
How do you add a new menu item to a given tab? How do you add a new tab to the Admin menu?

### 5.5 Create appropriate permissions for users
How are menu items related to ACL permissions? How do you add a new user with given set of permissions?

## 6 Customizing Magento Business Logic

### 6.1 Identify/describe standard product types (simple, configurable, bundled, etc.)
How would you obtain a product of a specific type, and what tools (in general) does a product type model provide?

### 6.2 Describe category properties in Magento
How do you create and manage categories?

### 6.3 Define how products are related to the category
How do you assign and unassign products to categories?

### 6.4 Describe the difference in behavior of different product types in the cart
How are configurable and bundle products rendered? How can you create a custom shopping cart renderer?

### 6.5 Describe native shipment functionality in Magento
How do you customize the shipment step of order management?

### 6.6 Describe and customize operations available in the customer account area
How would you add another tab in the “My Account” section? How do you customize the order history page?

### 6.7 Add or modify customer attributes
How do you add or modify customer attributes in a setup script?

### 6.8 Customize the customer address
How do you add another field to the customer address entity using a setup script?
