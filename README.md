# HowToClojure

Notes on how I develop Clojure and ClojureScript inspired by https://github.com/PetrKryslUCSD/HowToUseJuliaWithSublimeText3

## Install Scoop and Git

1. In PowerShell, install Scoop.

    ```powershell
    Set-ExecutionPolicy RemoteSigned -scope CurrentUser
    iwr -useb get.scoop.sh | iex
    ```
    
2. Install Git:

    ```powershell
    scoop install git
    ```
    
3. Always rebase on pull: `git config --global pull.rebase true`
    
4. Add other Scoop buckets:

    ```powershell
    scoop bucket add java
    scoop bucket add extras
    scoop bucket add scoop-clojure https://github.com/littleli/scoop-clojure
    ```
    
    The installation of these buckets will be duplicated below to document where various tools come from.

## Remap Caps Lock to Alt

1. Install [SharpKeys].

    ```powershell
    scoop bucket add extras
    scoop install sharpkeys
    ```
    
2. Remap `Special: Caps Lock (00_3A)` to `Special: Left Alt (00_38)`.

[SharpKeys]: https://github.com/randyrants/sharpkeys

## Install Clojure and ClojureScript

1. Install Java, Clojure, and ClojureScript

    ```
    scoop bucket add java
    scoop install adoptopenjdk-lts-hotspot
    scoop bucket add scoop-clojure https://github.com/littleli/scoop-clojure
    scoop install clojure
    ```
    
## Install and configure Sublime Merge

1. Either download the dev version from the [Sublime Discord](https://discord.gg/D43Pecu) or via Scoop:

    ```powershell
    scoop install extras
    scoop install sublime-merge
    ```

2. In Sublime Merge, Preferences > Edit Settings. Put the following in:

    ```json
    {
        "caret_style": "solid",
        "caret_extra_top": 4,
        "caret_extra_bottom": 4,
        "caret_extra_width": 1,
        "font_face": "Monoid",
        "font_size": 9,
    }
    ```

## Configure Sublime Text

1. Either download the dev version from the [Sublime Discord](https://discord.gg/D43Pecu) or via Scoop:

    ```powershell
    scoop install extras
    scoop install sublime-text
    ```
    
2. In Sublime Text, Preferences > Settings. Put the following in:

    ```json
    {
        "color_scheme": "Packages/Color Scheme - Default/Breakers.sublime-color-scheme",
        "font_face": "Monoid",
        "font_size": 9,
        "rulers":
        [
            80,
            100
        ],
        "draw_minimap_border": true,
        "always_show_minimap_viewport": true,
        "highlight_line": true,
        "match_brackets": false,
        "match_brackets_angle": false,
        "match_brackets_braces": false,
        "match_brackets_content": false,
        "match_brackets_square": false,
        "match_tags": false,
        "line_padding_bottom": 1,
        "line_padding_top": 1,
        "drag_text": false,
        // "translate_tabs_to_spaces": true,
        "theme": "Adaptive.sublime-theme",
        "scroll_speed": 0,
        "tree_animation_enabled": false,
        "animation_enabled": false,
        "bold_folder_labels": true,
        "overlay_scroll_bars": "disabled",
        "hardware_acceleration": "opengl",
        "ignored_packages":
        [
            "Clojure",
            "Vintage",
        ],        
    }
    ```
    
### Install BracketHighlighter

1. Ctrl-Shift-P, Install Package, [BracketHighlighter](https://packagecontrol.io/packages/BracketHighlighter).

### Enable linting

1. Install [clj-kondo](https://github.com/borkdude/clj-kondo).

    ```
    scoop bucket add scoop-clojure https://github.com/littleli/scoop-clojure
    scoop install clj-kondo
    ```

2. Ctrl-Shift-P, Install Package, [SublimeLinter](http://www.sublimelinter.com/en/stable/).
3. Ctrl-Shift-P, Install Package, [SublimeLinter-contrib-clj-kondo](https://github.com/ToxicFrog/SublimeLinter-contrib-clj-kondo/).
4. Preferences > Package Settings > Sublime Linter > Settings

    ```json
    {
        "styles": [
            {
                "mark_style": "stippled_underline",
                // "icon": "dot", // "circle",
                "types": ["warning"]
            },
            {
                "mark_style": "squiggly_underline",
                // "icon": "x",
                "types": ["error"],
            }
        ]
    }
    ```


### Enable F1 to open docs via Zeal.

1. Install [Zeal](https://zealdocs.org/https://zealdocs.org/), [zeal-user-contrib](https://github.com/jmerle/zeal-user-contrib), and the ClojureScript docset.

    ```
    $ scoop install zeal
    $ yarn global add zeal-user-contrib
    $ zeal-user-contrib -o $Home\scoop\apps\zeal\current\docsets\
    ... type in ClojureScript and press Enter
    ```

2. Open Zeal.
3. Tools > Docsets > Available.
4. Type Clojure and click Download.
5. Open Sublime Text.
6. Ctrl-Shift-P, Install Package, Zeal.
7. Preferences > Package Settings > Zeal.
8. Replace the settings with:

    ```json
    {
      // "zeal_command": "%USERPROFILE%\\scoop\\apps\\zeal\\current\\zeal.exe",
      "zeal_command": "c:\\users\\oconnor\\scoop\\apps\\zeal\\current\\zeal.exe",

      "language_mapping": {
        "HTML": {"lang": "html", "zeal_lang": "html"},
        "JavaScript": {"lang": "javascript", "zeal_lang": "javascript"},
        "CSS": {"lang": "css", "zeal_lang": "css"},
        "PHP": {"lang": "php", "zeal_lang": "php"},
        "Python": {"lang": "python", "zeal_lang": "python"},
        "Ruby": {"lang": "ruby", "zeal_lang":"ruby"},
        "Clojure": {"lang": "clojure", "zeal_lang": "clojure"},
        "ClojureScript": {"lang": "clojurescript", "zeal_lang": "cljs"},
      }
    }
    ```
    
### Switch to Clojures

1. Ctrl-Shift-P, Disable Package, Clojure.
2. Clone https://github.com/oconnor0/Clojures to "Sublime Text 3\Packages\". (Maybe just until https://github.com/sublimehq/Packages/pull/2355 is resolved?)
3. Except that Clojures does some things around syntax scopes so that Ctrl-Shift-Space better expands its scope.

## Limitations with the current Clojure syntax highlighting

1. The first initial colon in keywords is given `punctuation.definition.keyword.clojure`. A second colon in keywords is not given that scope and is treated differently. This also caused Expand Selection to Scope problems and that aspect can be "fixed" by https://github.com/oconnor0/Clojures/commit/ae1548affd0bf32bbde9035590f55995e0726f5b#diff-b2ba6bbcd236c06e9be213f5a0d06eb3L74

2. Other symbols in forms (besides the first, constants, keywords, etc.) are given no scope. Expand Selection to Scope when on one of those symbols just expands to the enclosing brackets instead of first selecting the current symbol. Giving them a scope resolves this: https://github.com/oconnor0/Clojures/commit/ae1548affd0bf32bbde9035590f55995e0726f5b#diff-b2ba6bbcd236c06e9be213f5a0d06eb3R105

3. `(comment ...)` forms are not supported.

4. `#_` does not affect highlighting; nor does it create a new scope for so that Expand Selection to Scope grabs it first.

5. When using Monoid `->` converts to an arrow, but `<-` does not. Fira Code does not have this problem.

6. Folding doesn't work on a `defn` with multiline arguments like

```clojure
(defn f [a
         b
         c
         d]
  (a)
  (b)
  (c)
  (d))
```

7. Zeal doesn't pass the entire `clj->js` to Zeal, but only passes `clj-js`.

8. Auto-completion doesn't include final `?` in symbol list.
