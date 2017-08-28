### How can I check magento module status?

php bin/magento module:status

### How can I clear Cache and Reindex?

Here are the commands to cache and reindex.

php bin/magento cache:disable

php bin/magento cache:status

php bin/magento cache:flush

php bin/magento cache:clean

php bin/magento indexer:reindex

### How can I de compile using command?

Try running this command for de compile.

php bin/magento setup:di:compile

### Turn template hints on/off

UPDATE \`core\_config\_data\` SET \`value\` = 1 WHERE \`path\` = "dev/debug/template\_hints\_storefront"

### Add js file via require.js

Create file requirejs-config.js at app/design/\[vendor\]/\[theme\]/ with this content

var config = {

    // When load 'requirejs' always load the following files also

    deps: \["js/wim" //js file yang akan di load simpan di app/design/\[vendor\]/\[theme\]/web/js\]

};

### Magento new js file example to load other js lib

 Create other.js file at app/design/\[vendor\]/\[theme\]/web/js/

define\(\[

    'underscore',

    'jquery'

\], function\(\){

    "use strict";

    \_.each\(\["Hello", "World", "!!!!!!!!!!!!!!!!!!" \], console.log\);

}\);

### Grunt

grunt exec:&lt;your\_theme&gt;

grunt less:&lt;your\_theme&gt;

grunt watch

### Less breakpoint variable

  @screen\_\_xxs: 320px;

  @screen\_\_xs: 480px;

  @screen\_\_s: 640px;

  @screen\_\_m: 768px;

  @screen\_\_l: 1024px;

  @screen\_\_xl: 1440px;

### Select core config magento for change base\_url

SELECT path,VALUE FROM core\_config\_data WHERE path LIKE 'web/secure/base%';

SELECT path,VALUE FROM core\_config\_data WHERE path LIKE 'web/unsecure/base%';

