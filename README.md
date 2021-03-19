# CMUX
A configuration file multiplexer written in bash.

## Example Usage

Sometimes I want to passthrough my GPU for use in a VM. Sometimes I want to use my GPU on my host OS. <br>
I can use cmux to switch between these configuations without manually editing files.

To set this up I need to complete the following steps in order.

Manually configure `/etc/default/grub` and `/etc/mkinitcpio.conf` to enable GPU passthrough
```
cmux add /etc/default/grub GPUPassthroughEnable
cmux add /etc/mkinitcpio.conf GPUPassthroughEnable
```

Manually configure `/etc/default/grub` and `/etc/mkinitcpio.conf` to disable GPU passthrough
```
cmux cp GPUPassthroughEnable GPUPassthroughDisable
cmux update GPUPassthroughDisable
```


Now just switch between the configurations at will.
```
cmux apply GPUPassthroughEnable
```
or
```
cmux apply GPUPassthroughDisable
```

## Help

```
 _____ _____ _____ __ __ 
|     |     |  |  |  |  |
|   --| | | |  |  |-   -|
|_____|_|_|_|_____|__|__|
By Erik Olsen 

--Help--
-a|add <File> <State>   : Adds <File> to <State>
-c|cp <State1> <State2> : Copy state <State1> to state <State2>
-r|rm <State>           : Removes state <State>
-l|ls                   : Lists all states
-l|ls <State>           : Lists the contents of <State> as a tree
-A|apply <State>        : Apply <State> by copying its contents to the original locations
-u|update <State>       : Updates the files of <State> with the current files
-h|help                 : Display this text

Warning: CMUX does not contain any safety features. Be careful what you type because all changes are perminant.
```
