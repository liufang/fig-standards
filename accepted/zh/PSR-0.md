自动加载规范
============

> **Deprecated** - As of 2014-10-21 PSR-0 has been marked as deprecated. [PSR-4] is now recommended 
as an alternative.

[PSR-4]: http://www.php-fig.org/psr/psr-4/

下面的要求必须强制性要求遵守自动加载规则的可操作。

硬性规范
--------

* 一个完整的命名空间类必须符合该格式 `\<Vendor Name>\(<Namespace>\)*<Class Name>` 。
* 每个命名空间必须有一个顶级的命名空间 ("Venddor Name")。
* 每个命名空间允许拥有更多的子命名空间。
* 每个命名空间的空间分隔符转换为 `DIRECTORY_SEPARATOR` 的时候可以从磁盘加载文件。
* 没当在类中碰到 `_` 字符的时候转换成 `DIRECTORY_SEPARATOR`， `_` 字符在命名空间中
  没有特殊意义。
* 完全限定的命名空间加上后缀 `.php` 可从文件系统导入。
* 在 vendor names, namespaces, class name允许小写字母大写字母的组合。

例子
----

* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/path/to/project/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/path/to/project/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/path/to/project/lib/vendor/Zend/Mail/Message.php`

强调命名空间和类名
------------------
* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`

该规范制定了最低自动加载标准。 你可以在PHP5.3版本使用简单的SplClassLoader接口测试。

实例
----

接下来的例子从功能上简单演示上述标准的自动加载机制。

```php
<?php

function autoload($className)
{
    $className = ltrim($className, '\\');
    $fileName  = '';
    $namespace = '';
    if ($lastNsPos = strrpos($className, '\\')) {
        $namespace = substr($className, 0, $lastNsPos);
        $className = substr($className, $lastNsPos + 1);
        $fileName  = str_replace('\\', DIRECTORY_SEPARATOR, $namespace) . DIRECTORY_SEPARATOR;
    }
    $fileName .= str_replace('_', DIRECTORY_SEPARATOR, $className) . '.php';

    require $fileName;
}
spl_autoload_register('autoload');
```

SplClassLoader实现
------------------

以下要点你可以在你的项目中引入SplClassLoader实现， 这时PHP5.3目前自动加载的推荐方式。

* [http://gist.github.com/221634](http://gist.github.com/221634)

