#  RedisDb - PHP Redis Class
### Simple Class

### Installation
To utilize this class, first import RedisDb.php into your project, and require it.
```php
require_once ('RedisDb.php');
```
### Installation with composer
It is also possible to install library via composer
```bash
composer require saleh7/redisdb:dev-master
```
### Initialization
```php
$configure = [
    'host'      => '127.0.0.1'  // default
    'port'      => '6379',      // default
    'prefix'    => 'RedisDb',   // default
    'autoid'    => true,        // default
    'cu'        => false,       // default
];
RedisDb::init($configure);
```

### Insert
Simple example
```php
$data = [
  'name'       => 'Saleh',
  'age'        => 36,
  'phone'      => '490000000',
  'email'      => 'Saleh7@protonmail.ch',
  'password'   => '#######@@$/',
];
$id = RedisDb::insert('member', $data);
if($id)
    echo 'user was created. Id=' . $id;
```

### Insert multiple
Simple example
```php
$data = Array(
    Array (
      'name'       => 'Saleh',
      'age'        => 36,
      'phone'      => '490000000',
      'email'      => 'Saleh7@protonmail.ch',
      'password'   => '#######@@$/',
    ),
    Array (
      'name'       => 'Ahmad',
      'age'        => 22,
      'phone'      => '490000000',
      'email'      => 'Ahmad@++.ch',
      'password'   => 'test###',
    )
);
$ids = RedisDb::insertMulti('member', $data);
if($ids)
  echo 'new users inserted with following id\'s: ' . implode(', ', $ids);
```
##### If all datasets only have the same keys, it can be simplified
```php
$data = Array(
    Array ("admin", 36, "490000000", 'Saleh7@protonmail.ch'),
    Array ("other", 22, "490000001", 'Ahmad@++.ch')
);
$keys = Array("name", "age", "phone", "email");
$ids = RedisDb::insertMulti('member', $data, $keys);
if($ids)
  echo 'new users inserted with following id\'s: ' . implode(', ', $ids);
```
### Update
```php
$data = [
  'name'       => 'Abdallah',
  'age'        => 33,
  'email'      => 'Abdallah@protonmail.ch',
];
RedisDb::where('name', 'Saleh');
RedisDb::update('member', $data);
```
#####  update() also support limit parameter:
```php
RedisDb::update('member', $data, 2);
```
### Get
```php
RedisDb::get('member'); //contains an Array of all members 
RedisDb::get('member', 2); //contains an Array 2 members

RedisDb::where('name', 'Saleh');
//RedisDb::where('age', 33);
RedisDb::get('member'); // get member/members By name
```

#####  or Get just one row
```php
RedisDb::where('age', 33);
RedisDb::getOne('member');
```

###  Where
Regular == operator with variables:
```php
RedisDb::where('age', 33);
RedisDb::where('name', 'Saleh');
RedisDb::get('member');
```
#####  OR CASE:
```php
RedisDb::where('name', 'Saleh');
RedisDb::orWhere('name', 'Abdallah');
RedisDb::get('member');
```
##### Regular == operator with column to column comparison:
```php
//RedisDb::where('age', 33, '>=');
RedisDb::where('age', 33, '>');
RedisDb::get('member');
```

### Delete
```php
RedisDb::where('age', 33);
RedisDb::delete('member');
```

### setKey
```php
RedisDb::setKey('settings:lang', 'en'); // setKey($keyName, $value, $Options = null)
```

### getKey
```php
RedisDb::getKey('settings:lang');
```

### deleteKey
```php
RedisDb::deleteKey('settings:lang');
```

### Redis
#### [PhpRedis](https://github.com/phpredis/phpredis#classes-and-methods) 
```php
RedisDb::Redis()->set('settings:lang', 'en');
RedisDb::Redis()->get('settings:lang');
RedisDb::Redis()->delete('settings:lang');
RedisDb::Redis()->hSet('user', 'u1', 'Saleh');
RedisDb::Redis()->hGet('user', 'u1');
RedisDb::Redis()->hDel('user', 'u1');
```

License
----

MIT
