[![Build Status](https://travis-ci.com/dandavison/delta.svg?branch=master)](https://travis-ci.com/dandavison/delta)

## A syntax-highlighting pager for git

<table>
  <tr>
    <td>
      <img width=500px style="border: 1px solid black"
           src="https://user-images.githubusercontent.com/52205/61316245-8fd95f80-a7ce-11e9-9a26-607eefbeed45.png"
           alt="image" />
    </td>
    <td>
      <img width=500px style="border: 1px solid black"
           src="https://user-images.githubusercontent.com/52205/61316175-602a5780-a7ce-11e9-87a6-05ffa09c7475.png"
           alt="image" />
    </td>
  </tr>
  <tr>
    <td>
      delta --dark (default)
    </td>
    <td>
      delta --light
    </td>
  </tr>
</table>

<br>

## Installation

Executables: [Linux](https://github.com/dandavison/delta/releases/download/0.0.5/delta-0.0.5-x86_64-unknown-linux-musl.tar.gz) | [MacOS](https://github.com/dandavison/delta/releases/download/0.0.5/delta-0.0.5-x86_64-apple-darwin.tar.gz) | [Windows](https://github.com/dandavison/delta/releases/download/0.0.5/delta-0.0.5-x86_64-pc-windows-msvc.zip)

Homebrew:
```sh
brew tap dandavison/delta https://github.com/dandavison/delta
brew install dandavison/delta/git-delta
```

All available executables: https://github.com/dandavison/delta/releases

<br>

## Configure git to use delta

```sh
git config --global core.pager "delta --dark"  # --light for light terminal backgrounds
```

Alternatively, you can edit your `.gitconfig` directly. An example is
```
[core]
    pager = delta --plus-color="#012800" --minus-color="#340001" --theme="base16-ocean.dark"
```

All git commands that display diff output should now display syntax-highlighted output. For example:
  - `git diff`
  - `git show`
  - `git log -p`
  - `git stash show -p`


<br>

## Usage
```
USAGE:
    delta [FLAGS] [OPTIONS]

FLAGS:
        --compare-themes       Compare available syntax highlighting themes. To use this option, supply git diff output
                               to delta on standard input. For example: `git show --color=always | delta --compare-
                               themes`.
        --dark                 Use colors appropriate for a dark terminal background.  For more control, see --theme,
                               --plus-color, and --minus-color.
    -h, --help                 Prints help information
        --highlight-removed    Apply syntax highlighting to removed lines. The default is to apply syntax highlighting
                               to unchanged and new lines only.
        --light                Use colors appropriate for a light terminal background. For more control, see --theme,
                               --plus-color, and --minus-color.
        --list-languages       List supported languages and associated file extensions.
        --list-themes          List available syntax highlighting themes.
        --show-colors          Show the command-line arguments for the current colors.
    -V, --version              Prints version information

OPTIONS:
        --commit-style <commit_style>
            Formatting style for commit section of git output. Options are: plain, box. [default: plain]

        --file-style <file_style>
            Formatting style for file section of git output. Options are: plain, box, underline. [default: underline]

        --hunk-style <hunk_style>
            Formatting style for hunk section of git output. Options are: plain, box. [default: box]

        --max-line-distance <max_line_distance>
            The maximum distance between two lines for them to be inferred to be homologous. Homologous line pairs are
            highlighted according to the deletion and insertion operations transforming one into the other. [default:
            0.3]
        --minus-color <minus_color>                The background color (RGB hex) to use for removed lines.
        --minus-emph-color <minus_emph_color>
            The background color (RGB hex) to use for emphasized sections of removed lines.

        --plus-color <plus_color>                  The background color (RGB hex) to use for added lines.
        --plus-emph-color <plus_emph_color>
            The background color (RGB hex) to use for emphasized sections of added lines.

        --theme <theme>                            The syntax highlighting theme to use.
    -w, --width <width>
            The width (in characters) of the background color highlighting. By default, the width is the current
            terminal width. Use --width=variable to apply background colors to the end of each line, without right
            padding to equal width.
```

<br>

## 24 bit color

  delta works best if your terminal application supports 24 bit colors. See https://gist.github.com/XVilka/8346728. For example, on MacOS, iTerm2 works but Terminal.app does not.

  If you're using tmux, it's worth checking that 24 bit color is  working correctly. For example, run a color test script like [this  one](https://gist.githubusercontent.com/lifepillar/09a44b8cf0f9397465614e622979107f/raw/24-bit-color.sh),  or one of the others listed [here](https://gist.github.com/XVilka/8346728). If  you do not see smooth color gradients, see the discussion at  [tmux#696](https://github.com/tmux/tmux/issues/696). The short  version is you need something like this in your `~/.tmux.conf`:
  ```
  set -ga terminal-overrides ",xterm-256color:Tc"
  ```
  and you may then  need to quit tmux completely for it to take effect.

<br>

## Credit
  https://github.com/trishume/syntect<br>
  https://github.com/sharkdp/bat<br>
  https://github.com/so-fancy/diff-so-fancy
