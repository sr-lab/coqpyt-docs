# `JsonRpcEndpoint`

Thread safe JSON RPC endpoint implementation. Responsible to receive and send JSON RPC messages, as described in the protocol. More information can be found: https://www.jsonrpc.org/

## Attributes

`stdin`
> Standard input for the coq-lsp process.

`stdout`
> Standard output for the coq-lsp process.

`read_lock : threading.Lock`
> Mutex to prevent multiple threads from reading from `stdout` at once.

`write_lock : threading.Lock`
> Mutex to prevent multiple threads from writing to `stdin` at once.

## Operations

```python
__init__(self, stdin, stdout)
```
> Creates a new JSON RPC Endpoint for sending messages across processes.
> 
> `stdin`
> > Standard input for the coq-lsp process.
> 
> `stdout`
> > Standard output for the coq-lsp process.

```python
send_request(self, message: Dict) -> None
```
> Sends the given message after JSON stringifying it.
> 
> `message : Dict`
> > The message to send.

```python
recv_response(self) -> Dict
```
> Receives a message and converts it to a dictionary.
> 
> Returns: `Dict` The message received.
>
> Raises:
> > `ResponseError` [ResponseError](../structs/ResponseError.md): The `ParseError` code is used if the specified size of the message is not an integer, the header doesn't end with a new line, the size of the body of the message is not an integer, the type of the header is unknown, or no size is provided.

## Static Operations

```python
__add_header(json_string: str) -> str
```
> Adds a header for the given json string.
> 
> `json_string : str`
> > The string to format.
> 
> Returns: `string` The string with the header.