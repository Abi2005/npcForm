# NpcForm
**NpcForm is a PocketMine-MP plugin that allows plugins to create and managing NpcForms!**

### Usage
You'll first need to import the `Scarce\NpcForm\NpcForm` and `Scarce\NpcForm\NpcFormHandler` class. This and NpcFormHandler should be the only classes required to create and manage NpcForms.
```php
<?php
use Scarce\NpcForm\NpcForm;
use Scarce\NpcForm\NpcFormHandler;
```
**NOTE:** \
-You should register the NpcFormEventHandler so that callables work by using\
```php
<?php
use Scarce\NpcForm\NpcFormHandler;
/** @var Plugin $plugin */
if (!NpcFormHandler::isRegistered()){
    NpcFormHandler::register($plugin);
}
```
-For the player to be able to see the form, they have to right-click on the NPC Entity. \
-NPC Entities despawn on server restart since their form data isn't saved after server restart. You can make them save by setting the form entity to save with chunk by doing `$form->getEntity()->setCanSaveWithChunk(true)`

**Creating a NpcForm Instance**\
Creating a NpcForm Instance is relatively simple and is similar to creating a FormAPI form.
You first have to instantiate a NpcForm`$form = new NpcForm()`The NpcForm takes two required parameteres and two non-required parameter `$form = new NpcForm(Callable $callable, Position $position, $yaw = 90, $pitch = 0)`
The callable paramter takes a player object and an integer paramenter which will be null if no response is given
```php
<?php
/** @var Position $position */
/** @var string $title */
//$position is where the NpcEntity will spawn
$form = new NpcForm(function(Player $player, ?int $data), $position, $yaw, $pitch);
```
To set the title of the form(and the NpcEntity) use:
```php
/** @var string $title */
$form->setTitle($title);
```
You can aslo set the content of the NpcForm by using
```php
/** @var string $content */
$form->setContent($title);
```
And most importantly, you can add buttons by using:
```php
/** @var string $name */
$form->addButton($name);
```
It is also possible to get the NPC Entity that corresponds with your Form by using:
```php
$form->getEntity();
```
To spawn the NPC to a player use:
```php
/** @Player $player */
$form->spawnTo(Player $player);
```
You can also spawn the entity to all players by using
```php
$form->spawnToAll();
```
Handiling NpcForm Callables
This will show an example of how to use the callable in the NpcForm class
```php
<?php
use Scarce\NpcForm\NpcForm;

public function sendNpcForm(Player $player){
        $form = new NpcForm(function(Player $player, ?int $data){
            //$data can be an integer, 0 is the first button, 1 is the second button etc...
            if ($data === null){
                return;
            }
            $player->sendMessage("$data");
        }, $player->asPosition(), $player->yaw, $player->pitch);
        
        $form->setTitle("Number Selector");
        $form->setContent( "Chose a Button!");
        $form->addButton("0");
        $form->addButton("1");
        $form->addButton("2");
        $form->addButton("3");
        $form->addButton("4");
        $form->addButton("5");
        //Sending The Form entity to only $player
        $form->spawnTo($player);
    }
```     
To Do
Help with any of the todo list objectives is accepted

-Save Npc Data on Server Reset[]\
-Find a way to force the client to interact with an entity[]





