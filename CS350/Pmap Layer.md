# Pmap Layer

> [!tldr] Holds architecture-specific VM code

VM layer invokes pmap layer
* On page fault, install mappings
* To protect or unmap pages
* To ask for dirty/access bits
Pmap layer is lazy
* Can discard mappings
* Process will fault and VM must reinstall mapping
