# Common Error Codes

## What is first.bin?

`first.bin` is the file initially requested for configuration pointing to URL types the channel should request.

Despite it being XML internally, the file is encrypted. It's unknown why this design was chosen, as the file was served over HTTPS by Nintendo. AES is symmetric and provides no method of signing. Additionally, the keys are easily found within the channel's contents.

This is AES-128-CBC encrypted, using keys available within the app's main arc.

Here is an example `openssl` command to decrypt an existing one using the default Nintendo-provided key and IV:

```text
openssl aes-128-cbc -d -in first.bin -out first.txt -K 943B13DD87468BA5D9B7A8B899F91803 -iv 66B33FC1373FE506EC2B59FB6B977C82
```

To encrypt, simply swap the `-d` \(decrypt\) flag for `-e` \(encrypt\).

## Example Contents

```markup
<Config>
  <ver>399</ver>
  <maint>0</maint>
  <url1>http://url1.dev.wiilink24.com/</url1>
  <url2>http://url2.dev.wiilink24.com/</url2>
  <url3>http://url3.dev.wiilink24.com/</url3>
  <eulaver>3</eulaver>
  <shopurl>http://shop.dev.wiilink24.com/index.esf</shopurl>
  <shopkey>7fce738e542f0a60fe5d8d8e1e8781af</shopkey>
  <shopvalid>1</shopvalid>
  <akahost>5</akahost>
  <akaca>1</akaca>
  <smpkey>5ab362aa57dbb1dc16849e3e2d1cf2ff</smpkey>
  <fmax>30</fmax>
  <bmax>10</bmax>
  <upddt>2021-01-13T08:06:31</upddt>
</Config>
```

* If `ver` is set to 9999, the title notes that it is discontinued with error 354606. This can be done with any request, however it makes the most sense to have set within the first request. If set, it does not persist, unlike other Nintendo-made channels.
* `maint` is a [Boolean](generic-terminology.md#xml-types). If set, it displays an "under maintenace" dialog with error 354608.
* `urlX` is a string used to set the URL used with each type. In general, `url1` is used for static data, `url2` is used for CGI-related requests, and `url3` is for static theatre data.
  * v512 only requires `url1` and `url2`, as it lacks any theatre functionality. It will ignore `url3` if given.
* `eulaver` is an Integer denotes the used version of the EULA. The EULA requested has no version attached, however - perhaps some part of save data is able to compare across versions.
  * v512 requires an `eulaver` of 2, where v770/v1025 require 3.
* `upddt` is a [DateTime](generic-terminology.md#xml-types). It does not appear to persist anywhere in save files or accessed elsewhere in memory.

{% hint style="info" %}
The following fields are used within v1025. v512 and v770 only use the fields listed above.
{% endhint %}

* `shopurl` is a direct URL to the encrypted SWF used for the shop.
* `shopkey` is the AES key used for the encrypted shop SWF.
  * Its corresponding IV is hardcoded to be `c12cf59b941a4d69b65771e8a8ef96e2`.
*  `shopvalid` is a Boolean. It is unknown how it is used.
* `akahost` is unknown at this time.
* `smpkey` is the AES key used to encrypt food delivery SWFs.
  * Its IV is unknown at this time.
* `fmax` and `bmax` are unknown.

