# Before Developping

## Disables caches

System &gt; Tools &gt; Cache Management &gt; Disables caches

## Server Configuration

app/etc/env.php

```xml
SetEnv MAGE_MODE "developer"
```

vhost:

```xml
<VirtualHost *:80>
    ServerName magento2.local
    DocumentRoot /var/www/html/magento2
    SetEnv MAGE_MODE "developer"
    <Directory /var/www/html/magento2>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride All
        Order allow,deny
        allow from all
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/magento2_error.log
    # Possible values include: debug, info, notice, warn, error, crit, alert, emerg.
    LogLevel warn
    CustomLog ${APACHE_LOG_DIR}/magento2_access.log combined
</VirtualHost>
```

Restart apache :

`sudo service apache2 restart`

| Mode name | Description |
| :--- | :--- |
| [developer](http://devdocs.magento.com/guides/v2.0/config-guide/bootstrap/magento-modes.html#mode-developer) | Intended for development only, this mode:Disables [static view file caching](http://magento.stackexchange.com/questions/74059/magento-2-whats-a-static-view-file)Provides verbose loggingEnables [automatic code compilation](http://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-compiler-single.html##config-cli-subcommands-compile-overview)Enables enhanced debuggingShows custom `X-Magento-*` HTTP request and response headersResults in the slowest performance \(because of the preceding\) |
| [default](http://devdocs.magento.com/guides/v2.0/config-guide/bootstrap/magento-modes.html#mode-default) | As the name implies, Magento operates in this mode if no mode is explicitly set. In this mode:Static view file caching is enabledEnables [automatic code compilation](http://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-compiler-single.html##config-cli-subcommands-compile-overview)Exceptions are not displayed to the user; instead, exceptions are written to log files.Hides custom `X-Magento-*` HTTP request and response headersAlthough you _can_ run Magento in default mode in production, we don’t recommend it. |
| [production](http://devdocs.magento.com/guides/v2.0/config-guide/bootstrap/magento-modes.html#mode-production) | Intended for deployment on a production system. Exceptions are not displayed to the user, exceptions are written to logs only, and static files are not cached. |

Edit php.ini:

/etc/php/7.0/apache2/php.ini

/etc/php/7.0/fpm/php.ini

```xml
error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT
display_errors = On
```

Retart apache

`sudo service apache2 restart`

Change Magento mode:

* Show mode:

```xml
magento deploy:mode:show
```

* Change mode:

```xml
magento deploy:mode:set {mode} [-s|--skip-compilation]
```

* List mode:
  * default
  * production
  * developer

Cannot currently change from either developer or production mode to default mode.

If change production mode to developer mode, delete the contents of the `var/generation` and `var/di` directories:

```xml
rm -rf <your Magento install dir>/var/di/* <your Magento install dir>/var/generation/*
```

# Declare a new Magento 2 module

Create Module in **"app/code": **`app/code/Test/Helloworld/`

* Test: namespace
* Helloworld: module name

Create config module:  etc/module.xml

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Test_Helloworld" setup_version="1.0.0.0" active="true"/>
</config>
```

* name: module name
* setup\_version: module version
* active: status of module \(true/false\)

## Module registration

Create a "**registration.php**" file on the root folder of module

```php
\Magento\Framework\Component\ComponentRegistrar::register(
    \Magento\Framework\Component\ComponentRegistrar::MODULE,
    'Test_Helloworld',
    __DIR__
);
```

Run update module:

```xml
sudo php bin/magento setup:upgrade
```

## Module Activation

Check list module and status in `app/etc/config.php`

```php
return array (
  'modules' => 
  array (
    ...
    'Test_Helloworld' => 1,
    ...
  ),
);
```

Check table: setup\_module

![](/assets/setup_module.png)

# Uninstall module

sudo php bin/magento module:uninstall &lt;module name&gt;

# Create Magento 2 frontend controller

## Router declaration

Create a XML file:

app/code/Test/Helloworld/etc/frontend/routes.xml

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:App/etc/routes.xsd">
    <router id="standard">
        <route id="helloworld" frontName="helloworld">
            <module name="Test_Helloworld" before="Magento_Core" after="Magento_Sales"/>
        </route>
    </router>
</config>
```

* `id="standard": frontend controller`
* `id="admin": admin controller`
* id : unique identifier for your router
* frontName : the string which be used on the front URL
* name : module name to call
* before : your module have to be called before the module defined inside
* after : your module have to be called after the module defined inside
* Note: "before" et "after" fields are NOT required

## Controller creation

app/code/Test/Helloworld/Controller/Index/Index.php

```php
namespace Test\Helloworld\Controller\Index;
class Index extends \Magento\Framework\App\Action\Action
{
    public function execute()
    {
        echo 'Execute Action Index_Index OK';
        die();
    }
}
```

* `namespace` is the path of your controller inside the `app/code` folder.
* `class`name is the name of your PHP file.

## Customize URL

Our previous URL is very simple :

`http://magento2.local/helloworld`

But Magento 2 convert it to :

`http://magento2.local/helloworld/index/index`

* The first "index" is the folder "Index" inside "Controller".

* The second "index" is the file "Index.php" on the "Index" folder.

# Create simple module with Magento 2

## Controller modification

Change content file:

`app/code/Test/Helloworld/Controller/Index/Index.php`

```php
namespace Test\Helloworld\Controller\Index;
class Index extends \Magento\Framework\App\Action\Action
{
    public function execute()
    {
        $this->_view->loadLayout();
        $this->_view->getLayout()->initMessages();
        $this->_view->renderLayout();
    }
}
```

=&gt; Show template

## Block creation

Create the file `app/code/Test/Helloworld/Block/Hello.php`

```php
namespace Test\Helloworld\Block;
class Hello extends \Magento\Framework\View\Element\Template
{
}
```

## Layout creation

Associate routes and block

name is very important and must be composed with :

&lt;Router Name&gt;\_&lt;Controller Name&gt;\_&lt;Action Name&gt;

The layout names of these URL are :

`helloworld_index_index`

Create file:

`app/code/Test/Helloworld/view/frontend/layout/helloworld_index_index.xml`

```xml
<?xml version="1.0"?>
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd"
      layout="2columns-right">
    <body>
        <referenceContainer name="content">
            <block class="Test\Helloworld\Block\Hello" name="hello" template="helloworld.phtml">
            </block>
        </referenceContainer>
    </body>
</page>
```

* class: block file
* template: template file
* name: alias name, using to call getChildHTML\(\),...

## Template creation

Create the file

`app/code/Maxime/Helloworld/view/frontend/templates/helloworld.phtml`

```php
<h2>HelloWorld</h2>
<p>Congratulations ! You have created your first Magento Module !</p>
<p>The block classname is : <?php echo get_class($block) ?></p>
```

Delete cache + var/generation folder and refresh page

sudo php bin/magento cache:flush

sudo rm -rf var/generation/

# Setup management on Magento 2

## Module declaration

Create this XML file:

`app/code/Test/Jobs/etc/module.xml`

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Test_Jobs" setup_version="1.0.0"/>
</config>
```

Create the file :  
`app/code/Test/Jobs/registration.php`

```php
\Magento\Framework\Component\ComponentRegistrar::register(
    \Magento\Framework\Component\ComponentRegistrar::MODULE,
    'Test_Jobs',
    __DIR__
);
```

## Installation setup creation

Create file :

`app/code/Test/Jobs/Setup/InstallSchema.php`

```php
namespace Test\Jobs\Setup;

use Magento\Framework\Setup\InstallSchemaInterface;
use Magento\Framework\Setup\ModuleContextInterface;
use Magento\Framework\Setup\SchemaSetupInterface;
use Magento\Framework\DB\Ddl\Table;

class InstallSchema implements InstallSchemaInterface
{
    /**
     * Installs DB schema for a module
     *
     * @param SchemaSetupInterface $setup
     * @param ModuleContextInterface $context
     * @return void
     */
    public function install(SchemaSetupInterface $setup, ModuleContextInterface $context)
    {
        $installer = $setup;
        $installer->startSetup();

        /**
         * Create table 'test_department'
         */

        $tableName = $installer->getTable('test_department');
        $tableComment = 'Department management for jobs module';
        $columns = array(
            'entity_id' => array(
                'type' => Table::TYPE_INTEGER,
                'size' => null,
                'options' => array('identity' => true, 'unsigned' => true, 'nullable' => false, 'primary' => true),
                'comment' => 'Department Id',
            ),
            'name' => array(
                'type' => Table::TYPE_TEXT,
                'size' => 255,
                'options' => array('nullable' => false, 'default' => ''),
                'comment' => 'Department name',
            ),
            'description' => array(
                'type' => Table::TYPE_TEXT,
                'size' => 2048,
                'options' => array('nullable' => false, 'default' => ''),
                'comment' => 'Department description',
            ),
        );

        $indexes = array(// No index for this table
        );

        $foreignKeys = array(// No foreign keys for this table
        );

        /**
         *  We can use the parameters above to create our table
         */

        // Table creation
        $table = $installer->getConnection()->newTable($tableName);

        // Columns creation
        foreach ($columns AS $name => $values) {
            $table->addColumn(
                $name,
                $values['type'],
                $values['size'],
                $values['options'],
                $values['comment']
            );
        }

        // Indexes creation
        foreach ($indexes AS $index) {
            $table->addIndex(
                $installer->getIdxName($tableName, array($index)),
                array($index)
            );
        }

        // Foreign keys creation
        foreach ($foreignKeys AS $column => $foreignKey) {
            $table->addForeignKey(
                $installer->getFkName($tableName, $column, $foreignKey['ref_table'], $foreignKey['ref_column']),
                $column,
                $foreignKey['ref_table'],
                $foreignKey['ref_column'],
                $foreignKey['on_delete']
            );
        }

        // Table comment
        $table->setComment($tableComment);

        // Execute SQL to create the table
        $installer->getConnection()->createTable($table);

        // End Setup
        $installer->endSetup();
    }

}
```

* A name: $tableName

* A table comment: $tableComment

* Table columns with their type, their size, some options and a comment

* Some indexes: $indexes

* Some foreign keys: $foreignKeys

Available columns options :

* identity: an auto\_increment column

* unsigned: unsigned number

* nullable: when it false, it add "NOT NULL" SQL to the column

* primary: primary key

* default: default value for our column

Launch the upgrade

```xml
sudo php bin/magento setup:upgrade
```

## Upgrade Setup Creation

Create the file :

`app/code/Test/Jobs/Setup/UpgradeSchema.php`

```php
namespace Test\Jobs\Setup;

use Magento\Framework\Setup\UpgradeSchemaInterface;
use Magento\Framework\Setup\ModuleContextInterface;
use Magento\Framework\Setup\SchemaSetupInterface;
use Magento\Framework\DB\Ddl\Table;

class UpgradeSchema implements UpgradeSchemaInterface
{
    /**
     * Upgrades DB schema for a module
     *
     * @param SchemaSetupInterface $setup
     * @param ModuleContextInterface $context
     * @return void
     */
    public function upgrade(SchemaSetupInterface $setup, ModuleContextInterface $context)
    {
        $installer = $setup;
        $installer->startSetup();

        // Action to do if module version is less than 1.0.0.0
        if (version_compare($context->getVersion(), '1.0.1') < 0) {

            /**
             * Create table 'test_jobs'
             */

            $tableName = $installer->getTable('test_job');
            $tableComment = 'Job management on Magento 2';
            $columns = array(
                'entity_id' => array(
                    'type' => Table::TYPE_INTEGER,
                    'size' => null,
                    'options' => array('identity' => true, 'unsigned' => true, 'nullable' => false, 'primary' => true),
                    'comment' => 'Job Id',
                ),
                'title' => array(
                    'type' => Table::TYPE_TEXT,
                    'size' => 255,
                    'options' => array('nullable' => false, 'default' => ''),
                    'comment' => 'Job Title',
                ),
                'type' => array(
                    'type' => Table::TYPE_TEXT,
                    'size' => 255,
                    'options' => array('nullable' => false, 'default' => ''),
                    'comment' => 'Job Type (CDI, CDD...)',
                ),
                'location' => array(
                    'type' => Table::TYPE_TEXT,
                    'size' => 255,
                    'options' => array('nullable' => false, 'default' => ''),
                    'comment' => 'Job Location',
                ),
                'date' => array(
                    'type' => Table::TYPE_DATE,
                    'size' => null,
                    'options' => array('nullable' => false),
                    'comment' => 'Job date begin',
                ),
                'status' => array(
                    'type' => Table::TYPE_BOOLEAN,
                    'size' => null,
                    'options' => array('nullable' => false, 'default' => 0),
                    'comment' => 'Job status',
                ),
                'description' => array(
                    'type' => Table::TYPE_TEXT,
                    'size' => 2048,
                    'options' => array('nullable' => false, 'default' => ''),
                    'comment' => 'Job description',
                ),
                'department_id' => array(
                    'type' => Table::TYPE_INTEGER,
                    'size' => null,
                    'options' => array('unsigned' => true, 'nullable' => false),
                    'comment' => 'Department linked to the job',
                ),
            );

            $indexes = array(
                'title',
            );

            $foreignKeys = array(
                'department_id' => array(
                    'ref_table' => 'test_department',
                    'ref_column' => 'entity_id',
                    'on_delete' => Table::ACTION_CASCADE,
                )
            );

            /**
             *  We can use the parameters above to create our table
             */

            // Table creation
            $table = $installer->getConnection()->newTable($tableName);

            // Columns creation
            foreach ($columns AS $name => $values) {
                $table->addColumn(
                    $name,
                    $values['type'],
                    $values['size'],
                    $values['options'],
                    $values['comment']
                );
            }

            // Indexes creation
            foreach ($indexes AS $index) {
                $table->addIndex(
                    $installer->getIdxName($tableName, array($index)),
                    array($index)
                );
            }

            // Foreign keys creation
            foreach ($foreignKeys AS $column => $foreignKey) {
                $table->addForeignKey(
                    $installer->getFkName($tableName, $column, $foreignKey['ref_table'], $foreignKey['ref_column']),
                    $column,
                    $foreignKey['ref_table'],
                    $foreignKey['ref_column'],
                    $foreignKey['on_delete']
                );
            }

            // Table comment
            $table->setComment($tableComment);

            // Execute SQL to create the table
            $installer->getConnection()->createTable($table);
        }

        $installer->endSetup();
    }
}
```

Compare the old module version with the new module version :

```php
if (version_compare($context->getVersion(), '1.0.1') < 0)
```

* version\_compare return -1 if current version is less than new version

* version\_compare retourne 0 if current version is equal new version

* version\_compare retourne 1 if current version is greater than new version

For each module upgrades, you have to put this condition on this file, like this:

```php
public function upgrade(SchemaSetupInterface $setup, ModuleContextInterface $context)
    {
        $installer = $setup;
        $installer->startSetup();

        if (version_compare($context->getVersion(), '1.0.0') < 0) {
            // Action to do if module version is less than 1.0.0
        }

        if (version_compare($context->getVersion(), '1.0.1') < 0) {
            // Action to do if module version is less than 1.0.1
        }

        if (version_compare($context->getVersion(), '1.1.0') < 0) {
            // Action to do if module version is less than 1.1.0
        }

        if (version_compare($context->getVersion(), '1.1.1') < 0) {
            // Action to do if module version is less than 1.1.1
        }

        if (version_compare($context->getVersion(), '2.0.0') < 0) {
            // Action to do if module version is less than 2.0.0
        }

        $installer->endSetup();
    }
```

Edit file :  
`app/code/Test/Jobs/etc/module.xml`

Change `setup_version` attribute to `1.0.1`

Launch the upgrade command:

```xml
sudo php bin/magento setup:upgrade
```

# Create a model with Magento 2

## Models declaration

Create the file :

`app/code/Test/Jobs/Model/Department.php`

```php
namespace Test\Jobs\Model;

use \Magento\Framework\Model\AbstractModel;

class Department extends AbstractModel
{
    const DEPARTMENT_ID = 'entity_id'; // We define the id fieldname

    /**
     * Prefix of model events names
     *
     * @var string
     */
    protected $_eventPrefix = 'jobs'; // parent value is 'core_abstract'

    /**
     * Name of the event object
     *
     * @var string
     */
    protected $_eventObject = 'department'; // parent value is 'object'

    /**
     * Name of object id field
     *
     * @var string
     */
    protected $_idFieldName = self::DEPARTMENT_ID; // parent value is 'id'

    /**
     * Initialize resource model
     *
     * @return void
     */
    protected function _construct()
    {
        $this->_init('Test\Jobs\Model\ResourceModel\Department');
    }
}
```

Create the “Job” model :

`app/code/Test/Jobs/Model/Job.php`

```php
namespace Test\Jobs\Model;

use \Magento\Framework\Model\AbstractModel;

class Job extends AbstractModel
{
    const JOB_ID = 'entity_id'; // We define the id fieldname

    /**
     * Prefix of model events names
     *
     * @var string
     */
    protected $_eventPrefix = 'jobs';

    /**
     * Name of the event object
     *
     * @var string
     */
    protected $_eventObject = 'job';

    /**
     * Name of object id field
     *
     * @var string
     */
    protected $_idFieldName = self::JOB_ID;

    /**
     * Initialize resource model
     *
     * @return void
     */
    protected function _construct()
    {
        $this->_init('Test\Jobs\Model\ResourceModel\Job');
    }
}
```

## ResourceModels declaration

Create file :

`app/code/Test/Jobs/Model/ResourceModel/Department.php`

```php
namespace Test\Jobs\Model\ResourceModel;

use \Magento\Framework\Model\ResourceModel\Db\AbstractDb;

/**
 * Department post mysql resource
 */
class Department extends AbstractDb
{

    /**
     * Initialize resource model
     *
     * @return void
     */
    protected function _construct()
    {
        // Table Name and Primary Key column
        $this->_init('test_department', 'entity_id');
    }

}
```

Two parameters:

* Table name

* Primary column’s name

Create file:

`app/code/Test/Jobs/Model/ResourceModel/Job.php`

```php
namespace Test\Jobs\Model\ResourceModel;

use \Magento\Framework\Model\ResourceModel\Db\AbstractDb;

/**
 * Department post mysql resource
 */
class Job extends AbstractDb
{

    /**
     * Initialize resource model
     *
     * @return void
     */
    protected function _construct()
    {
        // Table Name and Primary Key column
        $this->_init('test_job', 'entity_id');
    }

}
```

## Collections class creation

Create file:

`app/code/Test/Jobs/Model/ResourceModel/Department/Collection.php`

```php
namespace Test\Jobs\Model\ResourceModel\Department;

use \Magento\Framework\Model\ResourceModel\Db\Collection\AbstractCollection;

class Collection extends AbstractCollection
{
    protected $_idFieldName = \Test\Jobs\Model\Department::DEPARTMENT_ID;

    /**
     * Define resource model
     *
     * @return void
     */
    protected function _construct()
    {
        $this->_init('Test\Jobs\Model\Department', 'Test\Jobs\Model\ResourceModel\Department');
    }
}
```

"init" method has got two paramaters:

* The model path

* The ResourceModel path

Create file:

`app/code/Test/Jobs/Model/ResourceModel/Job/Collection.php`

```php
namespace Test\Jobs\Model\ResourceModel\Job;

use \Magento\Framework\Model\ResourceModel\Db\Collection\AbstractCollection;

class Collection extends AbstractCollection
{
    protected $_idFieldName = \Test\Jobs\Model\Job::JOB_ID;

    /**
     * Define resource model
     *
     * @return void
     */
    protected function _construct()
    {
        $this->_init('Test\Jobs\Model\Job', 'Test\Jobs\Model\ResourceModel\Job');
    }
}
```

Create Model have 3 file:

* Model file: A.php
* ResourceModel file: ResourceModel\A.php
* Collection file: ResourceModel\A\Collection.php

# Module datas setup with Magento 2

## Datas setup

Open the file and add 2 methods:  
`app/code/Test/Jobs/Model/Job.php`

```php
    public function getEnableStatus()
    {
        return 1;
    }

    public function getDisableStatus()
    {
        return 0;
    }
```

Create the file :

`app/code/Test/Jobs/Setup/UpgradeData.php`

```php
namespace Test\Jobs\Setup;

use Test\Jobs\Model\Department;
use Test\Jobs\Model\Job;
use Magento\Framework\Setup\UpgradeDataInterface;
use Magento\Framework\Setup\ModuleContextInterface;
use Magento\Framework\Setup\ModuleDataSetupInterface;

/**
 * @codeCoverageIgnore
 */
class UpgradeData implements UpgradeDataInterface
{

    protected $_department;
    protected $_job;

    public function __construct(Department $department, Job $job)
    {
        $this->_department = $department;
        $this->_job = $job;
    }

    /**
     * {@inheritdoc}
     * @SuppressWarnings(PHPMD.ExcessiveMethodLength)
     */
    public function upgrade(ModuleDataSetupInterface $setup, ModuleContextInterface $context)
    {
        $installer = $setup;
        $installer->startSetup();

        // Action to do if module version is less than 1.0.0.1
        if (version_compare($context->getVersion(), '1.0.1') < 0) {
            $departments = [
                [
                    'name' => 'Marketing',
                    'description' => 'Sed cautela nimia in peiores haeserat plagas, ut narrabimus postea,
                aemulis consarcinantibus insidias graves apud Constantium, cetera medium principem sed
                siquid auribus eius huius modi quivis infudisset ignotus, acerbum et inplacabilem et in
                hoc causarum titulo dissimilem sui.'
                ],
                [
                    'name' => 'Technical Support',
                    'description' => 'Post hanc adclinis Libano monti Phoenice, regio plena gratiarum et
                venustatis, urbibus decorata magnis et pulchris; in quibus amoenitate celebritateque
                nominum Tyros excellit, Sidon et Berytus isdemque pares Emissa et Damascus saeculis condita
                priscis.'
                ],
                [
                    'name' => 'Human Resource',
                    'description' => 'Duplexque isdem diebus acciderat malum, quod et Theophilum insontem atrox
                interceperat casus, et Serenianus dignus exsecratione cunctorum, innoxius, modo non reclamante publico vigore,
                discessit.'
                ]
            ];

            /**
             * Insert departments
             */
            $departmentsIds = array();
            foreach ($departments as $data) {
                $department = $this->_department->setData($data)->save();
                $departmentsIds[] = $department->getId();
            }


            $jobs = [
                [
                    'title' => 'Sample Marketing Job 1',
                    'type' => 'CDI',
                    'location' => 'Paris, France',
                    'date' => '2016-01-05',
                    'status' => $this->_job->getEnableStatus(),
                    'description' => 'Duplexque isdem diebus acciderat malum, quod et Theophilum insontem atrox
                interceperat casus, et Serenianus dignus exsecratione cunctorum, innoxius, modo non reclamante publico vigore,
                discessit.',
                    'department_id' => $departmentsIds[0]
                ],
                [
                    'title' => 'Sample Marketing Job 2',
                    'type' => 'CDI',
                    'location' => 'Paris, France',
                    'date' => '2016-01-10',
                    'status' => $this->_job->getDisableStatus(),
                    'description' => 'Duplexque isdem diebus acciderat malum, quod et Theophilum insontem atrox
                interceperat casus, et Serenianus dignus exsecratione cunctorum, innoxius, modo non reclamante publico vigore,
                discessit.',
                    'department_id' => $departmentsIds[0]
                ],
                [
                    'title' => 'Sample Technical Support Job 1',
                    'type' => 'CDD',
                    'location' => 'Lille, France',
                    'date' => '2016-02-01',
                    'status' => $this->_job->getEnableStatus(),
                    'description' => 'Duplexque isdem diebus acciderat malum, quod et Theophilum insontem atrox
                interceperat casus, et Serenianus dignus exsecratione cunctorum, innoxius, modo non reclamante publico vigore,
                discessit.',
                    'department_id' => $departmentsIds[1]
                ],
                [
                    'title' => 'Sample Human Resource Job 1',
                    'type' => 'CDI',
                    'location' => 'Paris, France',
                    'date' => '2016-01-01',
                    'status' => $this->_job->getEnableStatus(),
                    'description' => 'Duplexque isdem diebus acciderat malum, quod et Theophilum insontem atrox
                interceperat casus, et Serenianus dignus exsecratione cunctorum, innoxius, modo non reclamante publico vigore,
                discessit.',
                    'department_id' => $departmentsIds[2]
                ]
            ];

            foreach ($jobs as $data) {
                $this->_job->setData($data)->save();
            }
        }

        $installer->endSetup();
    }
}
```

Dependency injection with Magento 2:

```php
    public function __construct(Department $department, Job $job)
    {
        $this->_department = $department;
        $this->_job = $job;
    }
```

Cannot use the `Mage::getModel()` like Magento 1.

Change the "setup\_version" to "1.0.2"

Launch the upgrade command:

```xml
sudo php bin/magento setup:upgrade
```

"Setup\InstallData.php" =&gt; launched at the first module upgrade.

# Admin menu creation and access control list managment \(ACL\) on Magento 2





