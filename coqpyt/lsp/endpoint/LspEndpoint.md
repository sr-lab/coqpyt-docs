# `LspEndpoint(Thread)`

Endpoint used to handle sending and receiving messages to and from the language server. This object runs as a separate thread from the rest of the application to allow it to always be listening for responses from the server.

## Attributes

`json_rpc_endpoint : JsonRpcEndpoint` [JsonRpcEndpoint](../json_rpc_endpoint/JsonRpcEndpoint.md)
> Protocol used to assist in sending JSON messages to and from the language server.

`method_callbacks : Dict[str, Callable]`
> Collection of callbacks to run when the endpoint receives the response to a method call. Each callback is keyed by the notification is listens for.

`notify_callbacks : Dict[str, Callable]`
> Collection of callbacks to run when the endpoint receives specific notifications. Each callback is keyed by the notification is listens for.

`event_dict : Dict[int, threading.Condition]`
> Dictionary holding multithreaded locks for waiting methods. Each lock is keyed by the index of the called method.

`response_dict : Dict[int, Any]`
> Dictionary holding the results of method calls, keyed by the ID of the method call.

`next_id : int`
> The next ID to be used when calling a method. Gets incremented by 1 after each call.

`timeout : int`
> Max time to wait for the language server to respond to a method call. 

`shutdown_flag : bool`
> Whether the server should be signaled to shutdown.

`diagnostics : Dict[str, List[Diagnostic]]` [Diagnostic](../structs/Diagnostic.md)
> Contains all diagnostics keyed by the current file URI. Updated whenever the endpoint receives the `"textDocument/publishDiagnostics"` method call.


## Operations

```python
__init__(self, json_rpc_endpoint, method_callbacks = {}, notify_callbacks = {}, timeout = 2)
```
> Creates a new LspEndpoint to communicate with a language server.
> 
> `json_rpc_endpoint : JsonRpcEndpoint` [JsonRpcEndpoint](../json_rpc_endpoint/JsonRpcEndpoint.md)
> > Protocol used to assist in sending JSON messages to and from the language server.
> 
> `method_callbacks : Dict = {}`
> > *Optional.* Collection of callbacks to run when the endpoint receives the response to a method call. Defaults to empty.
> 
> `notify_callbacks : Dict = {}`
> > *Optional.* Collection of callbacks to run when the endpoint receives specific notifications. Defaults to empty.
> 
> `timeout : int = 2`
> > *Optional.* Max time to wait for the language server to respond to a method call. Defaults to 2.

```python
handle_result(self, rpc_id: int, result, error) -> None
```
> Takes the data received from the language server, adds it to the `response_dict` attribute associated with `rpc_id`, then sets the lock associated with `rpc_id` to notify any awaiting method handlers that the method is completed.
> 
> `rpc_id : int`
> > ID of the sent message.
> 
> `result : Any`
> > Result received from the language server.
> 
> `error : Any`
> > Any errors received from the language server.

```python
stop(self) -> None
```
> Halts the endpoint.

```python
run(self) -> None
```
> Initiates the endpoint to listen for messages over `json_rpc_endpoint` and handle any messages that arrive.
> 
> Raises:
> > `ResponseError` [ResponseError](../structs/ResponseError.md): If the language server attempts to call a method on the client which is not defined in `method_callbacks`, the `MethodNotFound` error code is used.

```python
send_response(self, id: int, result, error) -> None
```
> Sends a response message back to the language server specified by `id`.
> 
> `id : int`
> > ID of the method called by the language server.
> 
> `result`
> > Result of handling the method.
> 
> `error`
> > Any errors created in handling the method.

```python
send_message(self, method_name: str, params, id: Optional[int] = None) -> None
```
> Sends a message to the language server. Messages are specific types of requests where the server does not respond.
> 
> `method_name : str`
> > Name of the lsp method to call.
> 
> `params`
> > Parameters to pass to the method.
> 
> `id : Optional[int] = None`
> > *Optional.* ID of the method for tracking the server's response. Defaults to None.

```python
call_method(self, method_name: str, **kwargs) -> Any
```
> Sends a message to the language server and awaits a response. If `timeout` is reached, the method fails.
> 
> `method_name : str`
> > Name of the lsp method to call.
> 
> `**kwargs`
> > Parameters to pass to the method.
> 
> Returns: `Any` The response received from the language server.
>
> Raises:
> > `TimeoutError`: If the method call takes longer to respond than the timeout.
> > `ResponseError` [ResponseError](../structs/ResponseError.md): If the server returns an error from the method call.

```python
send_notification(self, method_name, **kwargs) -> None
```
> Sends a message to the language server.
> 
> `method_name : str`
> > Name of the lsp method to call.
> 
> `**kwargs`
> > Parameters to pass to the method.