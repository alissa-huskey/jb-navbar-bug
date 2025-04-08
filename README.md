navbar(start/center/end) ignored
================================

This reproduces a bug in [sphinx-book-theme](https://github.com/executablebooks/sphinx-book-theme/) in
which the `_config.yml` settings for `navbar_start`, `navbar_center` and `navbar_end` (as per
[Header and navbar](https://sphinx-book-theme.readthedocs.io/en/stable/sections/header.html)) are ignored.

Steps to Reproduce
------------------

 1. Create new python project: `poetry create NAME`
 2. Install `jupyter-book`: `poetry add jupyter-book`
 2. Initialize: `jb create docs`
 3. Create `_templates directory`: `mkdir docs/_templates`
 4. Add `mybutton.html` to `docs/_templates/`:
 
    ```html
    <button class="mybutton">My test button</button>
    ```
 5. Add `templates_path` to `docs/_config.py`:
 
    ```yml
    sphinx:
      config:
        templates_path: ["_templates"]
    ```
 6. Add `navbar_end` to `docs/_config.py`:
 
    ```yml
    html_theme_options:
      navbar_end: ["mybutton.html"]
    ```
 7. Build the book: `jb build docs`
 8. Start a html server: `python -m http.server --directory docs/_build/html 1313`
 9. Go to URL `http://localhost:1313/`
10. Look for `My test button`
11. (Just to be sure.) In a Javascript console: `$(".mybutton")`
