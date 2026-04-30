# `ProofFile(CoqFile)` [CoqFile](../base_file/CoqFile.md)

Allows to get information about the proofs of a Rocq file. ProofState will run the file from its current state, i.e., if the file has finished its execution, ProofState won't return anything. The Rocq file will be fully checked after the creation of a ProofState.

## Attributes

`__aux_file : _AuxFile` [_AuxFile](_AuxFile.md)
> An auxiliary file used to locate notations and libraries to be used in evaluating the current file.

`__error_mode : str`
> How errors are handled. Can be "strict" or "warning". If "strict", an exception will be raised when an unexpected behavior occurs. If "warning", a warning will be logged instead (it only applies to recoverable errors).

`__use_disk_cache : bool`
> If True, the terms from each loaded library are stored in a cache on disk. Then, when creating or manipulating future proof files, terms are loaded from the cache if their corresponding library (file) has the same text.  Note that caching only depends on the text of the file, so if the Rocq version changes, or the version of coqpyt changes, the cache should be deleted.

`__coq_lsp_options : Tuple[str]`
> Options to be passed to the coq-lsp on startup. 

`__program_context : Dict[str, Tuple[Term, List[Term]]]` [Term](../structs/Term.md)
> Collection of all terms in the current file. The dictionary is keyed by the scope the term was defined in. The first element in the tuple is the last term defined in the scope and the second element is the list of terms visible to the first element, defined both in the current file and in libraries.

`__proofs : List[ProofTerm]` [ProofTerm](../structs/ProofTerm.md)
> Collection of all finished proofs in the file.

`__open_proofs : List[ProofTerm]` [ProofTerm](../structs/ProofTerm.md)
> Collection of all proofs that haven't finished being proven.

`__current_goals : Optional[GoalAnswer]` [GoalAnswer](../lsp/structs/GoalAnswer.md)
> The cached goals that are to be proven at the current execution point in the file.

`__last_end_pos : Optional[Position]` [Position](../../lsp/structs/Position.md)
> The position where `__current_goals` was last updated to prevent excessive calls to the coq-lsp for getting the goals of the current proof.


## Properties

`proofs : List[ProofTerm]` [ProofTerm](../structs/ProofTerm.md)
> Gets all the closed proofs in the file and their corresponding steps. Each element has the list of steps for a single closed proof of the Rocq file. The proofs are ordered by the order they are closed on the file. The steps include the context used for each step and the goals in that step.

`open_proofs : List[ProofTerm]` [ProofTerm](../structs/ProofTerm.md)
> Gets all the open proofs in the file and their corresponding steps. Each element has the list of steps for a single open proof of the Rocq file. The proofs are ordered by the order they are opened on the file. The steps include the context used for each step and the goals in that step.

`unproven_proofs : List[ProofTerm]` [ProofTerm](../structs/ProofTerm.md)
> Gets all the the open proofs and admitted proofs.

`current_goals : Optional[GoalAnswer]` [GoalAnswer](../lsp/structs/GoalAnswer.md)
> Get goals in current position.

`in_proof : bool`
> True if the current step is inside a proof.

`can_close_proof : bool`
> True if the next step can be a \[Qed\].


## Operations

```python
__init__(self, file_path: str, library: Optional[str] = None, timeout: int = 30, memory_limit: int = 2097152, workspace: Optional[str] = None, coq_lsp: str = "coq-lsp", coq_lsp_options: Tuple[str] = None, coqtop: str = "coqtop", error_mode: str = "strict", use_disk_cache: bool = False)
```
> Creates a ProofFile.
>
> `file_path : str`
> > Path of the Rocq file.
>
> `library : Optional[str] = None`
> > *Optional.* The library of the file. Defaults to None.
>
> `timeout : int = 30`
> > *Optional.* Timeout used in coq-lsp. Defaults to 2?
>
> `memory_limit : int = 2097152`
> > *Optional.* RAM limit for the coq-lsp process in kilobytes. It only works for Linux systems. Defaults to 2097152.
>
> `workspace : Optional[str] = None`
> > *Optional.* Absolute path for the workspace. If the workspace is not defined, the workspace is equal to the path of the file.
>
> `coq_lsp : str = "coq-lsp"`
> > *Optional.* Path to the coq-lsp binary. Defaults to "coq-lsp".
>
> `coq_lsp_options : Tuple[str] = None`
> > *Optional.* Options to be passed to the coq-lsp on startup. Defaults to None.
>
> `coqtop : str = "coqtop"`
> > *Optional.* Path to the coqtop binary used to compile the Rocq libraries imported by coq-lsp. This is NOT passed as a parameter to coq-lsp, it is simply used to check the Rocq version in use. Defaults to "coqtop".
> 
> `error_mode : str = "strict"`
> > *Optional.* How errors are handled. Can be "strict" or "warning". If "strict", an exception will be raised when an unexpected behavior occurs. If "warning", a warning will be logged instead (it only applies to recoverable errors). Defaults to "strict".
> 
> `use_disk_cache : bool = False`
> > *Optional.* If True, the terms from each loaded library are stored in a cache on disk. Then, when creating or manipulating future proof files, terms are loaded from the cache if their corresponding library (file) has the same text.  Note that caching only depends on the text of the file, so if the Rocq version changes, or the version of coqpyt changes, the cache should be deleted.

```python
_handle_exception(self, e) -> None
```
> Shuts down the lsp client if `e` is a server error, deletes the temporary file if `__from_lib` is true, and closes the auxiliary file.
> 
> `e : any`
> > Error to handle.

```python
exec(self, nsteps = 1) -> List[Step]
```
> Executes steps in the file.
>
> `nsteps : int = 1`
> > *Optional.* Number of steps to execute. Defaults to 1.
>
> Returns: `List[Step]` [Step](../structs/Step.md) List of steps executed. 

```python
append_step(self, proof: ProofTerm, step_text: str) -> None
```
> Appends a step to a proof. This function will change the original file. If an exception is thrown the file will not be changed.
> 
> `proof : ProofTerm` [ProofTerm](../structs/ProofTerm.md)
> > The proof of the file to which the step is added.
> 
> `step_text : str`
> > The text of the step to add.
> 
> Raises:
> > `InvalidFileException` [InvalidFileException](../exceptions/InvalidFileException.md): If the file being changed is not valid.
> > `InvalidAddException` [InvalidAddException](../exceptions/InvalidAddException.md): If the file is invalid after adding the step.

```python
pop_step(self, proof: ProofTerm) -> None
```
> Removes the last step from a proof. This function will change the original file. If an exception is thrown the file will not be changed.
> 
> `proof : ProofTerm` [ProofTerm](../structs/ProofTerm.md)
> > The proof of the file from which the step is removed.
> 
> Raises:
> > `InvalidFileException` [InvalidFileException](../exceptions/InvalidFileException.md): If the file being changed is not valid.
> > `InvalidDeleteException` [InvalidDeleteException](../exceptions/InvalidDeleteException.md): If the file is invalid after removing the step.

```python
change_proof(self, proof: ProofTerm, proof_changes: List[ProofChange]) -> None
```
> Changes the steps of a proof transactionally. If an exception is thrown the file will not be changed.
> 
> `proof : ProofTerm` [ProofTerm](../structs/ProofTerm.md)
> > The proof of the file from which the changes apply.
> 
> `changes : List[ProofChange]` [ProofChange](../changes/ProofChange.md)
> > The changes to be applied to the proof. 
>
> Raises:
> > `InvalidFileException` [InvalidFileException](../exceptions/InvalidFileException.md): If the file being changed is not valid.
> > `InvalidChangeException` [InvalidChangeException](../exceptions/InvalidChangeException.md): If the file is invalid after applying the changes.
> > `NotImplementedError`: If the changes contain an unknown ProofChange.

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

```python
delete_step(self, step_index: int) -> None
```
> Deletes a step from the file. This function will change the original file. If an exception is thrown the file will not be changed.
>
> `step_index : int`
> > The index of the step to remove.

```python
change_steps(self, changes: List[CoqChange]) -> None
```
> Changes the steps of the original Rocq file transactionally. If an exception is thrown the file will not be changed.
>
> `changes : List[CoqChange]` [CoqChange](../changes/CoqChange.md)
> > The changes to be applied to the Rocq file.

```python
close(self) -> None
```
> Closes all resources used by this object.

```python
__locate(self, search, line: int) -> List[str]
```
> Uses the auxiliary file to search for the definition of a notation and returns the strings representing the terms that the notation be defined from.
> 
> `search : any`
> > Notation to search for.
> 
> `line : int`
> > The line of the auxiliary file that the locate was run from.
> 
> Returns: `List[str]` List of all terms corresponding to the notation.

```python
__step_context(self, step: Step) -> List[Term]
```
> Gets all terms that are used in the definition and execution of the provided step. 
> 
> `step : Step`
> > The step to consider
> 
> Returns: `List[Term]` [Term](../structs/Term.md) The list of terms used.
>
> Raises:
> > `NotationNotFoundException` [NotationNotFoundException](../exceptions/NotationNotFoundException.md): If the notation used in the step was not found and the error mode for the current file is set to `"strict"`.

```python
__get_program_context(self) -> Tuple[Term, List[Term]]
```
> Gets all terms defined that are accessible to the last step executed in the current file.
> 
> Returns: `Tuple[Term, List[Term]]` [Term](../structs/Term.md) Tuple of the last term defined for this scope and the list of all terms defined.
>
> Raises:
> > `RuntimeError`: If the obligation used to locate the current location in the file does not exist.

```python
__handle_obligations(self, step: Step, undo: bool = False) -> None
```
> If undo is false, it updates the current program context to contain any newly defined terms for all visible scopes. If undo is true, it removes the last defined scope of terms. 
> 
> `step : Step` [Step](../structs/Step.md)
> > Step that was executed or undone.
> 
> `undo : bool = False`
> > *Optional.* Whether the execution of the file was executing or undoing a step. Defaults to False.

```python
__has_obligations(self, step: Step) -> bool
```
> Checks whether the provided step requires that the current scope of the file should be updated.
> 
> `step : Step` [Step](../structs/Step.md)
> > Step to consider.
> 
> Returns: `bool` True of the scope of the file program context should be updated.

```python
__handle_end_proof(self, step: Step, index: Optional[int] = None, open_index: Optional[int] = None, undo: bool = False) -> None
```
> Closes or opens a proof depending on if the execution of the file was going forwards or backwards. If undo is False, the 
> 
> `step : Step`
> > The step where this proof is to be closed.
> 
> `index : Optional[int] = None`
> > *Optional.* The index where the proof should be located in `__proofs`. If this value is None, it will use the last index of the last closed proof. Defaults to None.
> 
> `open_index : Optional[int] = None`
> > *Optional.* The index where the proof should be located in `__open_proofs`. If this value is None, it will use the last index of the last opened proof. Defaults to None.
> 
> `undo : bool = False`
> > *Optional.* Whether the execution of the file was executing or undoing a step. Defaults to False.

```python
__handle_proof_step(self, step: Step, undo: bool = False) -> None
```
> Adds the given step into the list of steps for the last open proof. If undo is True, the step will be removed from the proof.
> 
> `step : Step` [Step](../structs/Step.md)
> > The step to add to the proof.
> 
> `undo : bool = False`
> > *Optional.* Whether the execution of the file was executing or undoing a step. Defaults to False.

```python
__handle_proof_term(self, step: Step, index: Optional[int] = None, undo: bool = False) -> None
```
> Creates a new proof term for the current step and adds it to the `__open_proofs` list. If undo is True, the proof is deleted instead.
> 
> `step : Step` [Step](../structs/Step.md)
> > The step where the proof's definition begins.
> 
> `index : Optional[int] = None`
> > *Optional.* The index where the proof should be located in `__open_proofs`. If this value is None, it will use the last index of the last opened proof. Defaults to None.
> 
> `undo : bool = False`
> > *Optional.* Whether the execution of the file was executing or undoing a step. Defaults to False.

```python
__check_proof_step(self, step: Step, undo: bool = False) -> None
```
> Checks what kind of term the current step is and handles it accordingly. If the step is a basic step in the file, the `__handle_proof_step` method is called. If the step defines a new term, this method calls `__handle_proof_term`.
> 
> `step : Step` [Step](../structs/Step.md)
> > Step to handle.
> 
> `undo : bool = False`
> > *Optional.* Whether the execution of the file was executing or undoing a step. Defaults to False.

```python
__step(self, step: Step, undo: bool) -> None
```
> Executes the current step. It also updates the auxiliary file to contain this step for context searching purposes.
> 
> `step : Step` [Step](../structs/Step.md)
> > Step to execute.
> 
> `undo : bool`
> > Whether the execution of the file was executing or undoing a step.

```python
__find_step(self, range: Range) -> Optional[Tuple[ProofTerm, int, int]]
```
> Searches for location in a proof of the step located at `range`.
> 
> `range : Range` [Range](../../lsp/structs/Range.md)
> > Range of the step to search for.
> 
> Returns: `Optional[Tuple[ProofTerm, int, int]]` [ProofTerm](../structs/ProofTerm.md) The proof term and location of the step if found. The first element is the proof the step is used in, the second element is the index of that proof in the file, and the third element is the index within that proof that the step is used.

```python
__find_step_index(self, range: Range) -> int
```
> Gets the index of the step located at `range` in relation to the entire file.
> 
> `range : Range` [Range](../../lsp/structs/Range.md)
> > Range of the step to search for.
> 
> Returns: `int` Index of the step.
>
> Raises:
> > `RuntimeError`: If no step exists in the provided range.

```python
__get_step(self, step_index: int) -> ProofStep
```
> Gets the proof step for the step located at `step_index` by recomputing the context of the file up to that point.
> 
> `step_index : int`
> > Index of the step to get.
> 
> Returns: `ProofStep` [ProofStep](../structs/ProofStep.md) Proof step referencing the current goals and context in the file.

```python
__update_libraries(self) -> None
```
> Updates the current context to contain all the terms of the currently imported libraries. If a library is added, the file will be loaded using `_AuxFile.get_library` and cached is specified.

```python
__find_open_proof_index(self, step: Step) -> int
```
> Locates the index of the open proof that the provided step comes directly after.
> 
> `step : Step` [Step](../structs/Step.md)
> > Step to consider.
> 
> Returns: `int` Index of the located open proof.

```python
__find_proof_index(self, step: Step) -> int
```
> Locates the index of the completed proof that the provided step comes directly after.
> 
> `step : Step` [Step](../structs/Step.md)
> > Step to consider.
> 
> Returns: `int` Index of the located completed proof.

```python
__local_exec(self, n_steps: int = 1) -> None
```
> Executes the indicated number of steps without modifying the proof information.
> 
> `n_steps : int = 1`
> > *Optional.* Number of steps to execute. Defaults to 1.

```python
__add_step(self, index: int) -> None
```
> Updates the proof context by running the step located at the provided index.
> 
> `index : int`
> > Index of the step to update with.

```python
__delete_step(self, step: Step) -> None
```
> Updates the proof context by undoing the given step.
> 
> `step : Step` [Step](../structs/Step.md)
> > The step to undo.

```python
__get_changes_data(self, changes: List[CoqChange]) -> Tuple[List[int], List[int], int]
```
> Calculates the indices of the modified steps and new current index of execution in the file from the changes listed in `changes`.
> 
> `changes : List[CoqChange]` [CoqChange](../changes/CoqChange.md)
> > The changes (additions and deletions) to apply to the current file.
> 
> Returns: `Tuple[List[int], List[int], int]` Tuple where the first element is the list of indices of added steps, the second element is the list of indices of deleted steps, and the third element is the new current step index of execution.

```python
__goals(self, end_pos: Position) -> Optional[GoalAnswer]
```
> Requests the goals of the proof at `end_pos` from the coq-lsp. Generally, this is used to find what still needs to be proven at a current point in the file.
> 
> `end_pos : Position`
> > The position of the proof.
> 
> Returns: `Optional[GoalAnswer]` [GoalAnswer](../lsp/structs/GoalAnswer.md) The information on the goals of the proof and the current step in the proof based on the provided position.

```python
__in_proof(self, goals: Optional[GoalAnswer]) -> bool
```
> Checks if the given goal answer for a proof still has goals that need to be satisfied.
> 
> `goals : Optional[GoalAnswer]` [GoalAnswer](../lsp/structs/GoalAnswer.md)
> > Object representing the goals for a proof.
> 
> Returns: `bool` Whether the goals still need to be satisfied.

```python
__can_close_proof(self, goals: Optional[GoalAnswer]) -> bool
```
> Checks if the given goal answer for a proof has all requirements satisfied so it can be properly closed.
> 
> `goals : Optional[GoalAnswer]` [GoalAnswer](../lsp/structs/GoalAnswer.md)
> > Object representing the goals for a proof.
> 
> Returns: `bool` Whether the proof can be closed.

```python
__is_proven(self, proof: ProofTerm) -> bool
```
> Checks if the given proof term has been successfully proven by a close proof step and has not been explicitly admitted.
> 
> `proof : ProofTerm`
> > The proof to consider.
> 
> Returns: `bool` Whether the proof is properly proven.


## Static Operations

```python
set_library_cache_size(size: Optional[int]) -> None
```
> Sets the size of the cache used to store the libraries of the Rocq files.
> 
> `size : Optional[int]`
> > The size of the cache. If None, the cache will have no limit.

```python
clear_disk_cache() -> None
```
> Clears the library cache.