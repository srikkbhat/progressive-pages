_[Demo and API docs](https://srikkbhat.github.io/progressive-pages)_

##&lt;progressive-pages&gt;

`progressive-pages` is used to select one of its children to show. One use is to cycle through a list of
children "pages". It attempts to import the selected element using path attribute if provided.
It can also be used to stamp the element into the page only after successful import using combination of link
attribute and `dom-if`. See demo for more details. Try this with [progressive-vulcans](https://github.com/srikkbhat/progressive-vulcans), 
which can use used to create incremental vulcanized files.

Example:

```html
    <template is="dom-bind" id="app">
      <progressive-pages selected="{{selected}}" id="pages">
        <div path$="path/to/my-page-one.html" link$="3"></div>
        <div path$="path/to/my-page-two.html" link$="4"></div>
        <div path$="path/to/my-page-three.html" link$="5"></div>
        <template is="dom-if" if="{{_equal(selected, '3')}}">
          <my-page-one></my-page-one>
        </template>
        <template is="dom-if" if="{{_equal(selected, '4')}}">
          <my-page-two></my-page-two>
        </template>
        <template is="dom-if" if="{{_equal(selected, '5')}}">
          <my-page-three></my-page-three>
        </template>
      </progressive-pages>
    </template>

    <script>
      var app = document.querySelector('#app');
      var pages = app.$.pages;
      app._equal = function(a, b) {
        return a == b;
      };
      pages.select('0');
      app.addEventListener('click', function(e) {
        if (pages.selected == '2' ) {
          pages.select('0');
        } else {
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
