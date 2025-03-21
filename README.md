# ferrari_website_hugo
Ferrari Liquor's website using Hugo framework.
Like all `https://{userid}.github.io/{reponame}`,
the website should be at `https://phunc20.github.io/ferrari_website_hugo`.


## Constraints
- GitHub
    - <https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#usage-limits>
    - <https://github.com/actions/upload-pages-artifact/issues/71>


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
1. Front matter
    - `sort_by: Date` instead of `sort_by: Name`
1. Too heavy. (Cf. [Constraints](#constraints))  
   The GitHub Page contains too heavy an artifact. Lowering the image quality
   is one solution. E.g.
   ```
   magick <INPUT_FILE> -quality 30% <OUTPUT_FILE>
   ```
    - One may use, for example, the following command to locate large image files
      ```
      find . -name "*.jpg" -exec du -hsx {} \; | sort -h
      ```
    - To apply quality degradation on git-tracked files exclusively, the following
      commands might be useful
      ```bash
      # To test or dry-run: Ctrl-c to abort
      $ git lf content/*[^logo].jpg | xargs -p -I {} magick {} -quality 50% {}
      # To run officially
      $ git lf content/*[^logo].jpg | xargs -I {} magick {} -quality 50% {}
      ```
      Then, to add these modified files to the staging area,
      ```bash
      $ git add -u
      ```
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
1. [x] `sort_by: Name` -> `sort_by: Date`
    - A probably useful command:
      ```bash
      grep -Rn "sort_by: Name" | cut -d: -f1 | xargs -I {} sed -i 's/sort_by: Name/sort_by: Date/' {}
      ```
