# Config \(first.bin\)

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
  <akahost>.akamai.net</akahost>
  <akaca>1</akaca>
  <smpkey>5ab362aa57dbb1dc16849e3e2d1cf2ff</smpkey>
  <fmax>30</fmax>
  <bmax>10</bmax>
  <upddt>2021-01-13T08:06:31</upddt>
</Config>
```

### Contents

* `ver` is the same as any other request. If set to 9999, it states that the service has been discontinued and returns an error of 354606.
* `maint` is a Boolean. If true, it states that the service is under maintenance with an error of 354608.
* `urX` provides the direct URL to various service types.
  * `url1` is typically used for static data, such as image assets.
  * `url2` has CGI data.
  * `url3` has static theatre data. As such, it is not used in v512.
* `eulaver` must be 2 in v512, and 3 in v770. It is unknown if it is recorded.
* `upddt` is a [DateTime](generic-terminology.md#xml-types). It does not appear to be recorded.

{% hint style="info" %}
The following fields are speciifc to v1025. They are ignored if set in older versions.
{% endhint %}

* `shopurl` is a direct URL to the encrypted SWF used for the shop. In general, the `esf` file extension denotes an encrypted SWF.
* `shopkey` is the AES key used to encrypt the shop's SWF.
  * Its respective IV, `c12cf59b941a4d69b65771e8a8ef96e2`, is hardcoded.
* `shopvalid` is unknown. It does not appear to be used once set, and does not hide/remove the shop.
* `akahost` is a string. If a URL matches the host, `akaca` is checked.
* `akaca` is a Boolean. If true, it appears to load `AddTrustExternalCARoot.cer` and `GTEGlRoot.der` to the IOS SSL trust store for requests. This additionally appears to occur for domains matching `.wiinoma.co.jp` and `.ext.wapp.wii.com`.
* `smpkey` appears to be the key used to encrypt SWFs used for external deliveries.
* `fmax` and `bmax` are unknown. They both have been observed to be 10.

