# `LspClient`

LspClient is used to communicate with an instance of a language server, providing methods for basic method calls and notifications. This class is used only to abstract away the names and behaviors of the each method call and does not handle how the messages are actually sent (see [LspEndpoint](../endpoint/LspEndpoint.md)). More information about what each operation returns such as the structure of method responses can be found [here](https://microsoft.github.io/language-server-protocol/specifications/lsp/3.17/specification/)

## Attributes

`lsp_endpoint : LspEndpoint` [LspEndpoint](../endpoint/LspEndpoint.md)
> Endpoint used to provide abstractions for communicating with the language server.


## Operations

```python
__init__(self, lsp_endpoint: LspEndpoint)
```
> Constructs a new LspClient instance.
> 
> `lsp_endpoint : LspEndpoint` [LspEndpoint](../endpoint/LspEndpoint.md)
> > Language server endpoint.

```python
initialize(self, processId: int, rootPath: str, rootUri: str, initializationOptions, capabilities: Dict, trace: str, workspaceFolders: List) -> Dict
```
> The initialize request is sent as the first request from the client to the server. If the server receives a request or notification before the initialize request it should act as follows:
> 1. For a request the response should be an error with code: -32002. The message can be picked by the server.
> 2. Notifications should be dropped, except for the exit notification. This will allow the exit of a server without an initialize request.
> 
> Until the server has responded to the initialize request with an InitializeResult, the client must not send any additional requests or notifications to the server. In addition the server is not allowed to send any requests or notifications to the client until it has responded with an InitializeResult, with the exception that during the initialize request the server is allowed to send the notifications window/showMessage, window/logMessage and telemetry/event as well as the window/showMessageRequest request to the client.
> 
> The initialize request may only be sent once.
> 
> This method also initializes the lsp endpoint to assist with the sending of messages.
> 
> `processId : int`
> > The process Id of the parent process that started the server. Is null if the process has not been started by another process. If the parent process is not alive then the server should exit (see exit notification) its process.
> 
> `rootPath : str`
> > The rootPath of the workspace. Is null if no folder is open. Deprecated in favour of rootUri.
> 
> `rootUri : str`
> > The rootUri of the workspace. Is null if no folder is open. If both `rootPath` and `rootUri` are set `rootUri` wins.
> 
> `initializationOptions : Any`
> > User provided initialization options.
> 
> `capabilities : Dict`
> > The capabilities provided by the client (editor or tool).
> 
> `trace : str`
> > The initial trace setting. If omitted trace is disabled ('off').
> 
> `workspaceFolders : List`
> > The workspace folders configured in the client when the server starts. This property is only available if the client supports workspace folders. It can be `null` if the client supports workspace folders but none are configured.
> 
> Returns: `Dict` Response of the `"initialize"` method call, containing the capabilites of the server, its name, and also its version.

```python
initialized(self) -> None
```
> The initialized notification is sent from the client to the server after the client received the result of the initialize request but before the client is sending any other request or notification to the server. The server can use the initialized notification for example to dynamically register capabilities. The initialized notification may only be sent once.

```python
shutdown(self) -> Any
```
> The shutdown request is sent from the client to the server. It asks the server to shut down, but to not exit (otherwise the response might not be delivered correctly to the client). There is a separate exit notification that asks the server to exit. Clients must not send any notifications other than `exit` or requests to a server to which they have sent a shutdown request. Clients should also wait with sending the `exit` notification until they have received a response from the `shutdown` request.
> 
> Returns: `Any` Response of the `"shutdown"` method call. If an exception occurs, the error will be returned.

```python
exit(self) -> None
```
> A notification to ask the server to exit its process. The server should exit with `success` code 0 if the shutdown request has been received before; otherwise with `error` code 1.

```python
didClose(self, textDocument: TextDocumentIdentifier) -> None
```
> The document close notification is sent from the client to the server when the document got closed in the client. The document’s master now exists where the document’s Uri points to (e.g. if the document’s Uri is a file Uri the master now exists on disk). As with the open notification the close notification is about managing the document’s content. Receiving a close notification doesn’t mean that the document was open in an editor before. A close notification requires a previous open notification to be sent. Note that a server’s ability to fulfill requests is independent of whether a text document is open or closed.
> 
> `textDocument : TextDocumentIdentifier` [TextDocumentIdentifer](../structs/TextDocumentIdentifier.md)
> > The document that was closed

```python
didOpen(self, textDocument: TextDocumentItem) -> None
```
> The document open notification is sent from the client to the server to signal newly opened text documents. The document's truth is now managed by the client and the server must not try to read the document's truth using the document's uri. Open in this sense means it is managed by the client. It doesn't necessarily mean that its content is presented in an editor. An open notification must not be sent more than once without a corresponding close notification send before. This means open and close notification must be balanced and the max open count for a particular textDocument is one. Note that a server's ability to fulfill requests is independent of whether a text document is open or closed.
> 
> The DidOpenTextDocumentParams contain the language id the document is associated with. If the language Id of a document changes, the client needs to send a textDocument/didClose to the server followed by a textDocument/didOpen with the new language id if the server handles the new language id as well.
> 
> `textDocument : TextDocumentItem` [TextDocumentItem](../structs/TextDocumentItem.md)
> > The document that was opened.

```python
didChange(self, textDocument: VersionedTextDocumentIdentifier, contentChanges: List[TextDocumentContentChangeEvent]) -> None
```
> The document change notification is sent from the client to the server to signal changes to a text document. In 2.0 the shape of the params has changed to include proper version numbers and language ids.
> 
> `textDocument : VersionedTextDocumentIdentifier` [VersionedTextDocumentIdentifier](../structs/VersionedTextDocumentIdentifier.md)
> > The initial trace setting. If omitted trace is disabled ('off').
> 
> `contentChanges: List[TextDocumentContentChangeEvent]` [TextDocumentContentChangeEvent](../structs/TextDocumentContentChangeEvent.md)
> > The actual content changes. The content changes describe single state changes to the document. So if there are two content changes c1 and c2 for a document in state S then c1 move the document to S' and c2 to S''.

```python
documentSymbol(self, textDocument: TextDocumentItem) -> List[SymbolInformation]
```
> The document symbol request is sent from the client to the server to return a flat list of all symbols found in a given text document. Neither the symbol's location range nor the symbol's container name should be used to infer a hierarchy.
> 
> `textDocument : TextDocumentItem` [TextDocumentItem](../structs/TextDocumentItem.md)
> > The text document.
> 
> Returns: `List[SymbolInformation]` [SymbolInformation](../structs/SymbolInformation.md) Information received about all symbols in the document.

```python
definition(self, textDocument: TextDocumentItem, position: Position) -> List[Location]
```
> The goto definition request is sent from the client to the server to resolve the definition location of a symbol at a given text document position.
> 
> `textDocument : TextDocumentItem` [TextDocumentItem](../structs/TextDocumentItem.md)
> > The text document.
> 
> `position : Position` [Position](../structs/Position.md)
> > The position inside the text document.
> 
> Returns: `List[Location]` [Location](../structs/Location.md) The location of the definitions of the symbol at `position`.

```python
typeDefinition(self, textDocument: TextDocumentItem, position: Position) -> List[Location]
```
> The goto type definition request is sent from the client to the server to resolve the type definition location of a symbol at a given text document position.
> 
> `textDocument : TextDocumentItem` [TextDocumentItem](../structs/TextDocumentItem.md)
> > The text document.
> 
> `position : Position` [Position](../structs/Position.md)
> > The position inside the text document.
> 
> Returns: `List[Location]` [Location](../structs/Location.md) The location of the definitions of the symbol at `position`.

```python
signatureHelp(self, textDocument: TextDocumentItem, position: Position) -> SignatureHelp
```
> The signature help request is sent from the client to the server to request signature information at a given cursor position.
> 
> `textDocument : TextDocumentItem` [TextDocumentItem](../structs/TextDocumentItem.md)
> > The text document.
> 
> `position : Position` [Position](../structs/Position.md)
> > The position inside the text document.
> 
> Returns: `SignatureHelp` [SignatureHelp](../structs/SignatureHelp.md) Information about the symbol at `position`.

```python
completion(self, textDocument: TextDocumentItem, position: Position, context: CompletionContext) -> List[CompletionItem] | CompletionList
```
> The Completion request is sent from the client to the server to compute completion items at a given cursor position. The returned completion items should have the documentation property filled in.
> 
> `textDocument : TextDocumentItem` [TextDocumentItem](../structs/TextDocumentItem.md)
> > The text document.
> 
> `position : Position` [Position](../structs/Position.md)
> > The position inside the text document.
> 
> `context : CompletionContext` [CompletionContext](../structs/CompletionContext.md)
> > The completion context. This is only available if the client specifies to send this using `ClientCapabilities.textDocument.completion.contextSupport === true`.
> 
> Returns: `List[CompletionItem] | CompletionList` [CompletionItem](../structs/CompletionItem.md) [CompletionList](../structs//CompletionList.md) List of possible items that could complete the context. A CompletionList is used if the result from the language server has the `isIncomplete` property.

```python
declaration(self, textDocument: TextDocumentItem, position: Position) -> List[Location] | List[LocationLink]
```
> The go to declaration request is sent from the client to the server to resolve the declaration location of a symbol at a given text document position.
> 
> The result type LocationLink[] got introduce with version 3.14.0 and depends in the corresponding client capability `clientCapabilities.textDocument.declaration.linkSupport`.
> 
> `textDocument : TextDocumentItem` [TextDocumentItem](../structs/TextDocumentItem.md)
> > The text document.
> 
> `position : Position` [Position](../structs/Position.md)
> > The position inside the text document.
> 
> Returns: `List[Location] | List[LocationLink]` [Location](../structs/Location.md) [LocationLink](../structs/LocationLink.md) The location of the declaration of the symbol at `position`.

```python
definition(self, textDocument: TextDocumentItem, position: Position) -> List[Location]
```
> The go to definition request is sent from the client to the server to resolve the declaration location of a symbol at a given text document position.
> 
> The result type LocationLink[] got introduce with version 3.14.0 and depends in the corresponding client capability `clientCapabilities.textDocument.declaration.linkSupport`.
> 
> `textDocument : TextDocumentItem` [TextDocumentItem](../structs/TextDocumentItem.md)
> > The text document.
> 
> `position : Position` [Position](../structs/Position.md)
> > The position inside the text document.
> 
> Returns: `List[Location] | List[LocationLink]` [Location](../structs/Location.md) [LocationLink](../structs/LocationLink.md) The location of the definitions of the symbol at `position`.