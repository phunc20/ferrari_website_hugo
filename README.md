# ferrari_website_hugo
Ferrari Liquor's website using Hugo framework


## Caveat
- `data/whisky/price.yaml`  
  The entries in this file correspond to the directories in `content/whisky`.
    - The naming of (directories) or (keys in this YAML file) is quite strict, e.g.
        - camel case not allowed (for example, `mL` should be replaced by, say, `ml`)
        - dot (i.e. `.`) seems to be not allowed
        - percentage sign (i.e. `%`) seems to be not allowed


## TODOs
1. Price
    - [ ] Put the prices in the outer album card.
    - [ ] Bold or bigger font
1. Themes
    - [ ] `grep -Rn "photoCount" layouts/` add price at an earlier stage
    - [ ] Flag and language switcher on each page
        - <https://gohugo.io/content-management/multilingual/#reference-translated-content>
        - <https://discourse.gohugo.io/t/language-switcher-in-menu/11570/8>
1. Absurd
    - [ ] Why in French's menu: Whisky is higher than Home?
1. [ ] Website's QR code
1. [ ] `data/price.yaml` cannot classify by cognac/whisky/etc.?
