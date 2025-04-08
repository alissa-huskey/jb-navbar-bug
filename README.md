sphinx-book-theme bug: navbar(start/center/end) ignored
=======================================================

[Issue #908](https://github.com/executablebooks/sphinx-book-theme/issues/908)

This reproduces a bug in [sphinx-book-theme](https://github.com/executablebooks/sphinx-book-theme/) in
which the `_config.yml` settings for `navbar_start`, `navbar_center` and `navbar_end` (as per
[the docs](https://sphinx-book-theme.readthedocs.io/en/stable/sections/header.html)) are ignored.

Steps to Reproduce
------------------

### From this repo

1. Clone repo: `git clone https://github.com/alissa-huskey/jb-navbar-bug.git && cd jb-navbar-bug`
2. Install: `poetry install`
3. Start a poetry shell: `poetry shell`
4. (Optional) Build book: `jb build --all docs`
5. Start a html server: `python -m http.server --directory docs/_build/html 1313`
6. Go to URL `http://localhost:1313/`
7. Look for `My test button`
8. (Just to be sure.) In a Javascript console: `$(".mybutton")`

### From Scratch

 1. Create new python project: `poetry create NAME && cd NAME`
 2. Start a poetry shell: `poetry shell`
 3. Install `jupyter-book`: `poetry add jupyter-book`
 4. Initialize: `jb create docs`
 5. Create `_templates directory`: `mkdir docs/_templates`
 6. Add `mybutton.html` to `docs/_templates/`:
 
    ```html
    <button class="mybutton">My test button</button>
    ```
 7. Add `templates_path` to `docs/_config.py`:
 
    ```yml
    sphinx:
      config:
        templates_path: ["_templates"]
    ```
 8. Add `navbar_end` to `docs/_config.py`:
 
    ```yml
    html_theme_options:
      navbar_end: ["mybutton.html"]
    ```
 9. Build the book: `jb build --all docs`
10. Start a html server: `python -m http.server --directory docs/_build/html 1313`
11. Go to URL `http://localhost:1313/`
12. Look for `My test button`
13. (Just to be sure.) In a Javascript console: `$(".mybutton")`
