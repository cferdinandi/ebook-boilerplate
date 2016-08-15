# Ebook Boilerplate
A lightweight boilerplate for self-publishing ebooks with markdown and command line. The ebook boilerplate transforms markdown files into PDF, EPUB, and MOBI files.

[Download the Ebook Boilerplate](https://github.com/cferdinandi/ebook-boilerplate/archive/master.zip)



## Getting Started

### Dependencies
Make sure these are installed first.

- [Pandoc](http://pandoc.org) (*you can skip the LaTeX dependency---we're using wkhtmltopdf instead*)
- [wkhtmltopdf](http://wkhtmltopdf.org)
- [Calibre](https://calibre-ebook.com/)

### Structure

- Save your book content as markdown files in the `chapters` directory. I recommend prefixing chapter names with numbers to order them.
- Save project images in the `img` directory. These should be referenced in your chapters relative to the root directory: `![Image caption](img/filename.jpg)`.
- Book assets---CSS, metadata, etc.---go in the `assets` directory.

### Quick Start

1. Add your book title, subtitle, author info, and so on to the `metadata.yml` and `title.md` files in the `assets` directory.
2. In bash/terminal/command line, `cd` into your project directory. Run the following commands, replacing `book` with your desired filename:

  **EPUB**
  ```bash
  pandoc assets/metadata.yml chapters/*.md -o book.epub -S
  ```

  **PDF**
  ```bash
  pandoc assets/title.md chapters/*.md -o book.pdf -t html5 -S -V papersize:"letter" -c assets/pandoc.css
  ```

  **MOBI**
  ```bash
  ebook-convert book.epub book.mobi
  ```



## Quirks and Other Issues

1. I use wkhtmltopdf instead of LaTeX because it lets you style PDFs with CSS, giving you much more control over how things look.
2. I don't apply any CSS to the EPUB and MOBI formats. I've had better support across a wider range of ereaders by letting them just use their default styles.
3. wkhtmltopdf does not add page numbers to the generated PDF, and I've yet to find a way to make it do so.
4. wkhtmltopdf also does not let you add a full-bleed cover image. You can either create a title page with an image on it, or generate a separate PDF and merge the two later.
5. You **must** include an empty line before you're `h1` level markdown headers (ex. `# Chapter Title`) or Pandoc will just skip it when creating your file. No idea why.
6. Break tags (`<br/>`) must include the self-closing slash (ie. don't do this: `<br>`) or they'll throw an error, even though slashless is valid HTML5.



## How to Contribute

Please review the  [contributing guidelines](CONTRIBUTING.md).



## License

The code is available under the [MIT License](LICENSE.md).