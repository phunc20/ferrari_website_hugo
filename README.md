# ferrari_website_hugo
Ferrari Liquor's website using Hugo framework


## Caveat
- `data/whisky/price.yaml`  
  The entries in this file correspond to the directories in `content/whisky`.
    - The naming of (directories) or (keys in this YAML file) is quite strict, e.g.
        - camel case not allowed (for example, `mL` should be replaced by, say, `ml`)
        - dot (i.e. `.`) seems to be not allowed
        - percentage sign (i.e. `%`) seems to be not allowed


## Testing
- Age verification
    - Once confirm >= 18 yo, how to have the popup back?  
      Ans: Since it's simply a Javascript toggle variable named
      `localStorage`: F12 to open developper tools > console > Type
      in the console's prompt `localStorage.clear()`, then it's done.


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
    - [x] Why in French's menu: Whisky is higher than Home? Ans: Simply because the
      weight in front matter is set diff in fr than in other languages.
1. [ ] Website's QR code
1. [ ] `data/price.yaml` cannot classify by cognac/whisky/etc.?
1. [ ] Refactor `layout/shortcodes/this_price.html` and `layout/partials/album-card.html`
1. Age verification
    - [ ] Switching btw pages popup still visible, even after confirmation. Why?
    - Which age?
        - <https://zh.wikipedia.org/zh-tw/%E5%90%88%E6%B3%95%E9%A3%B2%E9%85%92%E5%B9%B4%E9%BD%A1>
    - [ ] Still popping out (after confirmation of >= 18yo) ?
1. `about.html` to show
    - [ ] Google map
    - [ ] QR code of the website
1. [ ] Read the laws in Taiwan: <https://law.moj.gov.tw/LawClass/LawAll.aspx?pcode=G0330011>
1. [ ] Bombay Sapphire's logo's aspect ratio
1. [ ] Japanese numbers -> Full-width
