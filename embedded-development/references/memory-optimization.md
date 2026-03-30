# Memory Optimization

Load this reference when flash, RAM, or stack is tight.

## Main Levers

- Compile for size where appropriate
- Put read-only tables and strings in flash
- Prefer fixed-size allocation over fragmentation-prone heap use
- Reuse buffers when lifetime does not overlap
- Use narrower integer types where valid
- Measure task stack headroom instead of guessing

## Good Default Practices

- `const` for lookup tables and static messages
- `static` for file-local helpers and large persistent buffers
- Memory pools instead of unbounded heap allocation
- Linker garbage collection with section-splitting flags

## Risks To Check

- Large local arrays on task stacks
- Silent queue or buffer over-allocation
- Recursion in constrained firmware
- Flash wear from naive parameter storage
