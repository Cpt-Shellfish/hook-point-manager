# hook-point-manager
[![dicord](https://img.shields.io/discord/727190419158597683)](https://discord.gg/9NqwJqP)

Automatically creates and manages new hook points for modified shops.

## About
With this module, developers can easily create and manage new hook points for the auto_include system of *modified eCommerce shops*. With the help of this module, all modules can be developed to be updateable.

## Installation
You can install this module with the [Modified Module Loader Client (MMLC)](http://module-loader.de).

Search for: `robinthehood/hook-point-manager`

## How to use

### Default Hook Points (recommended)
In this example you can create hook points from the directory */new_files/vendor-no-composer/robinthehood/HookPointManager/Classes/DefaultHookPoints/*. It's better to look here for a hook point or make a pull request to add a new hook point:

```php
use RobinTheHood\HookPointManager\Classes\HookPointManager;

$hookPointManager = new HookPointManager();
$hookPointManager->registerDefault();
$hookPointManager->update();
```

### Create your own very special Hook Point (not recommended)
If you need a very special hook point, you can create your own without a Pull Request. This hook point is only usable for you, your projects and your module. This is **not recommended** if you can avoid it with a default hook point. You can find default hook points in */new_files/vendor-no-composer/robinthehood/HookPointManager/Classes/DefaultHookPoints/* or add a new default hook point with a pull request. If you still need your very super special hook point you can use the following code:

```php
$hookPointManager = new HookPointManager();

$hookPointManager->registerHookPoint([
    'name' => 'mc-my-hook-point-name',
    'module' => 'my-company/my-first-module',
    'file' => '/create_account.php',
    'hash' => '2b5ce65ba6177ed24c805609b28572a7',
    'line' => 30,
    'include' => '/includes/extra/my-company/my-first-module/create_account/'
], ['2.0.4.1', '2.0.4.2', '2.0.5.1']);
```

## Reference

### array $hookPoint
| index   | description                                          | example value                       |
|---------|------------------------------------------------------|-------------------------------------|
| name    | unique name of the hook point                        | mc-my-hook-point-name               |
| module  | module name of hook point creator                     | my-company/my-first-module          |
| file    | file path in which the hook point is to be installed | /create_account.php                 |
| hash    | md5-Hash of original unmodified file                 | 2b5ce65ba6177ed24c805609b28572a7    |
| line    | line after which the hook point is to be installed   | 30                                  |
| include | auto_include directory for the hook point files      | /includes/extra/.../create_account/ |

### HookPointManager::registerHookPoint(array $hookPoint, array $versions)
