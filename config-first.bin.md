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
  <shopurl>http://shop.prod.wiilink24.com/index.esf</shopurl>
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

