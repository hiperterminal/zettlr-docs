# Preguntas frecuentes

## Intenté instalar Zettlr en Windows, ¡pero hay una advertencia de seguridad que dice que no debería instalar la aplicación!

Zettlr utiliza la firma de código según lo recomendado tanto  por Microsoft como por Apple para garantizar que instale solo software confiable. Sin embargo, en Windows, una aplicación necesita una cantidad suficientemente grande de instalaciones para suprimir esta advertencia de seguridad. Esta "confianza" se asigna a un certificado de firma de código, no a la aplicación en sí. Como Zettlr utiliza certificados emitidos de forma privada, estos tienen una vida útil limitada. El certificado actual es válido hasta 2022, después de lo cual Zettlr se firmará con un nuevo certificado que tiene que pasar por todo el proceso una vez más. Siempre que descargue Zettlr [desde nuestra página de inicio](https://www.zettlr.com/download) o desde la [página de lanzamientos de GitHub](https://github.com/Zettlr/Zettlr/releases) (ambos son los mismos archivos) puede instalar la aplicación de forma segura y descartar la advertencia.

## ¡No puedo ignorar la advertencia de seguridad en Windows y, por lo tanto, no puedo instalar la aplicación!

En muchas empresas, el departamento de Tecnología establece restricciones para que usted no pueda descartar una advertencia de seguridad por su cuenta y, por lo tanto, no pueda instalar la aplicación. Si trabaja en un entorno tan restringido, puede ser mejor hablar con su departamento de Tecnología y pedirles que incluyan Zettlr en la lista blanca para que usted (o sus administradores) puedan instalar la aplicación. Si tienen preguntas sobre los orígenes y / o la confiabilidad, puede ser mejor señalarlos [al repositorio GitHub de Zettlr](https://github.com/Zettlr/Zettlr).


## ¡Eliminé la carpeta de tutoriales de mi computadora y ahora no puedo recuperarla!

Cuando Zettlr detecta que se está ejecutando por primera vez en una computadora, automáticamente copiará una carpeta con algunos archivos Markdown en su carpeta Documentos. Estos archivos de Markdown contienen una introducción básica sobre cómo usar Zettlr. Sin embargo, solo se copiarán una vez. Para obtener estos archivos si luego se dio cuenta de que le gustaría volver a visitar el tutorial, tiene dos opciones:

* Cambie el nombre o elimine el archivo `config.json` del directorio de datos de su aplicación. Si ese archivo no está allí, Zettlr pensará que se está ejecutando por primera vez y volverá a copiar el tutorial.
* Simplemente [descargue la carpeta directamente desde la fuente](https://github.com/Zettlr/Zettlr/tree/develop/static/tutorial) (tenga en cuenta que esta ubicación puede cambiar).

## ¿Hay planes de migrar Zettlr a teléfonos móviles y tabletas, para Android o iOS?

Recibimos cada vez más solicitudes de versiones móviles de Zettlr. Estamos muy contentos de que te guste Zettlr lo suficiente como para quererlo en todos tus dispositivos, ¡y nos encantaría cumplir tu deseo! Sin embargo, desafortunadamente, nuestros recursos son suficientes para mantener el desarrollo de Zettlr en funcionamiento y, por el momento, no es posible agregar más trabajo.

## ¿Qué es Markdown?

Markdown es un lenguaje de marcado simple que le permite escribir texto tan complejo como usar un software de oficina estándar, pero con mucho menos desorden. En lugar de tener que seleccionar manualmente todas las opciones de formato, en Markdown, escribir un `#` es suficiente para indicar un encabezado. ¿Quieres escuchar más? ¡Entonces dirígete a la [documentación sobre Markdown](referencia / markdown-basics.md)!

## If I don't want to use Zettlr anymore, what would I need to do to switch programs?

Simply uninstall Zettlr and begin using another program of your choice. Zettlr does not mess with your files. If you have been using Projects or modified the directories, there will be small files named `.ztr-directory` present in some folders. To remove them, simply reset the sorting of directories to default, and remove all projects prior to uninstalling the app (or manually remove these files afterwards).

## I'm using Linux and deleting files doesn't move them to the trash!

Zettlr never completely removes your files. It always only moves them to the trash so in case you accidentally remove a file you need, you can always restore it. On macOS and Windows systems, the trash is activated by default, but on some Linux distributions, you need to activate the trash functionality manually. On Linux, Zettlr (to be more precise: the underlying Electron framework) makes use of the binary `gvfs-trash` to move files to the trash. To make use of this functionality, please make sure you have `gvfs-trash` installed! On Debian/Ubuntu you can do so by running the following code in a terminal:

```bash
$ sudo apt install gvfs-bin
```

> If you do not want to use the trash functionality, you can also enable the setting in the advanced preferences telling Zettlr to terminally remove a file if moving it to the trash fails. Please note that this will remove files irreversibly!

## My `Home` and `End`-keys behave weirdly! How do I fix that?

Zettlr uses the code editor CodeMirror under the hood. By default, it assumes that pressing either the `Home` or `End`-key should move the cursor to the beginning and ending of the _actual_ line. An actual line is defined as a contiguous stream of characters _without a line break_. This means that what we _see_ as a paragraph is actually one single line that has been wrapped when it gets too long (that is: the editor automatically inserts linebreaks when the line gets too long).

There is an option in the editor preferences that allows you to control this behavior. If the preferences option "Use CodeMirror default actions for `Home` and `End`" is checked, this means that pressing the `Home` and `End` key will move the cursor to the beginning/end of the _actual_ line (that is: the beginning/end of the paragraph you see). If the option is checked, the keys will move the cursor to the beginning/end of the _visible_ line (that is, it will respect the automatically inserted linebreaks).

## What is the correct URI formatting for Markdown links?

By default, Zettlr renders Markdown links in the format `[Your Link Text](your-link)` to be clickable (when holding down `Cmd` or `Ctrl`). However, Markdown links can point both to websites and to other files on your computer. You can omit a lot of information from your link, and Zettlr makes use of a heuristic to determine the information on its own, but it might infer false context for what you intend. Here's how it works:

- Links with all information present (a protocol and a fully qualified path) will not be altered. Examples: `file:///home/foo/documents/test.md` and `http://www.example.com/`.
- Relative links with the `file://`-protocol will be converted to absolute. Example: `file://./relative/file.md` will become `file:///home/foo/documents/relative/file.md`.
- Links without a protocol will be assumed to have `https://`. Example: `www.zettlr.com` will become `https://www.zettlr.com`.
- Absolute file paths, but without the `file://`-protocol will have that prefixed. Example: `/home/bar/documents/absolute.md` will become `file:///home/bar/documents/absolute.md`.
- Relative file paths with and without the relative-indicator (`./`) will be converted to absolute file paths. Example: `./more/relative.md` and `more/relative.md` will become `file:///home/foo/documents/more/relative.md`. **Exception**: They reside in the same folder: `file.extension` will in that case be treated like an URI (except the file is `.md`).

To sum up: If you worry about how your links are treated, be more explicit. Two general rules of thumb can be used to force Zettlr to treat a link as a file or web-link: Prepend a `./` to explicitly request a _file_ link, and append `/` to explicitly request a _web_ link.

## The internal links do not open the respective file!

In case the internal links used to interlink files don't work as expected, please make sure you've done the following things:

1. Is the link recognised? Zettlr enables you to define what internal links look like. By default, they are encapsulated by `[[` and `]]`. When Zettlr recognises an internal link, it will colour it and if you hover over it with your mouse cursor, the contained text should become underlined. If it does not, Zettlr doesn't think that what you've written is a link. You can change this in the settings.
2. Did you press the `Cmd` or `Ctrl` key while clicking on the link? Clicking with your mouse somewhere in the text means that you intend to edit the text, so you have to tell Zettlr that you actually want to follow the link.
3. Did you use a valid filename or ID? Zettlr only opens files, if they report they _exactly_ have the given ID or the given filename. If nothing happens while clicking on the link, this surely means that a file with the given ID or filename does not exist in the system. Note that you must omit the file extension when creating a link. For example, to link to `my-file.md`, you only need to put `my-file` inside the brackets.
4. Is the file currently loaded into Zettlr? Internal linking only works if Zettlr has read in the file.

## I know LaTeX and want to use it inside my Markdown files as well. Is this possible?

Yes. Simply write your `LaTeX` statements where you want them. As soon as you export to PDF, Pandoc will take care of the rest and the statements will be interpreted by the PDF engine. Unfortunately, `LaTeX` syntax highlighting is not supported. Also, please note that Pandoc will clear all `LaTeX` blocks prior to exporting to anything other than PDF, which means that blocks within `\begin` and `\end`, for instance, will be missing completely from the final Office file. On HTML-export, all `LaTeX` blocks will be retained, but not converted to something else.

## I can't seem to align the text just or right!

It's not a bug, it's a feature: Markdown does not have the respective formatting signs because text should always be justified or aligned left (for LTR languages) and therefore it does not belong to the set of necessary block formats Markdown offers. Yet, you can still use `LaTeX` commands to render them left or right. Simply enclose the text you want to align right or justify in `\begin{<option>}` and `\end{<option>}`, where `<option>` may either refer to `flushleft`, `flushright` or  put a `\justify` in front of a paragraph you want to be justified. [Learn more at sharelatex.com](https://www.sharelatex.com/learn/Text_alignment).

## In PDF output, I want certain headings to be unnumbered/not listed in the Table of Contents

This is a special feature of Pandoc. Add the special classes `-` (simply a minus) or `.unlisted` respectively. The minus prevents numbers, while “unlisted” prevents the heading to appear in the table of contents. Note that this only applies to PDF output.

Examples:

```markdown
# This heading will be unnumbered, but in the ToC {-}

# This heading will be numbered, but not in the ToC {.unlisted}

# This heading will both be unnumbered, and hidden from the ToC {- .unlisted}
```

> Note that the special classes need to be the last thing on the line. Even comments will break this behaviour.

## I want to use single line breaks and not create new paragraphs. When I simply hit Enter once, it removes the single line break!

To force Pandoc to render single line breaks as such, end your line with a backslash (`\`) or two spaces. The backslash as well as the two spaces will not be rendered in the exported file.

## Zettlr does not seem to find LaTeX, which is nonetheless installed!

This can happen in case your computer decided to install the software in a non-standard directory. Zettlr will try its best to locate the applications but may fail if they are buried somewhere. Make sure the xelatex binary is within your PATH.

## On Export to PDF, I constantly get error messages!

It might happen that you get certain errors when trying to export your files. There are two common types of errors, which you can solve by yourself.

The most common error looks like this:

**LaTeX Error: File \<some name\>.sty not found.**

This simply means that a certain package was not found (they end in `.sty`). On Windows, these packages should be installed automatically as soon as they are needed (a window might pop up asking you for confirmation); on macOS and Linux you simply need to run the command `tlmgr install <some name>`.

> Note that some `.sty`-files are part of larger packages. The easiest way to find out which package to install, go to [the CTAN homepage](https://ctan.org/) and search for the package name (the file name without the `.sty`). You will then see in the "Contained in"-section the actual name of the package you have to install. Example: [The `footnote.sty`-package](https://ctan.org/pkg/footnote) is contained in the package `mdwtools`, so instead of running `tlmgr install footnote` you must run `tlmgr install mdwtools`.

In case of other errors, Zettlr enables you to copy and paste text from the error message, because in almost all cases, a short Google search leads to a solution. And if it doesn't the community can better help you if they see the error you are getting.

## I found a bug!

That's great news! Well, not great, but it's good that you found it! In this case please head over to [GitHub](https://github.com/Zettlr/Zettlr/) and open up an issue so that we know what's up and can work to resolve the bug.

## I have a feature request! / I have a suggestion for making a feature more efficient!

That's good to hear! We always depend on other people's experience with the app to improve its efficiency and its usability for different situations. In this case, please head over to [GitHub](https://github.com/Zettlr/Zettlr/) and open up an issue so that we can get right to it.

## What about my privacy? Does Zettlr transfer any data, or don't I have to worry?

Zettlr is privacy-first. It does not send any data, and it is fully functional offline. However, whenever you open Zettlr, or use the corresponding menu item, Zettlr will connect to the Zettlr-API to retrieve a list of all releases. This list is then used to determine whether or not you are using the newest release. During the connection, the Zettlr server will receive your IP-address, and this information stored for a maximum of 30 days (using logrotation), which is pretty common among servers. This information will never leave our server and will only be used during incidents to determine what happened. After the 30 days, the access will be removed from the server logs. We're Open Source, not Facebook.
