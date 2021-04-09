# Generic Terminology

## Files

Files within Wii no Ma are rather coherently structured. Within the main app's U8 archive \(content ID `00000026` for v1025\), an `xml` subdirectory exists. This contains basic information about every request, and in some cases, additional information. This file format is not very well understood, and thankfully easily worked around with Dolphin's debugging. Presumably this is a way to hint types, verifiable data, and node hierarchy.

## XML Structure

Every request follows this basic form:

```markup
<XMLType>
    <ver>123</ver>
</XMLType>
```

It should be noted `ver` is version-dependent.

| Title Version | XML Version |
| :--- | :--- |
| v0/v512 | 1 |
| v770 | 1 |
| v1025 | 399 |

In the case of v1025, the version is divided by 100 and equated to 3. We choose 399 simply because it's possible. - anything in the range of 300-399 would work the same.

## XML Types

| Type | Description |
| :--- | :--- |
| Boolean | A boolean value is either the string literal `1` or `0`. `true` and `false` will fail to parse. |
| Date | This type expects a date in `YYYY-MM-DD` format, such as `2021-01-13`. |
| DateTime | Similar to the above, except in `YYYY-MM-DDTHH:MM:SS`. The `T` is literal: an example might be `2021-01-13T08:06:31`. |

