# argParser
Option parser for AppleScript.  


## How it works

- an argument starts with `--` works as a fullname key and next is to be the value.  
- an argument starts with `-` works as a shortname key.  
*make sure to call setPropShortNames before parsing else it is treated as fullname.*  
- key-less arguments will be stored in `_` of the result.  

```
setPropShortNames({l:"list",h:"help"})
parse({"-l", "foo", "-h", "--key1", "value1", "--key2", "value2", "namelessValue"})

-- result {_:"namelessValue", list:"foo", help:null, key1:"value1", key2:"value2"}
```

## usage

1. Copy `argParser.scpt` to your script library folder.  
By default it's at `~/Library/Scripts`.  
Running `install.sh` on Terminal will do it instead of you. (Perhaps you need to do `chmod 755 install.sh` before.)  

2. See [sample.scpt](sample.scpt)

```
on run argv
	-- load script to object
	set parser to load script file ((path to scripts folder as string) & "argParser.scpt")
	tell parser
		-- set short names of argument (if needed)
		setPropShortNames({l:"list", h:"help"})
		-- parse argv
		parse(argv)
	end tell
	result
end run
```