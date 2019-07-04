# salesforce-gitattributes
.gitattributes Templates for Salesforce

## Simple Version

In this version we're just making some big assumptions about our repository to keep our `.gittatributes` file as slim as possible. We're also minimizing the risks when working across systems.

### Line Ending Normalization

By default all Salesforce files are retrieved with an LF as line ending. To keep this consistent across systems and not introduce any differences when retrieving files from our org, we force the LF with `eol=lf` for all files. But not all files are created equal and someday somebody might commit some binary files which we don't want to normalize - so instead of `text` we're better using `text=auto` to make use of Git's internal binary detection mechanism. If you're sure you never will commit any unexpected binary files you can opt for the former to save on some processing overhead.

#### Result

`* text=auto eol=lf` (with binary detection - our default)
`* text eol=lf` (without binary detection - alternative)

### Binaries

Sometimes Git will not correctly deduce our file type and will incorrectly normalize e.g. images - therefore screwing up our files on commit. This is especially true for Static Resources as these are often of binary nature. Since we started with a catch all we make use of the built-in macro attribute `binary` to exclude all Static Resources (and every other file type that is binary).

#### Result

`*.resource binary` (example for Static Resources)

### Binary Exceptions (e.g. Static Resources)

If we define all Static Resources as binary - we sometimes might catch a file that is not binary at all. We want to exclude these so they are getting normalized correctly as well. Since they are mostly very specific we know they are just text and therefore we can just opt for `text`. As an added bonus we could also add e.g. `diff=css` for CSS files to get a better hunk header by using the built-in Git diff driver for CSS files.

#### Result

`*_css.resource text eol=lf diff=css` (example for CSS files)
