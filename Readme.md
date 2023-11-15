# Portfolio Website
This is the source code for my website. I use this website to write CTF [writeups](https://iasad.me/write-ups), [notes](https://notes.iasad.me), and [blogs](https://iasad.me/blogs) on topics that interest me. I also use this website to host my [resume](https://iasad.me/resume).
## Credits
* I use [Hugo](https://gohugo.io/) to generate the website.
* Color scheme is inspired by the [Gruvbox](https://github.com/morhetz/gruvbox) color palette.
* I am using [Fira Code](https://fonts.google.com/specimen/Fira+Code) font.
* I am using [Papermod](https://github.com/adityatelange/hugo-PaperMod) theme with some tweaks.

## Tweaks 
I've made the following modifications to the theme. If you like any modification and wish to implement it, simply copy the respective file to your `assets/css/extended` folder.

* Updated colors in `assets/css/extended/theme-vars.css`
* Added Terminal like prompt in header `assets/css/extended/prompt.css`
* Updated search page style `assets/css/extended/search.css`
* Updated tags and categories page style to a tags cloud
    *  `assets/css/extended/tagscloud.css`
    *  `assets/css/layouts/_default/terms.html`
* Updated archive page style `assets/css/extended/archive.css`
* Fixed thumbnail image size `assets/css/extended/thumbnail.css`