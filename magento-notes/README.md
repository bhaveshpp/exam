##### Note : Two module can contain same route id if they contain dependency of each other.
##### 

#### Magento Test

##### Magento 2 Tire Price Qualifier
- Customer group
- Website
- Quantity

Modile Sequence

```
<module>
    <sequence>
        <module />
    </sequence>
</module>

```

for activate new module run command 

> php bin/magento setup:upgrade
> php bin/magento module:enable namesplace_module

##### Product Import behavior

> if csv not contain the "additional attribute" column and import behaviour is replace then the additional attribute value will be setted to default value.

##### for checking module work proper in production mode

> php bin/magento setup:db-declaration:generate-whitlist vendor_module

#####  Controller Result redirect /Forword

> Magento\Framework\Controller\Result\Redirect

> in redirect the url remain same

> in forworder the url will different


#### mview

> Mview is 


#### correct way to save model

call save method of resource model

##### create new cahe type

#### virtual type declaration for sorter name


#### Simple Product

- simple product is basic product not contain any variModule containant 

- php bin/magento sempledata:deploy


All command list

- php bin/magento setup:upgrade
- php bin/magento setup:di:compile
- php bin/magento setup:static-content:deploy -f
    - php bin/magento setup:static-content:deploy --theme Codazon/unlimited_fashion_accessores en_US en_GB fr_FR -f
    - php bin/magento setup:static-content:deploy --theme Codazon/unlimited_fashion_accessores -f
    - php bin/magento setup:static-content:deploy en_US en_GB fr_FR -f
- php bin/magento indexer:reindex
- php bin/magento indexer:info
- php bin/magento cache:clean
- php bin/magento cache:flush
- php bin/magento cache:status
- php bin/magento cache:enable
- php bin/magento cache:enable eav config
- php bin/magento cache:disable
- php bin/magento info:adminuri
- php bin/magento admin:user:create
- php bin/magento admin:user:unlock
- php bin/magento dev:template:hints:enable
- php bin/magento dev:template:hints:disable
- php bin/magento sampledata:deploy
- php bin/magento maintenance:enable
    - php bin/magento maintenance:enable --ip 192.168.0.173
- php bin/magento maintenance:disable
- php bin/magento module:disable
- php bin/magento module:enable
- php bin/magento deploy:mode:set developer
- php bin/magento config:show
- php bin/magento config:set

