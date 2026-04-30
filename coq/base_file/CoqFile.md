# `CoqFile`

Abstraction to interact with a Rocq file. This object can be used to navigate through the file and observe defined terms. It can also be used to apply edits to the file with automatic checking of whether or not the changes were valid.

## Attributes

`coq_lsp_client : CoqLspClient` [CoqLspClient](../lsp/client/CoqLspClient.md)
> coq-lsp client used on the file.

`ast : List[RangedSpan]` [RangedSpan](../lsp/structs/RangedSpan.md)
> AST of the Rocq file. Each element is a step of execution in the Rocq file.

`steps_taken : int`
> The number of steps already executed.

`context : FileContext` [FileContext](../context/FileContext.md)
> The context defined in the file.

`path : str`
> Path of the file. If the file is from the Rocq library, a temporary file will be used.

`_path : str`
> Path of the actual file used. Points to the temporary file if `path` is from the Rocq library.

`file_module : List[str]`
> Modules where the file is included.

`steps : List[Step]` [Step](../structs/Step.md)
> Steps of the Rocq file. Derived from the ast.

`version : int`
> Version of current file. Increments after each change to the file.

`workspace : Optional[str]`
> Absolute path for the workspace.

`is_valid : bool`
> Whether the Rocq file is valid, contained no errors.

`__from_lib : bool`
> Whether the file's library is from the `Coq.Init` or `Corelib.Init` modules.

`__backup_steps : List[Step]` [Step](../structs/Step.md)
> Holds a backup of all steps. This is used for changes to the Rocq file that could error and would need to be rolled back.

`__index_tracker : List[Optional[int]]`
> Maps the index of steps in `steps` to the index of those same steps in `__backup_steps`.


## Properties

`curr_step : Step` [Step](../structs/Step.md)
> Next step to be executed.

`prev_step : Step` [Step](../structs/Step.md)
> The previously executed step.

`timeout : int`
> The timeout of the coq-lsp client.

`checked : bool`
> True if the whole file was already executed.

`diagnostics : List[Diagnostic]` [Diagnostic](../../lsp/structs/Diagnostic.md)
> The diagnostics of the file. Includes all messages given by Rocq.

`errors : List[Diagnostic]` [Diagnostic](../../lsp/structs/Diagnostic.md)
> The errors of the file. Includes all messages given by Rocq with severity 1.


## Operations

```python
__init__(self, file_path: str, library: Optional[str] = None, timeout: int = 30, memory_limit: int = 2097152, workspace: Optional[str] = None, coq_lsp: str = "coq-lsp", coq_lsp_options: Tuple[str] = None, coqtop: str = "coqtop")
```
>> Creates a CoqFile.
>
> `file_path : str`
> > Path of the Rocq file.
>
> `library : Optional[str] = None`
> > *Optional.* The library of the file. Defaults to None.
>
> `timeout : int = 30`
> > *Optional.* Timeout used in coq-lsp. Defaults to 30
>
> `memory_limit : int = 2097152`
> > *Optional.* RAM limit for the coq-lsp process in kilobytes. It only works for Linux systems. Defaults to 2097152.
>
> `workspace : Optional[str] = None`
> > *Optional.* Absolute path for the workspace. If the workspace is not defined, the workspace is equal to the path of the file. Defaults to None.
>
> `coq_lsp : str = "coq-lsp"`
> > *Optional.* Path to the coq-lsp binary. Defaults to "coq-lsp".
>
> `coq_lsp_options : Optional[Tuple[str]] = None`
> > *Optional.* Options to be passed to the coq-lsp on startup. Defaults to None.
>
> `coqtop : str = "coqtop"`
> > *Optional.* Path to the coqtop binary used to compile the Rocq libraries imported by coq-lsp. This is NOT passed as a parameter to coq-lsp, it is simply used to check the Rocq version in use. Defaults to "coqtop".

```python
_handle_exception(self, e) -> None
```
> Shuts down the lsp client if `e` is a server error and deletes the temporary file if `__from_lib` is true.
> 
> `e : any`
> > Error to handle.

```python
_step(self, sign: int) -> None
```
> Processes or undoes a step and increments or decrements `steps_taken`.
> 
> `sign : int`
> > `1` if processing a step; `-1` if undoing a step.

```python
_make_change(self, change_function, *args) -> None
```
> Backs up all parts of the file, then attempts to call `change_function`. If an exception is thrown during execution, the file gets rolled back.
> 
> `change_function : Callable`
> > Function to run.
> 
> `*args`
> > Parameters to pass to `change_function`.
> 
> Raises: 
> > `InvalidFileException` [InvalidFileException](../exceptions/InvalidFileException.md): If the current file doesn't exist. 

```python
_delete_step(self, step_index: int) -> None
```
> Removes the indicated step, writes the changes to the file, and re executes steps if the file context is past the deleted step.
> 
> `step_index : int`
> > Index of the step to delete.
> 
> Raises: 
> > `InvalidDeleteException` [InvalidDeleteException](../exceptions/InvalidDeleteException.md): If the step at the provided index causes the file to become invalid.

```python
_add_step(self, previous_step_index: int, step_text: str) -> None
```
> Adds the step corresponding to `step_text` after the indicated previous step, writes the changes to the file, and re executes steps if the file context is past the added step.
> 
> `previous_step_index : int`
> > Index of the step to insert the text after.
> 
> `step_text : str`
> > Text to insert, corresponding to a Rocq step.
> 
> Raises: 
> > `InvalidAddException` [InvalidAddException](../exceptions/InvalidAddException.md): If the provided step causes the file to become invalid.

```python
_get_steps_taken_offset(self, changes: List[CoqChange]) -> int
```
> Gets the offset of the total steps taken from its original location after applying the changes in `changes`.
> 
> `changes : List[CoqChange]` [CoqChange](../changes/CoqChange.md)
> > List of changes to apply to the file.
> 
> Returns: `int` The calculated offset.

```python
exec(self, nsteps=1) -> List[Step]
```
> Executes steps in the file.
>
> `nsteps : int = 1`
> > *Optional.* Number of steps to execute. Defaults to 1.
>
> Returns: `List[Step]` [Step](../structs/Step.md) List of steps executed. 

```python
run(self) -> List[Step]
```
> Executes the remaining steps in the file.
>
> Returns: `List[Step]` [Step](../structs/Step.md) List of the remaining steps in the file.

```python
delete_step(self, step_index: int) -> None
```
> Deletes a step from the file. This function will change the original file. If an exception is thrown the file will not be changed.
>
> `step_index : int`
> > The index of the step to remove.
>
> Raises:
> > `InvalidFileException` [InvalidFileException](../exceptions/InvalidFileException.md): If the file being changed is not valid.
> > `InvalidDeleteException` [InvalidDeleteException](../exceptions/InvalidDeleteException.md): If the file is invalid after deleting the step.

```python
add_step(self, previous_step_index: int, step_text: str) -> None
```
> Adds a step to the file. This function will change the original file. If an exception is thrown the file will not be changed.
>
> `previous_step_index : int`
> > The index of the previous step of the new step.
>
> `step_text: str`
> > The text of the step to add.
> 
> Raises:
> > `InvalidFileException` [InvalidFileException](../exceptions/InvalidFileException.md): If the file being changed is not valid.
> > `InvalidAddException` [InvalidAddException](../exceptions/InvalidAddException.md): If the file is invalid after adding the step.

```python
change_steps(self, changes: List[CoqChange]) -> None
```
> Changes the steps of the original Rocq file transactionally. If an exception is thrown the file will not be changed.
>
> `changes : List[CoqChange]` [CoqChange](../changes/CoqChange.md)
> > The changes to be applied to the Rocq file.
> 
> Raises:
> > `InvalidFileException` [InvalidFileException](../exceptions/InvalidFileException.md): If the file being changed is not valid.
> > `InvalidChangeException` [InvalidChangeException](../exceptions/InvalidChangeException.md): If the file is invalid after applying the changes.
> > `NotImplementedError`: If the changes contain a CoqChange that is not a CoqAdd or CoqDelete.

```python
save_vo(self) -> None
```
> Compiles the vo file for this Rocq file.

```python
close(self) -> None
```
> Closes all resources used by this object.

```python
__init_path(self, file_path: str, library: str) -> None
```
> Initializes the path to the file this object represents. If the file is from the Rocq library, a copy of the file will be created.
> 
> `file_path : str`
> > Path of the Rocq file.
> 
> `library : Optional[str]`
> > The library of the file.

```python
__init_step(self, lines: List[str], index: int, step_ast: RangedSpan, prev_step_ast: RangedSpan) -> Step
```
> Creates a new `Step` object representing the step between `step_ast` and `prev_step_ast`.
> 
> `lines : List[str]`
> > List of strings for every line in the file.
> 
> `index : int`
> > Index of the step in the AST.
> 
> `step_ast : RangedSpan` [RangedSpan](../lsp/structs/RangedSpan.md)
> > AST of the current step.
> 
> `prev_step_ast : RangedSpan` [RangedSpan](../lsp/structs/RangedSpan.md)
> > AST of the previous step.
> 
> Returns: `Step` [Step](../structs/Step.md) The `Step` object created.

```python
__init_steps(self, text: str, ast: List[RangedSpan]) -> None
```
> Initializes all steps in the file according to the provided list of AST expressions.
> 
> `text : str`
> > A string containing the entire contents of the file.
> 
> `ast : List[RangedSpan]` [RangedSpan](../lsp/structs/RangedSpan.md)
> > AST of the entire file.

```python
__validate(self) -> None
```
> Updates the diagnostics of each step and sets `is_valid` to true if there are no errors.

```python
__short_text(self, text: str, curr_step: RangedSpan, prev_step: Optional[RangedSpan] = None) -> str
```
> Removes excessive white space and line breaks from the text of the step. 
> 
> `text : str`
> > Lines of the file containing the current step.
> 
> `curr_step : RangedSpan` [RangedSpan](../lsp/structs/RangedSpan.md)
> > AST of the step being considered.
> 
> `prev_step : Optional[RangedSpan] = None` [RangedSpan](../lsp/structs/RangedSpan.md)
> > *Optional.* AST of the previous step. Defaults to None.
> 
> Returns: `str` Trimmed AST text.

```python
__read(self) -> str
```
> Reads the entire file and returns it as a string.
> 
> Returns: `str` File as a string.

```python
__refresh(self) -> None
```
> Notifies the LSP Client that the file was changed.

```python
__update_steps(self) -> None
```
> Reinitializes all steps after the file was changed.

```python
__delete_step_text(self, step_index: int) -> None
```
> Removes the text of a step and writes the changes to the Rocq file.
> 
> `step_index : int`
> > Index of the step to delete.

```python
__add_step_text(self, previous_step_index: int, step_text: str) -> None
```
> Adds the contents of `step_text` after the specified step and writes the changes to the Rocq file.
> 
> `previous_step_index : int`
> > Index of the step to insert the text after.
> 
> `step_text : str`
> > Text to insert, corresponding to a Rocq step.

```python
__delete_update_ast(self, step_index: int) -> None
```
> Deletes a step from the AST and updates the locations of all other steps in the file.
> 
> `step_index : int`
> > Index of the step to delete.

```python
__add_update_ast(self, previous_step_index: int, step_text: str) -> Step
```
> Adds a step to the AST and updates the locations of all other steps in the file.
> 
> `previous_step_index : int`
> > Index of the step to insert the text after.
> 
> `step_text : str`
> > Text to insert, corresponding to a Rocq step.
> 
> Returns: `Step` [Step](../structs/Step.md) The `Step` object created from the text.

```python
__copy_steps(self) -> None
```
> Modifies `steps` to reference the `Step` objects in `__backup_steps` when possible instead of using newly created `Step` objects. If the new `Step` was changed, the changes are transferred over.

```python
__set_backup_steps(self) -> None
```
> Initializes `__backup_steps` and `__index_tracker` based on the current steps in preparation of changes to the file.

```python
__change_steps(self, changes: List[CoqChange]) -> None
```
> Iterates over the provided changes and updates the AST, file, and context to reflect all changes made to the file.
> 
> `changes : List[CoqChange]` [CoqChange](../changes/CoqChange.md)
> > List of changes to apply to the file.
>
> Raises:
> > `NotImplementedError`: If the type of change passed into the function is not of type `CoqAdd` or `CoqDelete`.
> > `InvalidChangeException` [InvalidChangeException](../exceptions/InvalidChangeException.md): If the provided change contains more than one step or the change causes the file to become invalid.