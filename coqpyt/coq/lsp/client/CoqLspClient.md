# `CoqLspClient(LspClient)` [LspClient](../../../lsp/client/LspClient.md)

Abstraction to interact with coq-lsp

## Attributes

`file_progress : Dict[str, List[CoqFileProgressParams]]` [CoqFileProgressParams](../structs/CoqFileProgressParams.md)
> Contains all the `$/coq/fileProgress` notifications sent by the server. The keys are the URIs of the files and the values are the list of notifications.

`__completed_operation : threading.Event`
> Flag used to check if a pending operation has been completed. The flag is set when the LSP client sends the `textDocument/publishDiagnostics` request.

## Operations

```python
__init__(self, root_uri: str, timeout: int = 30, memory_limit: int = 2097152, coq_lsp: str = "coq-lsp", coq_lsp_options: Tuple[str] = None, init_options: Dict)
```
> Creates a CoqLspClient. After starting up the lsp in a new process, it initializes all objects used for communication with the server, then calls the initialization methods on the server.
> 
> `root_uri : str`
> > URI to the workspace where coq-lsp will run The URI can be either a file or a folder.
> 
> `timeout : int = 30`
> > *Optional.* Timeout used for the coq-lsp operations. Defaults to 2.
> 
> `memory_limit : int = 2097152`
> > *Optional.* RAM limit for the coq-lsp process in kilobytes. It only works for Linux systems. Defaults to 2097152.
> 
> `coq_lsp : str = "coq-lsp"`
> > *Optional.* Path to the coq-lsp binary. Defaults to "coq-lsp".
> 
> `coq_lsp_options : Tuple[str] = None`
> > *Optional.* Options to be passed to the coq-lsp on startup. Defaults to None.
> 
> `init_options : Dict`
> > *Optional.* Initialization options for coq-lsp server. Available options are:
> > - max_errors (int): Maximum number of errors per file, after that, coq-lsp will stop checking the file. Defaults to 120000000.
> > - show_coq_info_messages (bool): Show Rocq's info messages as diagnostics. Defaults to false.
> > - show_notices_as_diagnostics (bool): Show Rocq's notice messages as diagnostics, such as `About` and `Search` operations. Defaults to false.
> > - debug (bool): Enable Debug in Rocq Server. Defaults to false. 
> > - pp_type (int): Method to print Rocq Terms. 0 = Print to string. 1 = Use jsCoq's Pp rich layout printer. 2 = Rocq Layout Engine. Defaults to 1.

```python
didOpen(self, textDocument: TextDocumentItem) -> None
```
> Open a text document in the server and waits for the LSP to finish processing the file.
> 
> `textDocument : TextDocumentItem` [TextDocumentItem](../../../lsp/structs/TextDocumentItem.md)
> > Text document to open.

```python
didChange(self, textDocument: VersionedTextDocumentIdentifier, contentChanges: List[TextDocumentContentChangesEvent]) -> None
```
> Submit changes on a text document already open on the server and waits for the LSP to finish processing the file.
> 
> `textDocument : VersionedTextDocumentIdentifier` [VersionedTextDocumentIdentifier](../../../lsp/structs/VersionedTextDocumentIdentifier.md)
> > Text document changed.
> 
> `contentChanges : List[TextDocumentContentChangesEvent]` [TextDocumentContentChangeEvent](../../../lsp/structs/TextDocumentContentChangeEvent.md)
> > Changes made.

```python
proof_goals(self, textDocument: TextDocumentIdentifier, position: Position) -> Optional[GoalAnswer]
```
> Get proof goals and relevant information at a position.
> 
> `textDocument: TextDocumentIdentifier` [TextDocumentIdentifer](../../../lsp/structs/TextDocumentIdentifier.md)
> > Text document to consider.
> 
> `position : Position` [Position](../../../lsp/structs/Position.md)
> > Position used to get the proof goals.
> 
> Returns: `Optional[GoalAnswer]` [GoalAnswer](../structs/GoalAnswer.md) Contains the goals at a position, messages associated to the position and if errors exist, the top error at the position.

```python
get_document(self, textDocument: TextDocumentIdentifier) -> Optional[FlecheDocument]
```
> Get the AST of a text document.
> 
> `textDocument : TextDocumentIdentifier` [TextDocumentIdentifer](../../../lsp/structs/TextDocumentIdentifier.md)
> > Requested text document.
> 
> Returns: `Optional[FlecheDocument]` [FlecheDocument](../structs/FlecheDocument.md) Serialized version of Fleche's document.

```python
save_vo(self, textDocument: TextDocumentIdentifier) -> None
```
> Save a compiled file to disk.
> 
> `textDocument : TextDocumentIdentifier` [TextDocumentIdentifer](../../../lsp/structs/TextDocumentIdentifier.md)
> > File to be saved. The uri in the textDocument should contain an absolute path.

```python
__handle_publish_diagnostics(self, params: Dict) -> None
```
> Callback method used by the LspEndpoint to set the `__completed_operation` flag to true when the endpoint receives the `textDocument/PublishDiagnostics` notification.
> 
> `params : Dict`
> > *Unused.*

```python
__handle_file_progress(self, params: Dict) -> None
```
> Callback method used by the LspEndpoint for when the endpoint receives the `$/coq/fileProgress` notification. When called, it modifies the `file_progress` collection according to 
> 
> `params : Dict`
> > Parameters passed from the LSP server containing information about file progress. Parsed into a [CoqFileProgressParams](../structs/CoqFileProgressParams.md) object.

```python
__wait_for_operation(self) -> None
```
> Helper method used to wait for the LSP server to send `textDocument/PublishDiagnostics` notification. If the wait exceeds the endpoint's timeout, the Rocq LSP client is shutdown.
>
> Raises: 
> > `ResponseError` [ResponseError](../../../lsp/structs/ResponseError.md): If the shutdown flag has been set, the `ServerQuit` error code is used. If the endpoint's timeout is exceeded, the `ServerTimeout` error code is used.