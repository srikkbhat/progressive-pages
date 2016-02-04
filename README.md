_[Demo and API docs](https://srikkbhat.github.io/progressive-pages)_

##&lt;progressive-pages&gt;

`progressive-pages` is used to select one of its children to show. One use is to cycle through a list of
children "pages". It attempts to import the selected element using path attribute if provided.

Example:

```html
  <progressive-pages selected="0">
    <my-page-one path$="path/to/my-page-one.html"></my-page-one>
    <my-page-two path$="path/to/my-page-two.html"></my-page-two>
    <my-page-three path$="path/to/my-page-three.html"></my-page-three>
  </progressive-pages>

  <script>
    document.addEventListener('click', function(e) {
      var pages = document.querySelector('progressive-pages');
      pages.selectNext();
    });
  </script>
```


##ProgressivePages.PageBehavior

Use `ProgressivePages.PageBehavior` to implement a page to be lazy loaded by `progressive-pages`.
It also provides access to a functions `_onPageEntry` and `_onPageExit` which can be used to write custom code that will run when the page is selected and deselected.

Example:
```html
        <dom-module id="my-page-one">
          <template>
            <style>
              :host {
                display: block;
              }
            </style>

            <p>Page one</p>
          </template>
          <script>
            (function() {
              Polymer({

                is: 'my-page-one',

                behaviors: [
                  ProgressivePages.PageBehavior
                ],

                _onPageEntry: function() {
                  //The code written here will run when the page is selected.
                },

                _onPageExit: function() {
                  //The code written here will run when the page is deselected.
                }
              });
            })();
          </script>
        </dom-module>
```
