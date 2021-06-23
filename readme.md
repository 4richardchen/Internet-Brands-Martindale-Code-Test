# Instructions
Use [bootstrap4](https://getbootstrap.com/docs/4.0/getting-started/download/), [flexslider2](http://flexslider.woothemes.com/), and flat HTML files to implement 1 [this design](https://marvelapp.com/prototype/1198h7ej/screen/71061973/handoff)'s 2c media slider, full width media slider, and 4c in grid media slider.
  
# How to View
Clone this repo (not quite worth making this repo into a GitHub Pages-enabled one, just yet) then open [12c-media-slider](12c-media-slider.html), [4c-in-grid-media-slider](4c-in-grid-media-slider.html), and [full-width-media-slider](full-width-media-slider.html) in any modern browser.

Note: to load `file://` resources in Safari, go to Develop > Disable Local File Restrictions

# Approach, Methodology, Design Principles

Edit Bootstrap's default breakpoints and gutter, compile correspondingly new bootstrap css, use it in the page.

Avoid any http(s) calls to avoid non-availability due to firewall or host's deletion.
 
## Measurements

4c: If container is 1140px, then the gutters of 15px mean the 4c module will be 380px wide which with 15px gutters means the content is 350px wide. I chose that the module goes full width (a.k.a. col-12) below "lg" width (760px) for readability, but Marvel doesn't answer/state it explicitly.

Sticking to built-in p-`{spacing}` classes means 12c-media-slider's content title's `mt-5` should be 37px. I didn't add new p-`{spacing}` classes.

Content "Global Section Top + Bottom Padding" uses font of Marvel comments so I disregarded it accordingly.

Using flexslider's own image resizing logic, but can use img cover-fit to make it work better which would require knowing flexslider core thus didn't. Likewise for how it has a double-click-on-custom-control-to-wrap-around annoyance.

Marvel only zooms at 100% in Handoff mode so to compare a Marvel screenshot overlaid on the browser rendered version requires mosaicing multiple screenshots in Photoshop which was too time-consuming but I usually do such overlays to check my work.

## Time
I spent 7h total: 30m on Thursday, 2h on Friday, and balance on Monday, May 24. The most time consuming were sass maps, slider controls of [basic-slider-with-custom-direction-nav](flexslider/demo/basic-slider-with-custom-direction-nav.html), and doubling back on separating 3 templates after realizing all can't be in 1 file (tried, logically impossible, retreated). I enjoyed everything so much, limited only by having time only during working hours, and hope you enjoy my work, too.

## Bonus
I realized bonus takes only 3 sass lines (`:64:66`) and 1 html (`:9`) line of edits thus took only 30m, 20m of which was reading the Marvel app.

Notes about [light vs dark configuration](https://marvelapp.com/prototype/1198h7ej/screen/79523180/handoff):

* text button colors, foreground and background, both don't match [dark configuration in task](https://marvelapp.com/prototype/1198h7ej/screen/71061973/handoff) and is kept same so I also kept it the same
* likewise for slider indicators which aren't given at all; even if using pagination indicator colors they also don't match the latter asset
* likewise for module subtitle color

# Steps Taken

## Separate Vendor Assets
```sh
git init
git submodule add git@github.com:twbs/bootstrap.git
```

Download [flexslider](https://flexslider.woothemes.com), [Lato](https://fonts.google.com/specimen/Lato), and [Nunito Sans](https://fonts.google.com/specimen/Nunito+Sans).

No `vendor` folder as these three are documented as untouched.

## Code
[Customizing defaults](https://getbootstrap.com/docs/4.0/getting-started/theming/#variable-defaults) avoids re[building Bootstrap](https://getbootstrap.com/docs/4.0/getting-started/build-tools/#tooling-setup); keep Bootstrap's in its untouched git submodule (thus retains upgrade path); and to improve maintainability, readability, and labor.

```sh
vi css/main.sass
```
and html's and this readme.

## Compile
Pre-requisite is sass. Sourcemaps are on by default and we include them in the zip for dev.
```sh
sass -q --no-source-map css/main.sass css/main.css
```

## Test, QA, UAT
Tested on all modern browsers in [BrowerStack](https://browserstack.com).
