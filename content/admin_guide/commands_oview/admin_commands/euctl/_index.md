+++
title = "euctl"
weight = 10
+++


## Syntax


    euctl [-Anr] [-d | -s] NAME ...
    euctl [-nq] NAME=VALUE ...
    euctl [-nq] NAME=@FILE ...
    euctl --dump [--format {raw,json,yaml}] NAME
    euctl --edit [--format {raw,json,yaml}] NAME


## Positional Arguments


| Argument | Description | 
|  :---- |  :---- | 
| NAME | Output a variable's value. | 
| NAME=VALUE | Set a variable to the specified value and then output it. | 
| NAME=@FILE | Set a variable to that of the specified file's contents, then output it. | 


## Options


| Option | Description | Required | 
|  :---- |  :---- |  :---- | 
| -A, --all-types | List all the known variable names, including structures. Those with string or integer values will be output as usual; for the structured values, the methods of retrieving them are given. | No | 
| -d | Output variables' default values rather than their current values. Note that not all variables have default values. | No | 
| -s | Show variables' descriptions instead of their current values. | No | 
| -n | Suppress output of the variable name. This is useful for setting shell variables. | No | 
| -q | Suppress all output when setting a variable. This option overrides the behavior of the -n parameter. | No | 
| -r, --reset | Reset the given variables to their default values. | No | 
| --dump | Output the value of a structured variable in its entirety. The value will be formatted in the manner specified by the --format option. | No | 
| --edit | Edit the value of a structure variable interactively. The value will be formatted in the manner specified by the --format option. Only one variable may be edited per invocation. When looking for an editor, the program will first try the environment variable VISUAL, then the environment variable EDITOR, and finally the default editor, vi. | No | 
| --format {raw,json,yaml} | Use the specified format when displaying a structured variable.Valid values: raw | json | yamlDefault value: json | No | 


## Examples
When retrieving a variable, a subset of the MIB name may be specified to retrieve a list of variables in that subset. For example, to list all the dns variables: 



    euctl dns

This replaces `euca-describe-properties` . 

When setting a variable, the MIB name should be followed by an equal sign and the new value: 



    euctl dns.enabled=true

This replaces `euca-modify-property -p` . 

To write variables using the contents of the files as their new values rather than typing them into the command line, follow them with `=@` and those file names: 

    euctl cloud.network.network_configuration=@/etc/eucalyptus/network.yaml

This replaces `euca-modify-property -f` . 

Specify a filename to read the values from a file: 

    myproperty=@myvaluefile

It is possible to read or write more than one variable in a single invocation of `euctl` . Just separate them with spaces: 

    euctl one=1 two=2 three four=@4.txt five

In all of these cases, `euctl` will generally output each variable named on its command line, along with its current (and potentially just-changed) value. For example, the output of the command above could be: 

    one = 1 
    two = 2
    three = 3
    four = 4
    five = 5

To reset a variable to its default value, specify the -r option: 



    euctl -r dns.enabled



The information available from euctl consists of integers, strings, and structures. The structured information can only be retrieved by specialized programs and, in some cases, this program's `--edit` and `--dump` options. 


{{% notice note %}}
Refer to this command's manpage for a complete list of environment variables, options, and outputs. 
{{% /notice %}}
