# yamltools
A small set of tool to ease working with yaml file on the command line

## yamlxform

This small tools reads a YAML file given as argument or read from STDIN adn prints it to stdout in a form that it's easy greapable.
The output form is based on jsonpath representation. 
The goal is double: easy finding values and jsonpath queries for the lazy people.
For example using yaml.org 1.2 spec example 2.28
```sh

 $ echo "
> ---
> Time: 2001-11-23 15:01:42 -5
> User: ed
> Warning:
>   This is an error message
>   for the log file
> ---
> Time: 2001-11-23 15:02:31 -5
> User: ed
> Warning:
>   A slightly different error
>   message.
> ---
> Date: 2001-11-23 15:03:17 -5
> User: ed
> Fatal:
>   Unknown variable "bar"
> Stack:
>   - file: TopClass.py
>     line: 23
>     code: |
>       x = MoreObject("345\n")
>   - file: MoreClass.py
>     line: 58
>     code: |-
>       foo = bar
> " | yamlxform
---
.User=ed
.Warning=This is an error message for the log file
---
.User=ed
.Warning=A slightly different error message.
---
.User=ed
.Fatal=Unknown variable bar
.Stack[0].file=TopClass.py
.Stack[0].code=x = MoreObject(345n)

.Stack[1].file=MoreClass.py
.Stack[1].code=foo = bar
```
