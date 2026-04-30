# `Command`

Represents specific commands that can be run by the code editor.

## Attributes

`title : str`
> Title of the command, like `save`.

`command : str`
> The identifier of the actual command handler.

`arguments : List`
> Arguments that the command handler should be invoked with.


## Operations

```python
__init__(self, title: str, command: str, arguments: List)
```
> Constructs a new Diagnostic instance.
> 
> `title : str`
> > Title of the command, like `save`.
> 
> `command : str`
> > The identifier of the actual command handler.
> 
> `arguments : List`
> > Arguments that the command handler should be invoked with.