# Sniprun

Sniprun is a (still WIP) code runner plugin. It aims to provide stupidly fast testing for interpreted _and_ compiled languages.

Ever dreamt of printing the type of that obscure object, or that list to check if it contains everything you expect, but it was all pipe dream as your code would not even compile/run in its unfinished state?
Quickly grab some visual range, `:'<,'>SnipRun` it and... that's it! And there's more!

## Installation

(Recommended) Use your favorite plugin manager. (Run `install.sh` as a post-installation script, it will download or compile the sniprun binary)

For example, `vim-plug`:

```vim
Plug 'michaelb/sniprun', {'do': 'bash install.sh'}
```

Sniprun is developped and maintained on Linux (-only for now), support for other platforms is not in my goals plans, though simple compatibility patches PR are welcome.

## Usage

Sniprun is and will always (try to) be dead simple. `:SnipRun` a piece of code and the plugin will return its standart output. ( +stderr if supported)

### Running

Line mode: Place your cursor on the line you want to run, and type (in command mode):

```vim
:SnipRun

```

Bloc mode: Select the code you want to execute in visual mode and type in:

```vim
:'<,'>SnipRun
```

(nota bene: the `:'<,'>` is often pre-typed and appears if you type in `:`)

### Stopping

_ARGHHH_ I 'SnipRan' and infinite loop (or anything that takes too long)!
No worries, the second and last command will kill everything Sniprun ran so far (and has not finished yet):

```vim
 :SnipTerminate
```

Alternatively, exit Neovim.

### My usage recommandation

- Map the line mode to a simple command such as `ff`
- Rename `SnipRun` to a more convenient command that do not conflict with your existing mappings, to run bloc mode faster as is probably the most widely used mode while still having easily implemented support for multiples languages

## Support levels and languages

As of writing, languages can be supported up to different extents:

- Unsupported : You should not expect anything to work.
- Line : Code contained in a signle line works, for example: `print([x**2 for x in range(10)])` . Won't work if you use a variable defined elsewhere.
- Bloc : You can select any piece of code that is correct on its own (indepenently of indentation) in visual mode, and run it.
- Import : Support external imports, so you don't have to select the top-of-file import to test 'bloc-mode-style' a code selection somewhere else.
- File : Sniprun will recursively find the missing variable and function definitions to run your line of code(you don't have to select a bloc anymore).
- Project : Sniprun will detect the root of your project, and get the necessary code from files in your project.
- System : Sniprun will use local (and system) libraries, such as jar files, to run your what you want.

| Language   | Support level |
| ---------- | ------------- |
| Python3    | Bloc          |
| Rust       | Unsupported   |
| C          | Unsupported   |
| Java       | Unsupported   |
| JavaScript | Unsupported   |

## Known limitations

Due to its nature, Sniprun may have trouble with programs that :

- Meddle with standart output / stderr
- Prints double quotes (")
- Purposely fails
- Access files; sniprun does not run in a virtual environment.