php-manual
==========

php manual doc

Copy these files to runtimepath.(~/.vim,..)
Also can use vundle...


1. 
./configure --prefix=/Users/river/codeX/phpmanual/php551 --with-pear --with-zlib=/usr/local/Cellar/zlib/1.2.8 
make
make install

2.
php551/bin/pear install doc.php.net/phd_php
php551/bin/pear install XML_Parser

3.
svn co https://svn.php.net/repository/phpdoc/modules/doc-en phpdoc
cd phpdoc
vim build.sh
PHP=/Users/river/codeX/phpmanual/php551/bin/php
PHD=/Users/river/codeX/phpmanual/pear/bin/phd

vim /Volumes/DataHD/code/phpmanual/pear/share/pear/phpdotnet/phd/Index.php
add code: ini_set('memory_limit', '256M');

4.
wget http://blog.planetxml.de/uploads/source/php/phpdoc/parser2.php.txt -O parser2.php

vim parser2.diff

==========code start==========
--- a/parser2.php 2011-05-27 00:07:45.515535000 +0800
+++ b/parser2.php 2011-05-26 16:37:01.081761000 +0800
@@ -344,14 +344,16 @@
 //fwrite($fp, "!_TAG_FILE_SORTED       1\n");
 fclose($fp);
 
-load_entities('phpdoc/entities/global.ent');
+load_entities('phpdoc/doc-base/entities/global.ent');
+load_entities('phpdoc/doc-base/entities/version.ent');
+load_entities('phpdoc/doc-base/entities/file-entities.ent');
 load_entities('phpdoc/en/language-defs.ent');
 load_entities('phpdoc/en/language-snippets.ent');
-load_entities('phpdoc/en/livedocs.ent');
+load_entities('phpdoc/en/extensions.ent');
 load_entities('phpdoc/en/contributors.ent');
 //print_r($entities['&example.outputs;']);
 //print_r($entities);
-process_all('phpdoc\en\reference');
+process_all('phpdoc/en/reference');
 //process_all('d:/htdocs/livedocs/phpdoc/en/reference');
 
 echo "sorting tags\n";

==========code end==========
delete line: 
load_entities('phpdoc/doc-base/entities/version.ent');

5.
patch -p1 < parser2.diff

6.
mkdir out
php551/bin/php parser2.php
 

---ref:
http://blog.gasol.tw/2011/05/php-manual-in-vim.html
