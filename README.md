# Ebook Boilerplate
A lightweight boilerplate for self-publishing ebooks with markdown and command line. The ebook boilerplate transforms markdown files into PDF, EPUB, MOBI, and HTML files, *and* provides a zipped version with all four.

*__Note:__ This works in MacOS, but has not been tested in Windows. At a minimum, the `zip` command will not work and will need to be set to `false`.*

[Download the Ebook Boilerplate](https://github.com/cferdinandi/ebook-boilerplate/archive/master.zip)



## Quick Start

Make sure these are installed first.

- [Pandoc](http://pandoc.org) (*you can skip the LaTeX dependency---we're using wkhtmltopdf instead*)
- [wkhtmltopdf](http://wkhtmltopdf.org)
- [Calibre](https://calibre-ebook.com/)

In bash/terminal/command line, `cd` into your project directory. Then run:

```bash
sh build.sh
```

This will create your ebook files from your markdown files and assets.



## Project Structure

- Add your book title, subtitle, author info, and so on to the `metadata.yml` and `title.md` files in the `assets` directory. Fields that you need to update are in *ALL CAPS* so that you can easily find them.
- Save your book content as markdown files in the `chapters` directory. I recommend prefixing chapter names with numbers to order them.
- Book assets---CSS, metadata, etc.---go in the `assets` directory.
- Save project images in the `assets/img` directory (or anywhere else that makes sense for you). These should be referenced in your chapters relative to the root directory: `![Image caption](assets/img/filename.jpg)` or `<img src="assets/img/filename.jpg">`.
- *If you want a cover for your PDFs*, include a `cover.pdf` file in the `assets` directory.



## Configuration

There are two ways to configure the Ebook Boilerplate:

1. Open up the `build.sh` file and change the defaults.
2. Pass in flags with the `sh build.sh` command.

### Defaults

```bash
# Defaults
TITLE='ebook' # the title/filename
EPUB='false'  # if true, publish an EPUB version
PDF='false'   # if true, publish a PDF
MOBI='false'  # if true, publish a MOBI version
HTML='false'  # if true, public an HTML version
ZIP='false'   # if true, create a zip file
ALL='true'    # if true publish all formats (regardless of other settings)
COVER='false' # if true, add a cover for the PDF version
```

### Flags

- **`-t 'title'`** - The title/filename to use for your ebooks (defaults).
- **`-e`** - If enabled, generate an EPUB.
- **`-p`** - If enabled, generate a PDF.
- **`-c`** - If enabled, add a cover to the PDF file.
- **`-m`** - If enabled, generate a MOBI file.
- **`-h`** - If enabled, generate an HTML file.
- **`-z`** - If enabled, generate a zip file (requires all four other file types to work).
- **`-a`** - If enabled, generate all file types (defaults to `true`).

Enabling individual file types (`-e`, `-p`, `-m`, or `-h`) will automatically set *all file types* (`-a`) to `false`.

### Examples

**Custom title**

```bash
sh build.sh -t 'my-awesome-ebook'
```

**Only generate a PDF and EPUB**

```bash
sh build.sh -e -p
```

**Only generate a PDF and EPUB with a custom title**

```bash
sh build.sh -t 'my-awesome-ebook' -e -p
```

**Use a cover with your PDFs**

```bash
sh build.sh -c
```



## Quirks and Other Issues

1. I use wkhtmltopdf instead of LaTeX because it lets you style PDFs with CSS, giving you much more control over how things look.
2. I don't apply any CSS to the EPUB and MOBI formats. I've had better support across a wider range of ereaders by letting them just use their default styles.
3. wkhtmltopdf does not add page numbers to the generated PDF, and I've yet to find a way to make it do so.
4. You **must** include an empty line before youR `h2` page-level markdown headers (ex. `## Chapter Title`) or Pandoc will just skip it when creating your file. No idea why.
5. Break tags (`<br/>`) must include the self-closing slash (ie. don't do this: `<br>`) or they'll throw an error, even though slashless is valid HTML5.



## License

The code is available under the [MIT License](LICENSE.md).