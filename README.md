# HTML5 Forms

| Objectives |
| :--- |
| Explore HTML Forms and Inputs |
| Understand the difference between a `method` and an `action` |
| Create forms that utilize parameters |

### An Example `<form>` Element (Tag)

```html
<form method="POST" action="/page">
  <input type="text" name="page_name" />
  <input type="submit" value="Create" />
</form>
```

#### Attributes

In the opening of the `<form>` tag you can see two attributes: `method` & `action`

- **method**: the HTTP verb (method) that the browser uses to submit the form.
- **action**: the path of the HTTP request page that processes the information submitted via the form.

>A `route` is simply a combination of a method & action. For example `GET '/page'` or `POST '/users'` are both valid routes.

>For now simply understand that it is convention for [GET](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.3) to be used in a request when the client wants to receive data, and for [POST](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.5) to be used in a request when the client wants to send data.

**Client / Server Model **

![client/server](https://mdn.mozillademos.org/files/4291/client-server.png)

## Common Inputs (Fun Toys!)

| Field Type | HTML Code | Widget (Control) | Notes |
|:-- |:-- |:-- |:-- |
| plain text | `<input type="text">` | ![<input type="text">][text] | the type attribute can be omitted |
| password field | `<input type="password">` | ![<input type="password">][text] | echoes dots instead of characters |
| text area | `<textarea></textarea>` | ![<textarea></textarea>][area] | a more customizable plain text area |
| checkbox | `<input type="checkbox">` | ![<input type="checkbox">][check] | can be toggled on or off |
| radio button | `<input type="radio">` | ![<input type="radio" name="group"> <input type="radio" name="group">][radio] | can be grouped with other inputs |
| drop-down lists | `<select><option>` | ![<select><option>Option 1</option><option>Option 2</option></select>][select] | [check here for more info](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select) |
| file picker | `<input type="file">` | ![<input type="file">][file] | pops up an “open file” dialog |
| hidden field | `<input type="hidden">` |  | nothing there!
| submit button | `<input type="submit">` | ![<input type="submit">][submit] | activates the form's submission <br/>(a `POST` request or <br/>Javascript action) |

<!-- Images -->
[text]:   https://raw.github.com/h4w5/html_form_cheatsheet_images/master/input-text.png
[area]:   https://raw.github.com/h4w5/html_form_cheatsheet_images/master/textarea.png
[check]:  https://raw.github.com/h4w5/html_form_cheatsheet_images/master/input-checkbox.png
[radio]:  https://raw.github.com/h4w5/html_form_cheatsheet_images/master/input-radio.png
[select]: https://raw.github.com/h4w5/html_form_cheatsheet_images/master/select-option.png
[file]:   https://raw.github.com/h4w5/html_form_cheatsheet_images/master/input-file.png
[submit]: https://raw.github.com/h4w5/html_form_cheatsheet_images/master/input-submit.png

### Important Attributes

All input types (including `<textarea>`s):

- **`type`**: the type of data that is being input (affects the "widget" that is used to display this
  element by the browser).
- **`name`**: the key used to describe this data in the HTTP request.
- **`id`**: the unique identifier that other HTML elements, JavaScript and CSS use to access this
  element in the browser.
- **`value`**: the default data that is assigned to the element.
- **`placeholder`**: not a default value, but a useful HTML5 addition of a data "prompt" for an input.
- **`autofocus`**: defaults the cursor to a specific input when the page originally loads. You can only have one autofocus on your page.
- **`disabled`**: a Boolean attribute indicating that the "widget" is not available for interaction.
- **`required`**: a Boolean attribute indicating that the field must have a value / cannot be left empty.

Radio buttons or checkboxes:

- **`checked`**: a Boolean that indicates whether the control is selected by default (is false unless).
- **`name`**: the group to which this element is connected. For radio buttons, only one element per
  group (or name) can be checked.
- **`value`**: the data or value that is returned for a specific group (a multi-element control), if
  this element is checked.

## Form Submission Demo
#### Round 1.

Given the following HTML...

``` html
<form>
    <input name="instrument" value="bongos"> <!-- Text Field -->
    <input type="submit">                   <!-- Submit Button -->
</form>
```

<details>
<summary>**What endpoint/action are we submitting to?** (Click Here)</summary>
<br>
We did not supply a form `action`. That means that it will default to the current endpoint. In otherwords, you will refresh the current page.
</details>

<details>
<summary>**What data will be submitted to the server?** (Click Here)</summary>
<br>
* **instrument**: "bongos"
</details>

<details>
<summary>**What will that data look like? How will it be formatted?** (Click Here)</summary>
<br>
`?instrument=bongos`
</details>


#### Round 2.

Given the following HTML...

``` html
<form action="https://musicbrainz.org/search" method="GET">
    <label for="artist">Search by Music Artist</label>
    <input id="artist" name="query" value="Adele">
    <input name="type" value="artist" hidden>
    <input type="submit">
</form>
```

<details>
<summary>**What endpoint/action are we submitting to?** (Click Here)</summary>
<br>
We are making a "GET" request to "https://musicbrainz.org/search".
</details>

<details>
<summary>**What data will be submitted to the server?** (Click Here)</summary>
<br>
* **artist**: "Adele"
* **type**: "artist"
</details>

<details>
<summary>**What will that data look like? How will it be formatted?** (Click Here)</summary>
<br>
It will be in the form of a query parameter: `?query=adele&type=artist`
</details>

## Form Submission & jQuery
> **Important**: You do not need jQuery to submit a form. You do not need jQuery to submit a form. You do not need jQuery to submit a form.

Sometimes we want to submit a form, in the background, without ever refreshing the page. This is a common pattern in modern "single page applications". How do you submit form data *in the background*?

When a form is submitted it triggers the `submit` event. We can listen to this event using jQuery.

``` javascript
$("form").on("submit", function(event){
    alert("See you later! You're submitting a form!")
})
```

In order to **stop** the form from submitting, we have to prevent it's *default* behavior.

``` javascript
$("form").on("submit", function(event){
    event.preventDefault(); // Stops the form from submitting!
    alert("You're not going anywhere! (You prevented the form from submitting).")
})
```

If we want to grab a value from our form, we can use jQuery's [`val` method](http://api.jquery.com/val/).

``` javascript
$("input#artist").val(); // "Adele"
$("input[name=query]").val(); // "Adele"
$("input#artist").attr("name"); // "query"
```

> **Note**: jQuerys `text` method will not work on inputs!

If we want to grab **all** of the data (name/value pairs) in the form, we can use jQuery's [`serialize` method](http://api.jquery.com/serialize/).

``` javascript
$("form").serialize(); // e.g. "?query=Adele&type=artist"
```

Generally we will do this when the user clicks "submit", in combination with a `submit` listener and `preventDefault`, then we will use `ajax` to submit the form in the background (without ever refreshing the page!)

``` javascript
$("form").on("submit", function(event){
    event.preventDefault(); // Stops the form from submitting!
    var form_data = $(this).serialize();
    // ... verify the user didn't miss anything
    // ... add a spinner wheel to the page
    // ... send the form_data to the server using AJAX
    // ... wait for a response
})
```

> **Reminder**: You do not need jQuery to submit a form. We use jQuery to *stop* a form from submitting, and to *manually* submit data ourselves, with the goal of never causing the page to refresh.


## Good Looking Forms
#### The `<label>` Element (Tag)
We encourage you to always use the optional `<label>` tag with each of your form inputs.

    "This is the most important element if you want to build accessible forms." *— MDN*

There are two ways to use labels correctly:

```html
<!-- Simple (nested) label example -->
<label>Username
  <input type="text" name="username" />
</label>

<!-- Using the "for" attribute with the input's id -->
<!-- This is the preferred method if you are using Bootstrap -->
<label for="password">Username</label>
<input id="password" type="text" name="password" />
```

> Make sure the label's `for` attribute matches the input's `id` attribute!

#### Bootstrap Forms
Out of the box, unstyled HTML5 `inputs` look *terrible*.

Bootstrap to the rescue!

``` html
<form>
    <div class="form-group">
        <label for="exampleInput">Example Bootstrap Input</label>
        <input type="text" class="form-control" id="exampleInput">
    </div>
    <button type="submit" class="btn btn-default">Submit</button>
</form>
```

Note that the `form-group` class is meant to "group" together `label`/`input` pairs (and give them more vertical whitespace / breathing room). Also note that each `input` element receives a `form-control` class.

For super good looking forms, you'll need to dig into the docs: [Bootstrap Forms](https://getbootstrap.com/css/)


## Common Validations

Form validations help to prevent users from submitting bad data to the server:

* a missing or empty field (required)
* an email address that was missing an "@" symbol (wrong format)
* a password that is obiously too short (wrong length)

#### `required` attribute

Try submitting the below form without entering your name:

```html
<form>
  <label for="colorField">What is your favorite color?</label>
  <input id="colorField" name="favColor" required>
  <button>Submit</button>
</form>
```
Notice the `required` attribute on the input. Therefore, the form will not submit until some information is entered into the field.

#### `pattern` attribute

```html
<form>
  <label for="kindOfBob">Do you go by bob or bobert?</label>
  <input id="kindOfBob" name="bobType" pattern="bob|bobert" required>
  <button>Submit</button>
</form>
```

The `pattern` attribute allows us to specify the values we will accept. In this case only `bob` or `bobert` are acceptable.

#### `length` attribute

You may need the user to enter a specific amount of characters. Let's say you need a username to be at least 6 characters. You can use the `minlength` or `maxlength` attributes to help.

```html
<form>
  <label for="password">What's your password?</label>
  <input id="password" type="password" name="password" minlength="8" required>
  <button>Submit</button>
</form>
```


##Further Reading (optional)

MDN has a number of exhaustive resources on HTML forms and inputs. It can be a lot to absorb, so look for patterns and try to grasp the big picture.

* [HTML Form Reference](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms) is a great resource and has been distilled below.
* [HTML Input Reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)
* [Native Form Widgets](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/The_native_form_widgets)
* [Form Validation](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/Data_form_validation).
