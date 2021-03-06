This jQuery plugin is for easily finding the starting and ending positions of
selected text in text fields and textareas. It can also be used to set the
selection, and replace the selection with given text (or insert text wherever
the cursor is in the text field or textarea).

* jquery-textrange may not work with WYSIWYG editors. See [issue
  #3](https://github.com/dwieeb/jquery-textrange/issues/3) and [this
  question](https://wordpress.stackexchange.com/questions/105961/insert-text-a-cursor-position-in-to-tinymce-text-editor).

## Demo

* https://dwieeb.github.com/jquery-textrange/

## Browser Support

* Chrome
* Firefox
* Microsoft Edge
* *yes, even* Internet Explorer 5.5+

## Include

Include the file directly using `<script>` tags:

```html
<script src="https://code.jquery.com/jquery-latest.min.js"></script>
<script src="jquery-plugins/jquery-textrange.js"></script>
```

:memo: *note*: jquery-textrange can be loaded through any
[UMD](https://github.com/umdjs/umd/blob/master/README.md)-compatible Javascript
Module Loader.

## Methods

You can use this method to get all the information on the selected text of an
element or a specific bit of information.

### 'get'

##### Get everything

```javascript
$('input[name="example"]').textrange('get');
```

or for short:

```javascript
$('input[name="example"]').textrange();
```

This will return a JSON object with the following information:

```javascript
{
   "position": // cursor location in the text field)
   "start": //starting position of the selected text in the text field
   "end": // ending position of the selected text in the text field
   "length": // the length of the selected text in the text field
   "text": // the text that is selected
}
```

##### Get a particular property

This function can also be used to get a particular property of the object.

For example, this will obtain the starting location of the selected text:

```javascript
var start = $('input[name="example"]').textrange('get', 'start');
```

### 'set'

You can use this method to set the starting and ending locations of the
selected text in an element.

It works much like [PHP's
substr()](https://secure.php.net/manual/en/function.substr.php), so if you're
familiar with that, it should be a breeze! Here are some examples, anyway.

For the following examples, let's say `input[name="example"]` contains the text
`abcdef`.

```javascript
$('input[name="example"]').textrange('set'); // selects "abcdef" (select all)
$('input[name="example"]').textrange('set', 2); // selects "cdef"
$('input[name="example"]').textrange('set', 2, 3); // selects "cde"
$('input[name="example"]').textrange('set', 2, -2); // selects "cd"
$('input[name="example"]').textrange('set', -3); // selects "def"
$('input[name="example"]').textrange('set', -2, 1); // selects "e"
$('input[name="example"]').textrange('set', -4, -1); // selects "cde"
```

If you're looking to set the cursor at one specific location, you can use `0`
for length, or you can use `$().textrange('setcursor')` (see below).

### 'setcursor'

You can use this method to set the location of the cursor in your text field.

To set the cursor at the fifth character position:

```javascript
$('input[name="example"]').textrange('setcursor', 5);
```

### 'replace'

You can use this method to replace the selection with given text.

```javascript
$('input[name="example"]').textrange('replace', 'some text');
```

There is also an `insert` alias for `replace` if you're using this method to
insert text at the cursor location. They work the same way.

## Options

For the first parameter of each method, you can pass an object instead of a
string with additional options:

```javascript
$('input[name="example"]').textrange({ method: 'get' });
$('input[name="example"]').textrange({ method: 'set', nofocus: true }, 2);
$('input[name="example"]').textrange({ method: 'get', nofocus: true }, 'start');
```

* `method` (defaults to `'get'`): One of the methods above.
* `nofocus`: Do not call `.focus()` on the dom element. See [PR
  #20](https://github.com/dwieeb/jquery-textrange/pull/20).
