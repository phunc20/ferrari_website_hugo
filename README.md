# ferrari_website_hugo
Ferrari Liquor's website using Hugo framework.
Like all `https://{userid}.github.io/{reponame}`,
the website should be at `https://phunc20.github.io/ferrari_website_hugo`.


## Installation
- Hugo
    - Debian  
      `apt` sometimes appears too outdated, in which case one may be interested
      in downloading and installing from, e.g. the latest `.deb` release
        1. Go to <https://github.com/gohugoio/hugo/releases/latest>
        1. Download the `.deb` of your likings, just note that there are, as of 2025, different choices btw
            - `hugo`
            - `hugo_extended`
            - `hugo_extended_withdeploy`
    - Arch Linux  
      `pacman` usually provides the latest. Go to <https://github.com/gohugoio/hugo/releases/>
      if you want a different release.


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
1. `sort_by: Name` -> `sort_by: Date`
    - [ ] Make sure bottles are sorted in the same order across all languages
        - A probably useful command:
          ```bash
          grep -Rn "sort_by: Name" | cut -d: -f1 | xargs -I {} sed -i 's/sort_by: Name/sort_by: Date/' {}
          ```
    - [ ] Make sure brands are also sorted in the same order across all languages
        - Rule for brand order
            - Alphabetical order (English):
                1. ABCD
                2. EFGH
                3. IJKL
                4. MNOP
                5. QRST
                6. UVW
                7. XYZ
            - Stop ordering through `weight`; instead, write code using alphabetical order from English.
1. [ ] Add filters to each page
1. Logo images
    - Opacity
      ```
      convert input_image.png -background white -alpha remove -alpha off output_image.png
      ```
    - Crop
        - 1st example:
          ```bash
          $ file .trash/ok/aa.png
          .trash/ok/aa.png: PNG image data, 449 x 539, 8-bit/color RGB, non-interlaced
          $ convert .trash/ok/aa.png -crop 449x290+0+45 cut.png
          ```
          where `449x290+0+45` means starting the crop at the coordinate `(0, 45)` and cropping an image of size
          `449x290`.
    - Zoom out
        - By `-extent`
          ```bash
          $ convert .trash/no/bc_logo.png -gravity Center -extent 400x400 out.png
          ```
            - Options for `-gravity` are `Center`, `North`, `South`, `East`, `West`, `NorthWest`, `NorthEast`, `SouthWest`, `SouthEast`.
            - `-extent <new_width>x<new_height>`
1. Karaoke
    - Search system
        - [ ] `jsonl` data format for easier Git version control
    - Knowledge
        - [ ] Security in Javascript/Go
            - [`safe.JS`](https://gohugo.io/functions/safe/js/)
            - [`encoding.Jsonify`](https://gohugo.io/functions/encoding/jsonify/)
            - [`transform.Unmarshal`](https://gohugo.io/functions/transform/unmarshal/)


## Theme
- `layouts/` files and their purposes
    - `_default/`
        - `home.html` is the first page of the website, i.e. the main page.
        - `list.html` is the pages of categories of alcohols, e.g. `whisky`, `wine`, `baijiu`, etc.
- `assets/`
    - `css/`
        - You can put your customized CSS file inside this directory. For example, if you have an HTML
          file under the path `content/karaoke-by-gender.html` and you want it attached with a CSS file
          `assets/css/karaoke-by-gender.css` then you should
            1. Create and edit a Markdown file under, say, `content/karaoke-by-gender.md` with front matter
               similar to that from below.
               ```markdown
               ---
               title: "依照歌手查詢"
               #url: "/karaoke-by-gender/"
               layout: karaoke-by-gender
               ---
               ```
            1. Create and edit an HTML file, under e.g., `layouts/_default/karaoke-by-gender.html`
            1. Create and edit a CSS file under `assets/css/karaoke-by-gender.css`. E.g.
               ```css
               form {
                   font-size: 1.125rem;
               }
               ```
            1. Import that CSS file in your `assets/css/main.scss`
               ```scss
               @import "karaoke-by-gender";
               ```


## Competitors or Colleagues
可以互相參考價格

- [旺旺洋酒 aka 大旺購物網](https://wangwang.tw)
    - 門市地址 and 電話
        - 彰化市自強南路 28 號, 04-7226662
        - 臺中市南屯區大墩二街 19 號 1 樓, 04-24716920
