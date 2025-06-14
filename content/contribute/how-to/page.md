# Using this Book

This book contains all the Academy's content in _sequence_.\
It is intended to read from start to finish, in order, and following the `index.md` page for each module.

## 📔 How to use `mdBook`

This book is made with [mdBook](https://rust-lang.github.io/mdBook/) - a Rust native documentation tool.\
Please give the official docs there a read to see what nice features are included.\
To name a [few key items](https://rust-lang.github.io/mdBook/guide/reading.html#top-menu-bar):

| Icon | Description                                                                     |
| ---- | ------------------------------------------------------------------------------- |
|      | Opens and closes the chapter listing sidebar.                                   |
|      | Opens a picker to choose a different color theme.                               |
|      | Opens a search bar for searching within the book.                               |
|      | Instructs the web browser to print the entire book.                             |
|      | Opens a link to the website that hosts the source code of the book.             |
|      | Opens a page to directly edit the source of the page you are currently reading. |

### Search

Pressing the search icon () in the menu bar, or pressing the `S` key on the keyboard will open an input box for entering search terms.\
Typing some terms will show matching chapters and sections in real time.

Clicking any of the results will jump to that section.\
The up and down arrow keys can be used to navigate the results, and enter will open the highlighted section.

After loading a search result, the matching search terms will be highlighted in the text.\
Clicking a highlighted word or pressing the `Esc` key will remove the highlighting.

## 🎞️ How-to use `reveal.js` Slides

Most pages include _embedded slides_ that have a lot of handy features.\
These are with [`reveal-md`](https://github.com/webpro/reveal-md): a tool built with `reveal.js` to allow for [Markdown](https://commonmark.org/help/) only slides, with a few extra syntax items to make _your slides look and feel awesome_ with very little effort.

> 📝 Be use to have _the slides `iframe` on a page active_ (🖱️ click on it) to use slide keybindings...\
> Otherwise those are captured by the `mdbook` tools!\
> (`s` is search for the book, and speaker notes for the slides)

Be a `power user` of these by using the **keybindings** to interact with them:

* Use `space` to navigate _all_ slides: top to bottom, left to right.
  * Use `down/up` arrow keys to navigate _vertical_ slides.
  * Use `left/right` arrow keys to navigate horizontal slides.
* Press `Esc` or `o` to see an `overview` view that arrow keys can navigate.
* Press `s` to open up speaker view.\
  **👀 Speaker notes include very important information, not to be missed!**

### 💫 Slides Demo

Tryout those keybindings (🖱️ click on the slides to start) below:

[How to use the slides](page.md#-how-to-use-revealjs-slides) -[Full screen slides (new tab)](slides.html)\


<details>

<summary>(🖱️ expand) Raw Markdown of Slides Content</summary>

\{{#include slides.md\}}

</details>

☝️ All slides `Slides Content` is available on all pages.\
This enables **search** to work throughout this book to **jump-to-location** for any keywords you remember related to something covered in a lesson 🚀.

### 📖 Learn More

* [https://revealjs.com/](https://revealjs.com/)
  * [Official Slides Demo](https://revealjs.com/demo/)
* [Markdown ➡ Slides Build Tooling](https://github.com/webpro/reveal-md/)
