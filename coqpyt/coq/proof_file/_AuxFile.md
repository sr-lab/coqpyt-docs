# `_AuxFile`

An abstraction over a temporary file created by CoqPyt to be used to get information about the context of Rocq files and to load imported libraries.

## Attributes

`coq_lsp_client : CoqLspClient` [CoqLspClient](../lsp/client/CoqLspClient.md)
> coq-lsp client used on the file.

`path : str`
> Path of the file. Does not actually use the direct file path given, instead it places it in a temporary directory with a hashed name.

`version : int`
> Version of current file. Increments after each change to the file.

`__copy : bool`
> Whether the AuxFile should copy the contents of the file this object abstracts into the AuxFile's actual location.


## Operations

```python
__init__(self, file_path: str, coq_lsp_options: Tuple[str], copy: bool = False, workspace: Optional[str] = None, timeout: int = 30)
```
> Creates a new AuxFile object
> 
> `file_path : str`
> > Path to the file this auxiliary file is created for.
> 
> `coq_lsp_options : Optional[Tuple[str]]`
> > *Optional.* Options to be passed to the coq-lsp on startup. Defaults to None.
> 
> `copy : bool = False`
> *Optional.* Whether the AuxFile should copy the contents of the file this object abstracts into the AuxFile's actual location. Defaults to False.
> 
> `workspace : Optional[str] = None`
> *Optional.* Absolute path for the workspace. If the workspace is not defined, the workspace is equal to the path of the file. Defaults to None.
> 
> `timeout : int = 30`
> *Optional.* Timeout used in coq-lsp. Defaults to 30.

```python
_handle_exception(self, e) -> None
```
> Shuts down the LSP client if `e` is a server error and deletes the file.
> 
> `e : any`
> > Error to handle.

```python
get_diagnostics(self, keyword: str, search, line: int) -> Optional[str]
```
> Gets the diagnostic message of the command that starts with `keyword` and ends with `search`, located on the given line of the file.
> 
> `keyword : str`
> > Start of the command's text.
> 
> `search : any`
> > End of the command's text.
> 
> `line : int`
> > Line the command should be located on.
> 
> Returns: `Optional[str]` The message of the diagnostic if all requirements match.

```python
read(self) -> str
```
> Reads the contents of the auxiliary file.
> 
> Returns: `str` String containing the entire file.

```python
write(self, text: str) -> None
```
> Overwrites the file with the string stored in `text`.
> 
> `text : str`
> > Text to write to the file.

```python
append(self, text: str) -> None
```
> Appends the string stored in `text` to the end of the file.
> 
> `text : str`
> > Text to append.

```python
truncate(self, text: str) -> None
```
> Deletes all data in the file after the last occurrence of `text`.
> 
> `text : str`
> > Text to truncate after.

```python
didOpen(self) -> None
```
> Tells the Rocq LSP client to open the current file and parse it.

```python
didChange(self) -> None
```
> Tells the Rocq LSP client that the file was changed and should be re parsed.

```python
close(self)
```
> Shuts down the LSP client and deletes the auxiliary file.

```python
__init_path(self, file_path: str) -> None
```
> Initializes the path to the file by creating a new file in the directory of `file_path` to be used as the auxiliary file.
> 
> `file_path : str`
> > Path to the file this auxiliary file is created for.

```python
__get_queries(self, keyword: str) -> List[Query]
```
> Searches through every diagnostic created for the file. If the start of the text of the command that the diagnostic was created for is equal to `keyword`, the diagnostic gets added to the returned list of queries. The value of `query` for the query is the remaining text of the command referenced.
> 
> `keyword : str`
> > The keyword to search the file with.
> 
> Returns: `List[Query]` [Query](../lsp/structs/Query.md) The list of all queries found in the search.


## Static Operations

```python
set_cache_size(size: Optional[int]) -> None
```
> Sets the size of the Least Recently Used cache for the `__load_library` helper function.
> 
> `size : Optional[int]`
> > New size of the cache.

```python
get_coqpyt_disk_cache_loc(cls) -> Optional[str]
```
> Gets the location of the CoqPyt library cache in the filesystem.
> 
> Returns: `Optional[str]` Path to the library cache directory.

```python
get_from_disk_cache(cls, library_hash: str) -> Optional[Dict[str, Term]]
```
> Gets the cached library file specified by the hash and decompresses it.
> 
> `library_hash : str`
> > String hash of the library.
> 
> Returns: `Optional[Dict[str, Term]]` [Term](../structs/Term.md) Dictionary representing the context defined by this file.

```python
to_disk_cache(cls, library_hash: str, terms: Dict[str, Term]) -> None
```
> Takes the term context of a library and compresses it to be stored in a cache file.
> 
> `library_hash : str`
> > String hash of the library.
> 
> `terms : Dict[str, Term]` [Term](../structs/Term.md)
> > Collection of terms defined in this library.

```python
get_library(cls, library_name: str, library_file: str, timeout: int, coq_lsp_options: Tuple[str], workspace: Optional[str] = None, use_disk_cache: bool = False) -> Dict[str, Term]
```
> Gets all terms defined in the specified library. If use disk cache is True, the function will attempt to read the cached context before reevaluating the library file. The file will then be cached if it wasn't already.
> 
> `library_name : str`
> > Name of the library to get.
> 
> `library_file : str`
> > File path to where the library is defined.
> 
> `timeout : int`
> > Timeout used in coq-lsp.
> 
> `coq_lsp_options : Tuple[str]`
> > Options to be passed to the coq-lsp on startup.
> 
> `workspace : Optional[str] = None`
> *Optional.* Absolute path for the workspace. If the workspace is not defined, the workspace is equal to the path of the file. Defaults to None.
> 
> `use_disk_cache : bool = False`
> > *Optional.* Whether CoqPyt should attempt to load/save the current library to/from the library cache. Defaults to False.
> 
> Returns: `Dict[str, Term]` [Term](../structs/Term.md)

```python
get_libraries(aux_file: _AuxFile) -> List[str]
```
> Gets the list of libraries used referenced by the auxiliary file.
> 
> `aux_file : _AuxFile`
> > File where the libraries are listed.
> 
> Returns: `List[str]` The list of libraries.

```python
get_coq_context(timeout: int, workspace: Optional[str] = None, use_disk_cache: bool = False, coq_lsp_options: Tuple[str] = None) -> FileContext
```
> Gets the context of all terms defined by libraries that are imported in to Rocq files by default. It does this by creating an empty file, listing all the libraries used by the file, then loading each library separately to get their terms.
> 
> `timeout : int`
> > Timeout used in coq-lsp.
> 
> `workspace : Optional[str] = None`
> *Optional.* Absolute path for the workspace. If the workspace is not defined, the workspace is equal to the path of the file. Defaults to None.
> 
> `use_disk_cache : bool = False`
> > *Optional.* Whether CoqPyt should attempt to load/save the current library to/from the library cache. Defaults to False.
> 
> `coq_lsp_options : Optional[Tuple[str]]`
> > *Optional.* Options to be passed to the coq-lsp on startup. Defaults to None.
> 
> Returns: `FileContext` [FileContext](../context/FileContext.md) Context containing all terms defined in the default libraries.

```python
__load_library(library_name: str, library_file: str, library_hash: str, timeout: int, coq_lsp_options: Tuple[str] = None, workspace: Optional[str] = None) -> FileContext
```
> Opens up the file for this library as a CoqFile then executes every step in the file. After execution, it gets all terms defined then closes the file.
> 
> `library_name : str`
> > Name of the library.
> 
> `library_file : str`
> > File path to where the library is defined.
> 
> `library_hash : str`
> > String hash of the library.
> 
> `timeout : int`
> > Timeout used in coq-lsp.
> 
> `coq_lsp_options : Optional[Tuple[str]]`
> > *Optional.* Options to be passed to the coq-lsp on startup. Defaults to None.
> 
> `workspace : Optional[str] = None`
> *Optional.* Absolute path for the workspace. If the workspace is not defined, the workspace is equal to the path of the file. Defaults to None.
> 
> Returns: `FileContext` [FileContext](../context/FileContext.md) Context containing all terms that were defined in the file.