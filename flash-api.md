# Flash API

TODO: Write documentation. There are also getter/setters on the objects, and classes outside of the `wiinoma` namespace, such as `wii`.

## `wiinoma.Vibrate`

| name | description |
| :--- | :--- |
| RequestFocusVibrate |  |

## `wiinoma.Alert`

| name | description |
| :--- | :--- |
| sets |  |
| get |  |

## `wiinoma.Message`

| name | description |
| :--- | :--- |
| GetMessage | Appears to return false if there is no message. |
| GetShopId |  |

## `wiinoma.Sound`

| name | description |
| :--- | :--- |
| Play |  |
| Stop |  |
| PlayBGM |  |
| StopBGM |  |
| PauseBGM |  |

## `wiinoma.Info`

| name | description |
| :--- | :--- |
| GetRevision | Returns the channel's revision as a string. |

## `wiinoma.System`

| name | description |
| :--- | :--- |
| Exit |  |
| ExitToLiving |  |
| FinishedStartup | Ends the infinite loading screen. |
| DisableApplicationExit |  |
| EnableMouse |  |
| DisableMouse |  |

## `wiinoma.Swing`

| name | description |
| :--- | :--- |
| Action |  |
| onWiinomaSwing |  |

## `wiinoma.Cache`

| name | description |
| :--- | :--- |
| RegisterUrl |  |
| IsRegisteredUrl |  |

## `wiinoma.Save`

| name | description |
| :--- | :--- |
| GetUserId |  |
| SetUserId |  |
| GetFavoriteId |  |
| SetFavoriteId |  |
| GetFamilyNum |  |
| GetMaxUserIdSize |  |
| GetMaxFavoriteIdNum |  |
| GetMaxFavoriteIdSize |  |

## `wiinoma.Mii`

| name | description |
| :--- | :--- |
| GetNum | Returns the current Mii's ID as a `Number`. It is one-indexed, so please subtract 1 to get its true ID. |
| GetFamilyId\(miiNum\) | Returns the Mii's family ID as a `Number`. |
| GetName\(miiNum\) | Returns the Mii's name as a `String`. |
| GetIconUrl\(facialType, miiNum\) | Returns a usable render of a specified Mii as a `String`. See [Facial Types](flash-api.md#facial-types) for usable types. |
| SetIconBgColor |  |
| SetIconSize |  |
| GetAge\(miiNum\) | Returns the Mii's age as a `Number`. |
| GetGender\(miiNum\) | Returns the Mii's gender as a `Boolean`. False is female, true is male. |

### Facial Types

| Type Name |
| :--- |
| `normal` |
| `anger` |
| `sorrow` |
| `surprise` |
| `blink` |
| `openmouth` |

## `wiinoma.Keyboard`

| name | description |
| :--- | :--- |
| SetFullWidthForNumeric |  |
| SetFullWidthForQwerty |  |
| SetFullWidthForNoRestriction |  |
| SetFullWidthForNumericWithPassword |  |
| SetFullWidthForQwertyWithPassword |  |
| IsFullWidthForNumeric |  |
| IsFullWidthForQwerty |  |
| IsFullWidthForNoRestriction |  |
| IsFullWidthForNumericWithPassword |  |
| IsFullWidthForQwertyWithPassword |  |

## `wiinoma.Evaluate`

| name | description |
| :--- | :--- |
| SetType |  |
| GetType |  |
| SetInfo1 |  |
| GetInfo1 |  |
| SetInfo2 |  |
| GetInfo2 |  |

## `wiinoma.Wipe`

| name | description |
| :--- | :--- |
| request |  |

## `wiinoma.HomeButtonMenu`

| name | description |
| :--- | :--- |
| SetForbidden |  |
| IsForbidden |  |

## `wiinoma.Personal`

| name | description |
| :--- | :--- |
| CanUse |  |
| UsingPasswordLock |  |
| CheckPassword |  |
| Get |  |

## `wiinoma.Progress`

| name | description |
| :--- | :--- |
| SetProgress |  |
| IsProgress |  |

## `wiinoma.ParentalControl`

| name | description |
| :--- | :--- |
| Restrict |  |
| CheckPassword |  |

## `wiinoma.MiiStamp`

| name | description |
| :--- | :--- |
| SetFamilyIndex |  |
| SetExpression |  |
| SetSKUCode |  |
| SetColor |  |
| SetBody |  |
| SetFont |  |
| SetMessage |  |
| SetError |  |
| SetPreviewUrl |  |
| SetOrderUrl |  |
| GetPreviewMovieClipUrl |  |
| GetPreviewLastError |  |
| getResult |  |

## `wiinoma.MiiSeal`

| name | description |
| :--- | :--- |
| SetFamilyIndex |  |
| SetExpression |  |
| SetDisplayScale |  |
| SetDisplayOffset |  |
| SetBodyVisible |  |
| SetAnimeType |  |
| SetOffsetType |  |
| SetAutoScale |  |
| SetOrderUrl |  |
| getResult |  |

