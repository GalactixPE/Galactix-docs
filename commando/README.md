<h1>Commando<img src="https://raw.githubusercontent.com/CortexPE/Commando/master/commando.png" height="64" width="64" align="left"></img>&nbsp;</h1>
<br />

A PocketMine-MP Virion for easier implementation of dynamic commands, including support for Minecraft: Bedrock Edition argument listing aimed for both the end users and the plugin developers.

## Basic Usage:

***NOTE: Other miscellaneous functions can be indexed within your IDEs or by reading the source code. This is only the basic usage of the virion, it does not show every aspect of it as that'd be too long to document.***

### Create your command class
In our command class, we need to extend `BaseCommand` and implement its required methods to use all of Commando's features.
```php
<?php

use CortexPE\Commando\BaseCommand;
use pocketmine\command\CommandSender;

class MyCommand extends BaseCommand {
	protected function prepare(): void {
		// This is where we'll register our arguments and subcommands
	}
	
	public function onRun(CommandSender $sender, string $aliasUsed, array $args): void {
		// This is where the processing will occur if it's NOT handled by other subcommands
	}
}
```

### Register the arguments
If we register arguments, we need to import and use / extend (if needed) the provided argument objects.
```php
use GalactixPE\CityCore\libs\Commando\args\RawStringArgument;

	protected function prepare(): void {
		// $this->registerArgument(position, argument object (name, isOptional));
		$this->registerArgument(0, new RawStringArgument("name", true));
	}
```

### Handling our arguments
The arguments passed on our `onRun` method will be mapped by `name => value` this makes it easy to understand which argument is which, instead of using numeric indices. It is also guaranteed that the arguments passed will be the declared type that we've set.
```php
	public function onRun(CommandSender $sender, string $aliasUsed, array $args): void {
		if(isset($args["name"])){
			$sender->sendMessage("Hello, " . $args["name"] . "!");
		} else {
			$this->sendUsage();
		}
	}
```

### Registering the command from a module
Once we've constructed our command with our arguments and subcommands, we can now register our command to PocketMine's command map, to be available to our users.
```php
// onEnable:
$this->registerCommand(new MyCustomCommand($this, "examplecommand", "My Description"));
```
The only difference with using this framework is that you don't need to set the usage message, as they are pre-generated after all the arguments have been registered.

### SubCommands
Subcommands work the same way as regular commands, the only difference is that they're registered on the parent command with `BaseCommand->registerSubCommand()` having their own set of arguments and own usage message.

### Error messages
The virion provides default error messages for user input errors regarding the arguments given. It also provides a way to register your own error message formats for the sake of customizability.
```php
$cmdCtx->setErrorFormat($errorCode, $format);
// Arrays can be passed on `BaseCommand->setErrorFormats()` to bulk-set other error messages
```
The error messages are sent in bulk to the users to let them know what parts are wrong with their input, not having to do trial-and-error.
*A current limitation is that, you cannot register your own error messages with other error codes.*

-----
**This framework was made with :heart: by CortexPE, Enjoy!~ :3**
