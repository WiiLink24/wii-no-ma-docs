# Common Error Codes

The following is a non-exhaustive list of XML error codes. Contributions are more than welcome. XML errors will always be within the range of 3541xx.

## Error codes

<table>
  <thead>
    <tr>
      <th style="text-align:left">Error</th>
      <th style="text-align:left">Meaning</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">354116</td>
      <td style="text-align:left">A node is missing.</td>
    </tr>
    <tr>
      <td style="text-align:left">354117</td>
      <td style="text-align:left">
        <p>A node contained a dictionary, but lacked sufficient children.</p>
        <p>Typically this error is thrown when either too many or too little children
          nodes were provided.</p>
        <p>This error can be set by two individual functions. Please see <a href="common-error-codes.md#how-to-debug">How to debug</a> for
          more information.</p>
      </td>
    </tr>
  </tbody>
</table>

## How to debug

Node errors are typically set via helper functions instead of directly to their object. Between Wii no Ma version v1025 and v770, there are five functions that set the XML error code directly: `XMLError`, `XMLErrorOther`, `SetNodeMissing`, `SetNodeMissingDict`, and `SetNodeMissingDictContents`.

We hope the following table assists labeling efforts throughout reverse engineering.

| Version | Symbol | Address |
| :--- | :--- | :--- |
| v770 | XMLError | 8025e454 |
|  | XMLErrorOther | 8025e44c |
|  | SetNodeMissing | 8025e474 |
|  | SetNodeMissingDict | 8025e48c |
|  | SetNodeMissingDictContents | 8025e498 |
|  |  |  |
| v1025 | XMLError | 802b0d64 |
|  | XMLErrorOther | 802b0d5c |
|  | SetNodeMissing | 802b0db0 |
|  | SetNodeMissingDict | 802b0dc8 |
|  | SetNodeMissingDictContents | 802b0e20 |

### Meanings

`XMLError` is used to set a specific error by an integer. It is worth breakpointing on it in general. `XMLErrorOther` is sparingly used throughout XML verification methods. If a specific XML error occurs and XMLError was not called, it is worth breakpointing on this as well before investigating otherwise.

While `SetNodeMissingDict` produces the same error code as `SetNodeMissingDictContents` \(354117\), it is used differently:

* `SetNodeMissingDict` is called when a node that should contain a dictionary is missing and therefore had a child count of 0.
* `SetNodeMissingDictContents` is called whenever its contents are not within range of what is expected. It is typically called directly after instructions resembling the following:

```text
lwz        r0, 0x0(r3)
cmplw      r6, r0
blt        MISSING_DICT
lwz        r0, 0x4(r3)
cmplw      r6,r0
ble        MISSING_DICT

MISSING_DICT:
; in which r3 is the current XML object
or         r3,r29,r29
; and in which r4 is a pointer to this node's name, such as "categinfo"
or         r4,r24,r24
bl         SetNodeMissingDictContents
```

If you are looking for these functions yourself, a good way to orient yourself while reverse engineering is to find any instance of a reference to the string `ver` for `SetNodeMissing`, which can look like similar to this when decompiled:

```c
int len = strlen("ver");
char* nodeContents = FindNodeContents(buffer, "ver", len);
verNode = GetNode(nodes, "ver");
if (nodeContents == NULL) {
  SetNodeMissing(xmlObject, "ver");
  success = 0;
}
```

