# Format JSON deterministically: implementation

## What the example does

Sorted keys and indentation make small JSON documents easier to review. This is readable formatting, not a standardized cryptographic canonicalization scheme.

The public function is `solve(value)`. The JSON input contract can be seen in this concrete example:

```json
{
  "z": 1,
  "a": [
    2,
    3
  ]
}
```

Expected result:

```json
"{\n  \"a\": [\n    2,\n    3\n  ],\n  \"z\": 1\n}"
```

Run `python3 example.py` for the Python representation of the result. `solution.py` contains the full implementation and can also be imported by another script.

## Scope

The function implements exactly the behavior described above. It does not perform network or filesystem access. Python exceptions indicate unsupported input; the next lesson turns them into a command-line error response. Review the limitations before reusing it in an application.
