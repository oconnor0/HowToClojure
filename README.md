# HowToClojure
Notes on how I develop Clojure and ClojureScript

## Install Clojure and ClojureScript

1. Install Java, Clojure, and ClojureScript

    ```
    scoop bucket add java
    scoop install adoptopenjdk-lts-hotspot
    scoop bucket add scoop-clojure https://github.com/littleli/scoop-clojure
    scoop install clojure
    ```

## Configure Sublime Text

### Enable linting

1. Install clj-kondo.

    ```
    scoop bucket add scoop-clojure https://github.com/littleli/scoop-clojure
    scoop install clj-kondo
    ```

2. Ctrl-Shift-P, Install Package, SublimeLinter.
3. Ctrl-Shift-P, Install Package, SublimeLinter-contrib-clj-kondo.
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

1. Install Zeal, zeal-user-contrib, and the ClojureScript docset.

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
