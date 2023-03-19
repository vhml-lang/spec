# Commands

Commands are keywords that will perform actions to change your VHML file. Commands must be executed at the top of a file.

## Imports

Imports allow you to import config values from another VHML file. There are two types of imports

* `import:url`
  * This fetches a VHML file from a url and imports it. Supported protocols: `http`, `https`
* `import:file`
  * This gets a VHML file from a local directory and imports it. If no absolute path is specified, it will look for a VHML file relative to the file you are using this statement in.

Once a file has been imported, you can override keys from that file. The following syntax is how you would import a file

```vhml
::import:file "example.vhml"
::import:url "https://example.com/example.vhml"
```

## Extensions

Extensions are opt-in features for VHML. These can vastly change the syntax. Here is a list of avaliable extensions for VHML:

* `brackets` (TODO)

You can opt in to an extension with the following:

```vhml
::extend brackets
```
