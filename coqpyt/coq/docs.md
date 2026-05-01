# `coq` Package

This package contains all classes that are directly related to CoqPyt.


## Packages

- [`lsp`](./lsp/docs.md)


## Files and Classes

- `base_file.py`
    - [`CoqFile`](./base_file/CoqFile.md)
- `changes.py`
    - [`CoqAdd`](./changes/CoqAdd.md)
    - [`CoqChange`](./changes/CoqChange.md)
    - [`CoqDelete`](./changes/CoqDelete.md)
    - [`ProofAppend`](./changes/ProofAppend.md)
    - [`ProofChange`](./changes/ProofChange.md)
    - [`ProofPop`](./changes/ProofPop.md)
- `context.py`
    - [`FileContext`](./context/FileContext.md)
- `exceptions.py`
    - [`InvalidAddException`](./exceptions/InvalidAddException.md)
    - [`InvalidChangeException`](./exceptions/InvalidChangeException.md)
    - [`InvalidDeleteException`](./exceptions/InvalidDeleteException.md)
    - [`InvalidFileException`](./exceptions/InvalidFileException.md)
    - [`NotationNotFoundException`](./exceptions/NotationNotFoundException.md)
- `proof_file.py`
    - [`_AuxFile`](./proof_file/_AuxFile.md)
    - [`ProofFile`](./proof_file/ProofFile.md)
- `structs.py`
    - [`ProofStep`](./structs/ProofStep.md)
    - [`ProofTerm`](./structs/ProofTerm.md)
    - [`SegmentStack`](./structs/SegmentStack.md)
    - [`SegmentType`](./structs/SegmentType.md)
    - [`Step`](./structs/Step.md)
    - [`Term`](./structs/Term.md)
    - [`TermType`](./structs/TermType.md)