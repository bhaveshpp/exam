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



