# Generic Terminology

## Files

Files within Wii no Ma are rather coherently structured. Within the main app's U8 archive \(content ID `00000026` for v1025\), an `xml` subdirectory exists. This contains basic information about every request, and in some cases, additional information. This file format is not very well understood, and thankfully easily worked around with Dolphin's debugging. Presumably this is a way to hint types, verifiable data, and node hierarchy.

## URL Structure

As noted in the documentation for [config.bin](config-first.bin.md#example-contents), there are several configurable URL types: `url1`, `url2`, and `url3`.

`url1` typically refers to normal, non-theater data. This includes things such as room/parade data, movies and their metadata, Concierge Miis, and poster imagery. Nintendo hosted this on Akamai originally, presumably publishing new files occasionally to refresh content.

`url2` houses requestable, dynamic data. It's unknown who was used to host this. All routes via this end with `.cgi`. Examples include searching movies, recording movie voting data, requesting support, and getting the current time of day.

`url3` is similar to `url1` but entirely for the theater. For the most part, the general file hierarchy is replicated.

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

