# Ordered batch processing for Format JSON deterministically

`batch.py` accepts an outer JSON array containing separate inputs. This is an extra level of nesting when `solve` itself accepts a list. It produces one result envelope per item, preserving input order and zero-based position.

```sh
python3 batch.py < samples/batch.json
```

The batch covers these three input/output pairs:

## Case 1

Input:
```json
{
  "z": 1,
  "a": [
    2,
    3
  ]
}
```

Result:
```json
"{\n  \"a\": [\n    2,\n    3\n  ],\n  \"z\": 1\n}"
```

## Case 2

Input:
```json
{
  "text": "你好"
}
```

Result:
```json
"{\n  \"text\": \"你好\"\n}"
```

## Case 3

Input:
```json
null
```

Result:
```json
"null"
```

## Partial failures

Each successful item has `ok: true` and `result`. A failed item has `ok: false` and an exception type; later items still run. Exit status 1 means at least one item failed, while status 2 means the batch envelope itself was invalid. An empty outer array is a valid empty batch.

Sorted keys and indentation make small JSON documents easier to review. This is readable formatting, not a standardized cryptographic canonicalization scheme.

The implementation processes sequentially, avoiding shared-state concurrency and keeping output order predictable. Input is limited to one MiB and 1000 items; this version materializes all results in memory. The next lesson removes that whole-batch memory requirement with line-oriented processing.
