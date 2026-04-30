# `FileContext`

Represents the context of a Rocq file in terms of the loaded terms and libraries up to a specific point in the file.

## Attributes

`libraries : Dict[str, Dict[str, Term]]` [Term](../structs/Term.md)
> A collection containing all terms defined in imported libraries. The outer dictionary is keyed by the library name, while the inner is keyed by the name of the term.

`__path : str`
> Path of the file.

`__module : List[str]`
> Module where the file is included.

`__terms : Dict[str, List[Term]]` [Term](../structs/Term.md)
> Dictionary containing all terms defined under a given name in the file.

`__last_terms : List[List[Tuple[str, Term]]]` [Term](../structs/Term.md)
> Stack of terms added after executing each step.

`__segments : SegmentStack` [SegmentStack](../structs/SegmentStack.md)
> Stack of the current position in the module tree.

`__anonymous_id : Optional[int]`
> Incrementing id used to provide names for anonymous terms.

`__expr : Callable`
> Version based function to get the `expr` field of an AST.

`__where_notation_key : str`
> Version based string containing the dictionary key of notations returned by coqtop.

`__ext_plugin : Callable`
> Version based function to get the external plugin field of a Rocq expression.

`__ext_entry : Callable`
> Version based function to get the external entry field of a Rocq expression.

`ext_index : Callable`
> Version based function to get the external index field of a Rocq expression. This function will be made private once `__get_program_context` is extracted from ProofFile to here.

`__fixpoint_notations : Callable`
> Version based function to get the notations of a term in the AST.

`obligation_tag_with_id : Callable`
> Version based function to check if an obligation tag references an id. This function will be made private once `__get_program_context` is extracted from ProofFile to here.


## Properties

`local_terms : List[Term]` [Term](../structs/Term.md)
> The executed terms defined in the current file.

`terms : Dict[str, Term]` [Term](../structs/Term.md)
> All terms defined in the current file.

`in_module_type : bool`
> True if currently inside a module type.

`last_term : Optional[Term]` [Term](../structs/Term.md)
> The last term defined in the current file.

`curr_modules : List[str]`
> The current module path.


## Operations

```python
__init__(self, path: str, module: Optional[List[str]] = None, coqtop: str = "coqtop", terms: Optional[Dict[str, Term]] = None)
```
> Creates a new FileContext object.
> 
> `path : str`
> > Path of the file.
> 
> `module : Optional[List[str]] = None`
> > *Optional.* Module where the file is included. Defaults to None.
> 
> `coqtop : str = "coqtop"`
> > *Optional.* Path to the coqtop binary used to compile the Rocq libraries imported by coq-lsp. Defaults to "coqtop".
> 
> `terms : Optional[Dict[str, Term]] = None` [Term](../structs/Term.md)
> > *Optional.* Collection of terms to initialize the context with. Defaults to None.

```python
process_step(self, step: Step) -> None
```
> Extracts the identifiers from a step and updates the context with new terms defined by the step.
> 
> `step : Step` [Step](../structs/Step.md)
> > The step to be processed.

```python
undo_step(self, step: Step) -> None
```
> Removes the terms defined by a step from the context.
> 
> `step : Step` [Step](../structs/Step.md)
> > The step to be reverted.

```python
expr(self, step: Step) -> List
```
> `step : Step` [Step](../structs/Step.md)
> > The step to be processed.
> 
> Returns: `List` 'expr' field from the AST of a step.

```python
attrs(self, step: Step) -> List
```
> `step : Step` [Step](../structs/Step.md)
> > The step to be processed.
> 
> Returns: `List` 'attrs' field from the AST of a step.

```python
term_type(self, step: Step) -> TermType
```
>`step : Step` [Step](../structs/Step.md)
> > The step to be processed.
> 
> Returns: `TermType` The term type of the step.

```python
is_proof_term(self, step: Step) -> bool
```
> `step : Step` [Step](../structs/Step.md)
> > The step to be processed.
> 
> Returns: `bool` Whether the step introduces a new proof term.

```python
is_end_proof(self, step: Step) -> bool
```
> `step : Step` [Step](../structs/Step.md)
> > The step to be processed.
> 
> Returns: `bool` Whether the step closes an open proof term.

```python
is_segment_delimiter(self, step: Step) -> bool
```
> `step : Step` [Step](../structs/Step.md)
> > The step to be processed.
> 
> Returns: `bool` Whether the step delimits a segment (module or section).

```python
update(self, context: Union[FileContext, Dict[str, Term]] = {}) -> None
```
> Updates the context with new terms.
> 
> `terms : Union[FileContext, Dict[str, Term]] = {}`
> > The new terms to be added.

```python
add_library(self, name: str, terms: Dict[str, Term]) -> None
```
> Adds a library to the context.
> 
> `name : str`
> > The name of the library.
> 
> `terms : Dict[str, Term]` [Term](../structs/Term.md)
> > The terms defined by the library.

```python
remove_library(self, name: str) -> None
```
> Removes a library from the context.
> 
> `name : str`
> > The name of the library.
> 
> Raises:
> > `RuntimeError`: If the library was not found in the current context.

```python
append_module_prefix(self, name: str) -> str:
```
> Attaches the current module path to the start of a name.
> 
> `name : str`
> > The name.
> 
> Returns: `str` The full name with the module path.

```python
get_term(self, name: str) -> Optional[Term]
```
> Get a notation from the context.
> 
> `name : str`
> > The term name.
> 
> Returns: `Optional[Term]` [Term](../structs/Term.md) The term mapped to the name, if it exists.

```python
get_notation(self, notation: str, scope: str) -> Term
```
> Get  a notation from the context.
> 
> `notation : str`
> > Id of the notation. E.g. "_ + \_".
> 
> `scope : str`
> > Scope of the notation. E.g. "nat_scope".
> 
> Returns: `Term` [Term](../structs/Term.md) Term that corresponds to the notation.
>
> Raises:
> > `NotationNotFoundException` [NotationNotFoundException](../exceptions/NotationNotFoundException.md): If the notation is not found in the context.

```python
reset(self)
```
> Resets the context to its initial state.

```python
__init_coq_version(self, coqtop: str) -> None
```
> Checks the version of coqtop and updates helper functions to assist the parsing of coqtop's output according to its version.
> 
> `coqtop : str`
> > Path to the coqtop binary used to compile the Rocq libraries imported by coq-lsp.

```python
__init_context(self, terms: Optional[Dict[str, Term]] = None) -> None
```
> Initializes the collection of terms in the file context.
> 
> `terms : Optional[Dict[str, Term]]` [Term](../structs/Term.md)
> > *Optional.* Dictionary of terms to initialize the context with. Defaults to None.

```python
__add_terms(self, step: Step, expr: List) -> None
```
> Parses an expression in the AST and adds all terms defined in the expression to the context.
> 
> `step : Step` [Step](../structs/Step.md)
> > Step corresponding to the part of the AST that is being processed.
> 
> `expr : List`
> > Expression corresponding to this step as found in the AST.

```python
__add_term(self, name: str, step: Step, term_type: TermType) -> None
```
> Creates a term and adds it to the collection of terms in the context.
> 
> `name : str`
> > Name of the term.
> 
> `step : Step` [Step](../structs/Step.md)
> > Step in which the term is defined.
> 
> `term_type : TermType` [TermType](../structs/TermType.md)
> > Type of the term added.

```python
__remove_term(self, name: str, term: Term) -> None
```
> Removes a term from the context.
> 
> `name : str`
> > Name of the term to remove.
> 
> `term : Term` [Term](../structs/Term.md)
> > Term to remove.

```python
__handle_where_notations(self, step: Step, expr: List, term_type: TermType) -> None
```
> Creates a new term to represent when a term has extra notations defined.
> 
> `step : Step` [Step](../structs/Step.md)
> > Step in which the term is defined.
> 
> `expr : List`
> > Part of AST where the term is defined.
> 
> `term_type : TermType` [TermType](../structs/TermType.md)
> > Type of the term.

```python
__is_extend(self, expr: List, entry: str | Tuple[str], exact: bool = True) -> bool
```
> Checks if the given expression in the AST extends the provided `entry` field.
> 
> `expr : List`
> > Expression in the AST to consider.
> 
> `entry : str | Tuple[str]`
> > Accepted extension name.
> 
> `exact : bool = True`
> > *Optional.* Whether the name of the extension matches perfectly. Defaults to True.
> 
> Returns: `bool` True of the expression extends `entry`.

```python
__term_type(self, expr: List) -> TermType
```
> Gets the entry of the `TermType` enum that corresponds to the type of the expression.
> 
> `expr : List`
> > Expression in the AST to consider.
> 
> Returns: `TermType` [TermType](../structs/TermType.md) Type of the expression.


## Static Operations

```python
is_id(el) -> bool
```
> Checks if an element of an AST is an identifier (qualid).
> 
> `el`
> > Element of the expression to consider.
> 
> Returns: `bool` True if `el` is an identifier.

```python
is_notation(el) -> bool
```
> Checks if an element of an AST is a notation.
> 
> `el`
> > Element of the expression to consider.
> 
> Returns: `bool` True if `el` is an notation.

```python
get_id(id: List) -> Optional[str]
```
> Gets the identifier (qualid) of an element of the AST. This function will be made private once `__step_context__` is extracted from ProofFile to here.
> 
> `id : List`
> > Element of the expression to consider.
> 
> Returns: `Optional[str]` The identifier of an element if it exists.

```python
get_ident(id: List) -> Optional[str]
```
> Gets the identifier of a generic argument of an element in the AST. Specifically, the generic argument is the inhabitant of some type at the levels raw, global, or typed, along with the representation of the type. This function will be made private once `__get_program_context` is extracted from ProofFile to here.
> 
> `el : List`
> > Element of the expression to consider.
> 
> Returns: `Optional[str]` The identifier of the generic argument if it exists.

```python
get_notation_scope(notation: str) -> str
```
> Get the scope of a notation.
> 
> `notation : str`
> > Possibly scoped notation pattern. E.g. "_ + _ : nat_scope".
> 
> Return: `str` The scope of the notation. E.g. "nat_scope".

```python
__get_names(expr: List) -> List[str]
```
> Gets the names of all terms defined in an expression.
> 
> `expr : List`
> > Expression in the AST to consider.
> 
> Returns: `List[str]` All names defined.

```python
__get_v(el: List) -> Optional[str]
```
> Gets the `v` attribute of an element in the AST. 
> 
> `el : List`
> > Element of the AST.
> 
> Returns: `Optional[str]` Data stored behind the `v` attribute.

```python
__get_notation_key(notation: str, scope: str) -> str
```
> Gets the key of a notation in a provided scope.
> 
> `notation : str`
> > String representation of the notation.
> 
> `scope : str`
> > String representation of the scope the notation is located in.
> 
> Returns: `str` The notation key.