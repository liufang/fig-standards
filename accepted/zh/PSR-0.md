�Զ����ع淶
============

> **Deprecated** - As of 2014-10-21 PSR-0 has been marked as deprecated. [PSR-4] is now recommended 
as an alternative.

[PSR-4]: http://www.php-fig.org/psr/psr-4/

�����Ҫ�����ǿ����Ҫ�������Զ����ع���Ŀɲ�����

Ӳ�Թ淶
--------

* һ�������������ռ��������ϸø�ʽ `\<Vendor Name>\(<Namespace>\)*<Class Name>` ��
* ÿ�������ռ������һ�������������ռ� ("Venddor Name")��
* ÿ�������ռ�����ӵ�и�����������ռ䡣
* ÿ�������ռ�Ŀռ�ָ���ת��Ϊ `DIRECTORY_SEPARATOR` ��ʱ����ԴӴ��̼����ļ���
* û������������ `_` �ַ���ʱ��ת���� `DIRECTORY_SEPARATOR`�� `_` �ַ��������ռ���
  û���������塣
* ��ȫ�޶��������ռ���Ϻ�׺ `.php` �ɴ��ļ�ϵͳ���롣
* �� vendor names, namespaces, class name����Сд��ĸ��д��ĸ����ϡ�

����
----

* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/path/to/project/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/path/to/project/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/path/to/project/lib/vendor/Zend/Mail/Message.php`

ǿ�������ռ������
------------------
* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`

�ù淶�ƶ�������Զ����ر�׼�� �������PHP5.3�汾ʹ�ü򵥵�SplClassLoader�ӿڲ��ԡ�

ʵ��
----

�����������Ӵӹ����ϼ���ʾ������׼���Զ����ػ��ơ�

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

SplClassLoaderʵ��
------------------

����Ҫ��������������Ŀ������SplClassLoaderʵ�֣� ��ʱPHP5.3Ŀǰ�Զ����ص��Ƽ���ʽ��

* [http://gist.github.com/221634](http://gist.github.com/221634)

