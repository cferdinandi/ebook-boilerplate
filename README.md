# Ebook Boilerplate
A lightweight boilerplate for self-publishing ebooks with markdown and command line. The ebook boilerplate transforms markdown files into PDF, EPUB, MOBI, and HTML files, *and* provides a zipped version with all four.

*__Note:__ This works in MacOs, but has not been tested in Windows. At a minimum, the `zip` command will not work and will need to be removed from the `build.sh` file.*

[Download the Ebook Boilerplate](https://github.com/cferdinandi/ebook-boilerplate/archive/master.zip)



## Getting Started

### Dependencies
Make sure these are installed first.

- [Pandoc](http://pandoc.org) (*you can skip the LaTeX dependency---we're using wkhtmltopdf instead*)
- [wkhtmltopdf](http://wkhtmltopdf.org)
- [Calibre](https://calibre-ebook.com/)

### Structure

- Save your book content as markdown files in the `chapters` directory. I recommend prefixing chapter names with numbers to order them.
- Book assets---CSS, metadata, etc.---go in the `assets` directory.
- Save project images in the `assets/img` directory (or anywhere else that makes sense for you). These should be referenced in your chapters relative to the root directory: `![Image caption](assets/img/filename.jpg)` or `<img src="assets/img/filename.jpg">`.

### Quick Start

1. Add your book title, subtitle, author info, and so on to the `metadata.yml` and `title.md` files in the `assets` directory. Fields that you need to update are in *ALL CAPS* so that you can easily find them.
2. Open up `build.sh` and change the `FILENAME` variable to the filename you'd like to use for your ebook files.
3. In bash/terminal/command line, `cd` into your project directory. Run `sh build.sh` to create your files.



## Building Individual Files

Don't want to build everything at once? You can manually build different formats, too.

**EPUB**
```bash
pandoc assets/metadata.yml chapters/*.md -o BOOK-TITLE.epub -S
```

**PDF**
```bash
pandoc assets/title.md assets/toc.md chapters/*.md assets/scripts.md -o BOOK-TITLE.pdf -t html5 -S -V papersize:"letter" -c assets/pandoc.css
```

**MOBI**
```bash
ebook-convert book.epub book.mobi
ebook-convert BOOK-TITLE.epub BOOK-TITLE.mobi
```

**HTML**
```bash
pandoc -H assets/pandoc-before.css -H assets/pandoc.css -H assets/pdf-overrides.css -H assets/pandoc-after.css assets/title.md assets/toc.md chapters/*.md assets/scripts.md -o BOOK-TITLE.html -S
```

**Zip**<br>
*You'll need to remove any file formats you did not create*
```bash
zip BOOK-TITLE.zip BOOK-TITLE.epub BOOK-TITLE.mobi BOOK-TITLE.pdf BOOK-TITLE.html
```



## Quirks and Other Issues

0. I use wkhtmltopdf instead of LaTeX because it lets you style PDFs with CSS, giving you much more control over how things look.
0. I don't apply any CSS to the EPUB and MOBI formats. I've had better support across a wider range of ereaders by letting them just use their default styles.
0. wkhtmltopdf does not add page numbers to the generated PDF, and I've yet to find a way to make it do so.
0. wkhtmltopdf also does not let you add a full-bleed cover image. You can either create a title page with an image on it, or generate a separate PDF and merge the two later.
0. You **must** include an empty line before youR `h2` page-level markdown headers (ex. `## Chapter Title`) or Pandoc will just skip it when creating your file. No idea why.
0. Break tags (`<br/>`) must include the self-closing slash (ie. don't do this: `<br>`) or they'll throw an error, even though slashless is valid HTML5.



## License

The code is available under the [MIT License](LICENSE.md).