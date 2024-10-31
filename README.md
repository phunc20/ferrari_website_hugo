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
1. [ ] Put the prices in the outer album card.
2. Themes
    - [ ] `grep -Rn "photoCount" layouts/` add price at an earlier stage
