# `lsp` Package

This package provides basic implementation of JSON RPC based LSP client.


## Files and Classes

- `client.py`
    - [`LspClient`](./client/LspClient.md)
- `endpoint.py`
    - [`LspEndpoint`](./endpoint/LspEndpoint.md)
- `json_rpc_endpoint.py`
    - [`JsonRpcEndpoint`](./json_rpc_endpoint/JsonRpcEndpoint.md)
    - [`MyEncoder`](./json_rpc_endpoint/MyEncoder.md)
-  `structs.py`
    - [`Command`](./structs/Command.md)
    - [`CompletionContext`](./structs/CompletionContext.md)
    - [`CompletionItem`](./structs/CompletionItem.md)
    - [`CompletionItemKind`](./structs/CompletionItemKind.md)
    - [`CompletionList`](./structs/CompletionList.md)
    - [`CompletionTriggerKind`](./structs/CompletionTriggerKind.md)
    - [`Diagnostic`](./structs/Diagnostic.md)
    - [`DiagnosticRelatedInformation`](./structs/DiagnosticRelatedInformation.md)
    - [`DiagnosticSeverity`](./structs/DiagnosticSeverity.md)
    - [`ErrorCodes`](./structs/ErrorCodes.md)
    - [`InsertTextFormat`](./structs/InsertTextFormat.md)
    - [`LANGUAGE_IDENTIFIER`](./structs/LANGUAGE_IDENTIFIER.md)
    - [`Location`](./structs/Location.md)
    - [`LocationLink`](./structs/LocationLink.md)
    - [`ParameterInformation`](./structs/ParameterInformation.md)
    - [`Position`](./structs/Position.md)
    - [`Range`](./structs/Range.md)
    - [`ResponseError`](./structs/ResponseError.md)
    - [`SignatureHelp`](./structs/SignatureHelp.md)
    - [`SignatureInformation`](./structs/SignatureInformation.md)
    - [`SymbolInformation`](./structs/SymbolInformation.md)
    - [`SymbolKind`](./structs/SymbolKind.md)
    - [`TextDocumentContentChangeEvent`](./structs/TextDocumentContentChangeEvent.md)
    - [`TextDocumentIdentifier`](./structs/TextDocumentIdentifier.md)
    - [`TextDocumentItem`](./structs/TextDocumentItem.md)
    - [`TextDocumentPositionParams`](./structs/TextDocumentPositionParams.md)
    - [`TextEdit`](./structs/TextEdit.md)
    - [`VersionedTextDocumentIdentifier`](./structs/VersionedTextDocumentIdentifier.md)