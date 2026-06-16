# API Reference Combined

jTable ka complete reference — General Options, Field Options, Actions, Methods, Events, aur Localization sab ek jagah.

---

## General Options

General options control the overall behavior of a jTable instance.

---

### How to Set General Options

### Per-instance

Set options directly in the jTable initialization call:

```javascript
$(document).ready(function () {
    $('#MyTableContainer').jtable({
        columnResizable: false, // disable column resizing
        // other options...
    });
});
```

### For all instances

Set options on the jTable prototype right after importing the script file:

```javascript
// Single option
$.hik.jtable.prototype.options.columnResizable = false;

// Multiple options at once
$.extend(true, $.hik.jtable.prototype.options, {
    columnResizable: false,
    animationsEnabled: false,
    ajaxSettings: {
        type: 'GET'
    }
});
```

> **Note:** Per-instance settings always override prototype-level defaults.

---

### Option Reference

### addRecordButton

| | |
|---|---|
| **Type** | jQuery object |
| **Default** | auto-generated link |

A jQuery object to use instead of the default `+ add new record` link. Assign any page element to open the "add new record" dialog when clicked.

---

### ajaxSettings

| | |
|---|---|
| **Type** | object |
| **Default** | `{ type: 'POST', dataType: 'json' }` |

Default settings for every AJAX request jTable makes. Accepts all options from jQuery's [`$.ajax()`](http://api.jquery.com/jQuery.ajax/). This setting is merged (not replaced), so you only need to specify the values you want to change:

```javascript
ajaxSettings: { type: 'GET' }
```

---

### animationsEnabled

| | |
|---|---|
| **Type** | boolean |
| **Default** | `true` |

When `true`, jTable shows animations when a row is created, updated, or deleted.

---

### columnResizable

| | |
|---|---|
| **Type** | boolean |
| **Default** | `true` |

When `true`, users can resize data columns by dragging the column borders.

---

### columnSelectable

| | |
|---|---|
| **Type** | boolean |
| **Default** | `true` |

When `true`, users can show or hide columns by right-clicking the table header.

---

### defaultDateFormat

| | |
|---|---|
| **Type** | string |
| **Default** | `'yy-mm-dd'` |

Default format for date fields. See [jQuery UI datepicker format strings](http://docs.jquery.com/UI/Datepicker/formatDate).

---

### defaultSorting

| | |
|---|---|
| **Type** | string |
| **Default** | none |

Default sort order when the table first loads. Specify a field name followed by `ASC` or `DESC`, e.g. `'Name ASC'` or `'Name DESC'`.

---

### deleteConfirmation

| | |
|---|---|
| **Type** | boolean or function |
| **Default** | `true` |

Controls the delete-confirmation behaviour.

- **boolean** — when `true` a confirmation dialog is shown before deletion.
- **function** — receives a `data` argument and can fully customise the confirmation flow:

```javascript
deleteConfirmation: function(data) {
    data.deleteConfirmMessage = 'Are you sure you want to delete ' + data.record.Name + '?';
}
```

`data` properties:

| Property | Description |
|---|---|
| `data.row` | jQuery selection of the row being deleted. |
| `data.record` | The record object (e.g. `data.record.Name`). |
| `data.cancel` | Set to `true` to cancel deletion (default: `false`). |
| `data.cancelMessage` | Optional message to show when deletion is cancelled. |
| `data.deleteConfirm` | Whether to show a confirmation dialog (default: `true`). |
| `data.deleteConfirmMessage` | Custom confirmation message text. |

---

### dialogShowEffect

| | |
|---|---|
| **Type** | string |
| **Default** | `'fade'` |

jQuery UI effect used when **opening** a dialog. Options include `'blind'`, `'bounce'`, `'clip'`, `'drop'`, `'explode'`, `'fold'`, `'highlight'`, `'puff'`, `'pulsate'`, `'scale'`, `'shake'`, `'size'`, `'slide'`, and more. See the [jQuery UI effect docs](http://www.jqueryui.com/demos/effect).

---

### dialogHideEffect

| | |
|---|---|
| **Type** | string |
| **Default** | `'fade'` |

jQuery UI effect used when **closing** a dialog. Accepts the same values as `dialogShowEffect`.

---

### gotoPageArea

| | |
|---|---|
| **Type** | string |
| **Default** | `'combobox'` |

Controls the "go to page" input when paging is enabled.

| Value | Description |
|---|---|
| `'combobox'` | A dropdown listing all pages. |
| `'textbox'` | A free-text input. |
| `'none'` | No "go to page" control. |

---

### jqueryuiTheme

| | |
|---|---|
| **Type** | boolean |
| **Default** | `false` |

When `true`, jTable adopts the colors and styles of the active jQuery UI theme instead of its own built-in themes. Include the required CSS files:

```html
<!-- jQuery UI theme -->
<link href="/Scripts/jqueryUi/themes/redmond/jquery-ui-1.10.1.custom.min.css" rel="stylesheet" />
<!-- jTable jQuery UI adapter -->
<link href="/Scripts/jtable/themes/jqueryui/jtable_jqueryui.css" rel="stylesheet" />
```

Use the [jQuery UI ThemeRoller](http://jqueryui.com/themeroller/) to build a custom theme.

---

### loadingAnimationDelay

| | |
|---|---|
| **Type** | int (milliseconds) |
| **Default** | `500` |

How long jTable waits before showing the "loading…" animation. If the AJAX request finishes before this delay, the animation never appears. Set to `0` to disable the delay entirely.

---

### messages

| | |
|---|---|
| **Type** | object |
| **Default** | See [Localization](./07-localization.md) |

Used to localise all UI strings. See the [Localization](./07-localization.md) reference for the full list of keys.

---

### multiselect

| | |
|---|---|
| **Type** | boolean |
| **Default** | `false` |

When `true`, users can select multiple rows simultaneously.

---

### multiSorting

| | |
|---|---|
| **Type** | boolean |
| **Default** | `false` |

When `true`, users can sort by multiple columns by holding **Ctrl** while clicking column headers. Multiple sort criteria are sent to the server as a comma-separated string, e.g. `'Name DESC,BirthDay ASC'`.

---

### openChildAsAccordion

| | |
|---|---|
| **Type** | boolean |
| **Default** | `false` |

When `true`, opening a child table automatically closes any other currently open child tables (accordion behaviour).

---

### paging

| | |
|---|---|
| **Type** | boolean |
| **Default** | `false` |

When `true`, jTable sends paging parameters (`jtStartIndex`, `jtPageSize`) to the server and expects a `TotalRecordCount` in the response. See [listAction](./04-actions.md#listaction) for details.

---

### pageList

| | |
|---|---|
| **Type** | string |
| **Default** | `'normal'` |

Style of the page-number list when paging is enabled.

| Value | Description |
|---|---|
| `'minimal'` | First, previous, next, and last links only. |
| `'normal'` | Page numbers plus the minimal controls. |

---

### pageSize

| | |
|---|---|
| **Type** | number |
| **Default** | `10` |

Number of rows per page when paging is enabled. Can be changed at runtime:

```javascript
$('#MyTableContainer').jtable('option', 'pageSize', 20);
```

---

### pageSizes

| | |
|---|---|
| **Type** | array of numbers |
| **Default** | `[10, 25, 50, 100, 250, 500]` |

The choices shown in the "page size" dropdown when paging is enabled.

---

### pageSizeChangeArea

| | |
|---|---|
| **Type** | boolean |
| **Default** | `true` |

When `false`, the "page size" dropdown is hidden even when paging is enabled.

---

### saveUserPreferences

| | |
|---|---|
| **Type** | boolean |
| **Default** | `true` |

When `true`, jTable saves and restores user preferences such as column widths. Preferences are keyed on a hash derived from [`tableId`](#tableid), all column names, and the total column count — changing any of these resets saved preferences.

---

### selecting

| | |
|---|---|
| **Type** | boolean |
| **Default** | `false` |

When `true`, users can select rows in the table.

---

### selectingCheckboxes

| | |
|---|---|
| **Type** | boolean |
| **Default** | `false` |

When `true`, a checkbox column is added to allow row selection.

---

### selectOnRowClick

| | |
|---|---|
| **Type** | boolean |
| **Default** | `true` |

When `true`, clicking anywhere on a row selects it. Set to `false` if you want selection to happen only via the checkbox (see [`selectingCheckboxes`](#selectingcheckboxes)).

---

### showCloseButton

| | |
|---|---|
| **Type** | boolean |
| **Default** | `false` |

When `true`, a close button is displayed on the table. Clicking it raises the [`closeRequested`](./06-events.md#closerequested) event. Used internally by jTable for child tables.

---

### sorting

| | |
|---|---|
| **Type** | boolean |
| **Default** | `false` |

When `true`, users can sort the table by clicking column headers.

---

### tableId

| | |
|---|---|
| **Type** | string |
| **Default** | none |

A unique identifier for this table instance. Used for saving/restoring user preferences and set as the HTML `id` of the `<table>` element. Optional.

---

### title

| | |
|---|---|
| **Type** | string |
| **Default** | none |

Text shown at the top of the table. If omitted, the title area is not rendered at all.

---

### toolbar

| | |
|---|---|
| **Type** | object |
| **Default** | none |

Controls the jTable toolbar and its items. By default the toolbar contains only the "Add new record" button (when `createAction` is defined). Use this option to add custom buttons.

**Default shape:**

```javascript
toolbar: {
    hoverAnimation: true,         // Enable hover animation on toolbar items
    hoverAnimationDuration: 60,   // Duration of hover animation (ms)
    hoverAnimationEasing: undefined, // Easing; uses jQuery default if undefined
    items: []                     // Custom toolbar item definitions
}
```

**Adding custom toolbar items:**

```javascript
toolbar: {
    items: [
        {
            icon: '/images/excel.png',
            text: 'Export to Excel',
            click: function () {
                // your custom logic
            }
        },
        {
            icon: '/images/pdf.png',
            text: 'Export to PDF',
            click: function () {
                // your custom logic
            }
        }
    ]
}
```

Each item must define at least `icon` or `text`. Additional per-item options:

| Option | Description |
|---|---|
| `cssClass` | Extra CSS classes to apply to the toolbar item element. |
| `tooltip` | Sets the HTML `title` attribute (tooltip text). |

---

### unAuthorizedRequestRedirectUrl

| | |
|---|---|
| **Type** | string |
| **Default** | none |

A URL to redirect to when an AJAX request returns `UnAuthorizedRequest: true` or HTTP 401. If not set, jTable reloads the current page on an unauthorised response.

---

## Field Options

A field definition describes the structure and behaviour of a single record field. Fields are declared inside the `fields` object of the jTable initialization options:

```javascript
fields: {
    FieldName: {
        // field options
    }
}
```

---

### Option Reference

### columnResizable

| | |
|---|---|
| **Type** | boolean |
| **Default** | `true` |

Whether this specific column can be resized by the user. The table-level [`columnResizable`](./02-general-options.md#columnresizable) option must also be `true` (its default) for resizing to work.

---

### create

| | |
|---|---|
| **Type** | boolean |
| **Default** | `true` (`false` for key fields) |

Whether this field appears in the **Create Record** form.

---

### edit

| | |
|---|---|
| **Type** | boolean |
| **Default** | `true` (`false` for key fields) |

Whether this field appears in the **Edit Record** form.

---

### defaultValue

| | |
|---|---|
| **Type** | string |
| **Default** | none |

A default value pre-filled when the create form opens. Must be a valid value for the field type — for option lists it must match one of the defined option values.

---

### dependsOn

| | |
|---|---|
| **Type** | string or array |
| **Default** | none |

Creates **cascading dropdowns**. When the parent field's value changes, jTable automatically refreshes this field's option list.

```javascript
CountryId: {
    title: 'Country',
    options: 'Demo/GetCountryOptions',
    list: false
},
CityId: {
    title: 'City',
    dependsOn: 'CountryId',
    options: function (data) {
        if (data.source == 'list') {
            return 'Demo/GetCityOptions?countryId=0'; // all cities for table display
        }
        return 'Demo/GetCityOptions?countryId=' + data.dependedValues.CountryId;
    }
}
```

To depend on multiple fields, pass a comma-separated string or an array:

```javascript
dependsOn: 'ContinentId,CountryId'
// or
dependsOn: ['ContinentId', 'CountryId']
```

---

### display

| | |
|---|---|
| **Type** | function |
| **Default** | none |

A function that returns fully custom content for the table cell. The return value can be a string, HTML markup, or a jQuery object.

```javascript
TestColumn: {
    title: 'Test',
    display: function (data) {
        return '<b>' + data.record.Name + '</b>';
    }
}
```

`data.record` gives access to all fields of the current row's record. Common uses include calculated columns, action links, and opening child tables.

---

### input

| | |
|---|---|
| **Type** | function |
| **Default** | none |

A function that returns a fully custom input element for the create/edit forms.

```javascript
Name: {
    title: 'Name',
    width: '20%',
    input: function (data) {
        var value = data.record ? data.record.Name : 'enter your name here';
        return '<input type="text" name="Name" style="width:200px" value="' + value + '" />';
    }
}
```

`data` properties:

| Property | Description |
|---|---|
| `data.formType` | `'create'` or `'edit'`. |
| `data.form` | jQuery reference to the form element. |
| `data.record` | The record being edited (`undefined` for create forms). |
| `data.value` | Current field value (default value for create, current value for edit). |

> Always set the `name` attribute on custom inputs to ensure the value is posted to the server.

---

### inputClass

| | |
|---|---|
| **Type** | string |
| **Default** | none |

CSS class(es) added to this field's input element in the create/edit forms. Useful for integrating validation plugins.

---

### inputTitle

| | |
|---|---|
| **Type** | string |
| **Default** | same as `title` |

A label shown next to this field in the create/edit forms, when it should differ from the column header.

---

### key

| | |
|---|---|
| **Type** | boolean |
| **Default** | `false` |

Marks this field as the primary key. Every record must have exactly one key field. Key fields default to `create: false` and `edit: false`.

When a key field has `edit: true`, the original key value is posted to the server as `jtRecordKey` alongside the updated value.

---

### list

| | |
|---|---|
| **Type** | boolean |
| **Default** | `true` |

Whether this field is rendered as a column in the table.

---

### listClass

| | |
|---|---|
| **Type** | string |
| **Default** | none |

CSS class(es) applied to the `<td>` element for this field in every table row.

---

### options

| | |
|---|---|
| **Type** | object, array, URL string, or function |
| **Default** | none |

The option list source for dropdown (combobox) or radio-button fields. Four formats are supported:

#### Object

Property names are values; property values are display texts.

```javascript
PhoneType: {
    title: 'Phone type',
    options: { '1': 'Home phone', '2': 'Office phone', '3': 'Cell phone' }
}
```

#### Array

```javascript
// Objects with Value / DisplayText properties
options: [{ Value: '1', DisplayText: 'Home phone' }, { Value: '2', DisplayText: 'Office phone' }]

// Simple strings when value equals display text
options: ['1', '2', '3', '4']
```

#### URL string

jTable downloads the options from the URL. The server must return:

```json
{
  "Result": "OK",
  "Options": [
    { "DisplayText": "Home phone", "Value": "1" },
    { "DisplayText": "Office phone", "Value": "2" }
  ]
}
```

`Result` is `"OK"` or `"ERROR"`. On error, include a `"Message"` property.

#### Function

Returns an object, array, or URL string dynamically:

```javascript
options: function (data) {
    if (data.source == 'list') {
        return '/Demo/GetPhoneTypes?UserType=0'; // use a single URL for table listing
    }
    return '/Demo/GetPhoneTypes?UserType=' + data.record.UserType;
}
```

`data` properties:

| Property | Description |
|---|---|
| `data.source` | `'list'`, `'create'`, or `'edit'` — why the function was called. |
| `data.clearCache()` | Clears the cached options for the current URL. |
| `data.form` | jQuery reference to the form (valid when `source` is `'create'` or `'edit'`). |
| `data.record` | The current record (valid when `source` is `'list'` or `'edit'`). |
| `data.dependedValues` | Current values of fields listed in `dependsOn`. |

> **Performance tip:** jTable caches option lists by URL. For table listing (`data.source == 'list'`), return a single URL covering all possible values; return filtered URLs only in create/edit forms.

---

### optionsSorting

| | |
|---|---|
| **Type** | string |
| **Default** | none (preserves insertion order) |

Automatically sort the option list. Possible values:

| Value | Description |
|---|---|
| `'value'` | Ascending by value. |
| `'value-desc'` | Descending by value. |
| `'text'` | Ascending by display text. |
| `'text-desc'` | Descending by display text. |

---

### sorting

| | |
|---|---|
| **Type** | boolean |
| **Default** | `true` |

Whether clicking this column header sorts the table (when table-level `sorting` is enabled).

---

### title

| | |
|---|---|
| **Type** | string |
| **Default** | none |

The column header text in the table and the label in create/edit forms. Required when the field is displayed in the table or forms.

---

### type

| | |
|---|---|
| **Type** | string |
| **Default** | `'text'` |

The data type of the field. Plain text and numeric fields do not need this set. Special values:

| Value | Description |
|---|---|
| `'password'` | Renders a password input in create/edit forms. |
| `'textarea'` | Renders a `<textarea>` in create/edit forms. |
| `'date'` | Renders a jQuery UI datepicker. Supports `displayFormat` sub-option (see [jQuery UI datepicker formats](http://docs.jquery.com/UI/Datepicker/formatDate)). |
| `'radiobutton'` | Renders the `options` list as radio buttons instead of a combobox. Requires `options`. |
| `'checkbox'` | Renders a checkbox. Supports sub-options: `values` (e.g. `{ '0': 'Passive', '1': 'Active' }`), `formText` (fixed label text), and `setOnTextClick` (default `true`). |
| `'hidden'` | A hidden form field. Not shown in the table. Pair with `defaultValue` to pass a fixed value on create. |

---

### visibility

| | |
|---|---|
| **Type** | string |
| **Default** | `'visible'` |

Controls whether the user can hide or show this column.

| Value | Description |
|---|---|
| `'fixed'` | Always visible; cannot be hidden by the user. |
| `'visible'` | Visible by default; user can hide it. |
| `'hidden'` | Hidden by default; user can show it. |

Users access the column-visibility menu by right-clicking the table header (requires [`columnSelectable`](./02-general-options.md#columnselectable) to be `true`).

---

### width

| | |
|---|---|
| **Type** | percentage string |
| **Default** | `'10%'` |

Width of this column in the table, e.g. `'30%'`. Required when the field is displayed in the table. All visible column widths should sum to 100%.

> jTable is designed to fill its container element, not to be a fixed width. To set a fixed table width, constrain the width of the container `<div>`.

---

## Actions

Actions define how the jTable client communicates with the server. All action definitions go inside the `actions` object:

```javascript
$('#MyTableContainer').jtable({
    actions: {
        // Action definitions here
    }
    // ...
});
```

Each action can be set to either a **URL string** or a **function**.

---

### listAction

| | |
|---|---|
| **Type** | URL string or function |
| **Default** | none |

Defines how to retrieve the list of records.

### URL string

jTable sends an AJAX **POST** to the URL when `load()` is called. The server must return JSON:

```json
{
  "Result": "OK",
  "Records": [
    { "PersonId": 1, "Name": "Benjamin Button", "Age": 17, "RecordDate": "/Date(1320259705710)/" },
    { "PersonId": 2, "Name": "Douglas Adams",   "Age": 42, "RecordDate": "/Date(1320259705710)/" }
  ]
}
```

`Result` is `"OK"` or `"ERROR"`. On error, include a `"Message"` property.

**Supported date formats for record fields:**

| Format | Example |
|---|---|
| `/Date(ms)/` | `/Date(1320259705710)/` |
| `YYYY-MM-DD HH:MM:SS` | `2012-01-03 21:40:42` |
| `YYYY-MM-DD` | `2012-01-03` |

#### Paging

When paging is enabled, jTable adds these query parameters:

| Parameter | Description |
|---|---|
| `jtStartIndex` | Zero-based start index for the current page. |
| `jtPageSize` | Maximum number of records to return. |

The response must also include `TotalRecordCount` (total records across all pages).

#### Sorting

When sorting is enabled, jTable adds:

| Parameter | Example |
|---|---|
| `jtSorting` | `'Name ASC'`, `'BirthDate DESC'`, or `'CityId DESC,Name ASC'` for multi-sort. |

**Server-side examples (paged + sorted):**

```csharp
// ASP.NET MVC
[HttpPost]
public JsonResult StudentList(int jtStartIndex = 0, int jtPageSize = 0, string jtSorting = null)
{
    try {
        var count = _repository.StudentRepository.GetStudentCount();
        var students = _repository.StudentRepository.GetStudents(jtStartIndex, jtPageSize, jtSorting);
        return Json(new { Result = "OK", Records = students, TotalRecordCount = count });
    } catch (Exception ex) {
        return Json(new { Result = "ERROR", Message = ex.Message });
    }
}
```

```csharp
// ASP.NET Web Forms
[WebMethod(EnableSession = true)]
public static object StudentList(int jtStartIndex, int jtPageSize, string jtSorting)
{
    try {
        int count = _repository.StudentRepository.GetStudentCount();
        List<Student> students = _repository.StudentRepository.GetStudents(jtStartIndex, jtPageSize, jtSorting);
        return new { Result = "OK", Records = students, TotalRecordCount = count };
    } catch (Exception ex) {
        return new { Result = "ERROR", Message = ex.Message };
    }
}
```

```php
// PHP
$recordCount = mysql_fetch_array(mysql_query("SELECT COUNT(*) AS RecordCount FROM people;"))['RecordCount'];
$result = mysql_query("SELECT * FROM people ORDER BY " . $_GET["jtSorting"]
    . " LIMIT " . $_GET["jtStartIndex"] . "," . $_GET["jtPageSize"] . ";");
$rows = [];
while ($row = mysql_fetch_array($result)) { $rows[] = $row; }
echo json_encode(['Result' => 'OK', 'TotalRecordCount' => $recordCount, 'Records' => $rows]);
```

### Function

The function may return either the result data directly or a [jQuery Deferred](http://api.jquery.com/category/deferred-object/) promise.

```javascript
// Return a promise (typical real-world usage)
listAction: function (postData, jtParams) {
    return $.Deferred(function ($dfd) {
        $.ajax({
            url: '/Demo/StudentList'
                + '?jtStartIndex=' + jtParams.jtStartIndex
                + '&jtPageSize='   + jtParams.jtPageSize
                + '&jtSorting='    + jtParams.jtSorting,
            type: 'POST',
            dataType: 'json',
            data: postData,
            success: function (data) { $dfd.resolve(data); },
            error:   function ()     { $dfd.reject(); }
        });
    });
}
```

Function arguments:

| Argument | Description |
|---|---|
| `postData` | The data passed to `load()` by the caller. |
| `jtParams.jtStartIndex` | Start index for paging. |
| `jtParams.jtPageSize` | Page size for paging. |
| `jtParams.jtSorting` | Sorting string. |

---

### createAction

| | |
|---|---|
| **Type** | URL string or function |
| **Default** | none (optional — omit to disable record creation) |

Defines how to save a new record. jTable sends an AJAX **POST** with the form values when the user submits the create form.

### URL string

Expected JSON response:

```json
{
  "Result": "OK",
  "Record": { "PersonId": 5, "Name": "Dan Brown", "Age": 55, "RecordDate": "/Date(1320262185197)/" }
}
```

The `Record` property must contain the newly created record (jTable uses it to add the row to the table).

**Server-side examples:**

```csharp
// ASP.NET MVC
[HttpPost]
public JsonResult CreatePerson(Person person)
{
    try {
        Person added = _repository.PersonRepository.AddPerson(person);
        return Json(new { Result = "OK", Record = added });
    } catch (Exception ex) {
        return Json(new { Result = "ERROR", Message = ex.Message });
    }
}
```

```csharp
// ASP.NET Web Forms
[WebMethod(EnableSession = true)]
public static object CreatePerson(Person record)
{
    try {
        Person added = _repository.PersonRepository.AddPerson(record);
        return new { Result = "OK", Record = added };
    } catch (Exception ex) {
        return new { Result = "ERROR", Message = ex.Message };
    }
}
```

```php
// PHP
mysql_query("INSERT INTO people(Name, Age, RecordDate) VALUES('" . $_POST["Name"] . "', " . $_POST["Age"] . ", now());");
$row = mysql_fetch_array(mysql_query("SELECT * FROM people WHERE PersonId = LAST_INSERT_ID();"));
echo json_encode(['Result' => 'OK', 'Record' => $row]);
```

### Function

Identical pattern to `listAction` — return the result directly or via a Deferred promise.

---

### updateAction

| | |
|---|---|
| **Type** | URL string or function |
| **Default** | none (optional — omit to hide the edit button) |

Defines how to save changes to an existing record. jTable sends an AJAX **POST** with all form field values.

### URL string

Minimal successful response:

```json
{ "Result": "OK" }
```

Optionally, return a `Record` to overwrite specific fields in the table row (field-by-field merge, not full replacement):

```json
{
  "Result": "OK",
  "Record": { "Name": "Dan Brown", "Age": 55, "LastUpdateDate": "/Date(1320262185197)/" }
}
```

**Server-side examples:**

```csharp
// ASP.NET MVC
[HttpPost]
public JsonResult UpdatePerson(Person person)
{
    try {
        _repository.PersonRepository.UpdatePerson(person);
        return Json(new { Result = "OK" });
    } catch (Exception ex) {
        return Json(new { Result = "ERROR", Message = ex.Message });
    }
}
```

```csharp
// ASP.NET Web Forms
[WebMethod(EnableSession = true)]
public static object UpdatePerson(Person record)
{
    try {
        _repository.PersonRepository.UpdatePerson(record);
        return new { Result = "OK" };
    } catch (Exception ex) {
        return new { Result = "ERROR", Message = ex.Message };
    }
}
```

```php
// PHP
mysql_query("UPDATE people SET Name = '" . $_POST["Name"] . "', Age = " . $_POST["Age"]
    . " WHERE PersonId = " . $_POST["PersonId"] . ";");
echo json_encode(['Result' => 'OK']);
```

### Function

Identical pattern to `listAction`.

---

### deleteAction

| | |
|---|---|
| **Type** | URL string or function |
| **Default** | none (optional — omit to hide the delete button) |

Defines how to delete a record. jTable sends an AJAX **POST** with the record's key value.

### URL string

Expected response:

```json
{ "Result": "OK" }
```

**Server-side examples:**

```csharp
// ASP.NET MVC
[HttpPost]
public JsonResult DeletePerson(int personId)
{
    try {
        _repository.PersonRepository.DeletePerson(personId);
        return Json(new { Result = "OK" });
    } catch (Exception ex) {
        return Json(new { Result = "ERROR", Message = ex.Message });
    }
}
```

```csharp
// ASP.NET Web Forms
[WebMethod(EnableSession = true)]
public static object DeletePerson(int PersonId)
{
    try {
        _repository.PersonRepository.DeletePerson(PersonId);
        return new { Result = "OK" };
    } catch (Exception ex) {
        return new { Result = "ERROR", Message = ex.Message };
    }
}
```

```php
// PHP
mysql_query("DELETE FROM people WHERE PersonId = " . $_POST["PersonId"] . ";");
echo json_encode(['Result' => 'OK']);
```

### Function

Identical pattern to `listAction`.

---

## Methods

All methods are called on a jTable instance using the jQuery plugin syntax:

```javascript
$('#MyTableContainer').jtable('methodName', arg1, arg2, ...);
```

---

### addRecord(options)

Adds a new record to the table programmatically.

**Options:**

| Option | Type | Default | Description |
|---|---|---|---|
| `record` | object | *(required)* | The record object to add. |
| `clientOnly` | boolean | `false` | When `true`, only adds the row to the UI without posting to the server. |
| `animationsEnabled` | boolean | table default | Set to `false` to skip the insert animation. |
| `url` | string | `createAction` URL | Override the server URL used to create the record. |
| `success` | function | none | Callback fired after the record is successfully added. |
| `error` | function | none | Callback fired if an error occurs. |

```javascript
$('#StudentTableContainer').jtable('addRecord', {
    record: {
        Name: 'Halil ibrahim Kalkan',
        EmailAddress: 'halil@jtable.org',
        Password: '123',
        Gender: 'M',
        CityId: 4,
        BirthDate: '2002-11-18',
        Education: '2',
        About: 'Test record',
        IsActive: true,
        RecordDate: '2011-11-12'
    }
});
```

---

### changeColumnVisibility(columnName, visibility)

Changes the visibility of a column at runtime.

| Argument | Description |
|---|---|
| `columnName` | The field name of the column to change. |
| `visibility` | `'fixed'` (always visible), `'visible'` (visible by default), or `'hidden'` (hidden by default). |

See the field [`visibility`](./03-field-options.md#visibility) option for more detail.

---

### closeChildRow(row)

Closes an open child row for the given table row. `row` is a jQuery row (`<tr>`) selection. Used internally by jTable for child table management.

---

### closeChildTable(row, closed)

Closes an open child table for the given table row.

| Argument | Description |
|---|---|
| `row` | jQuery `<tr>` selection of the parent row. |
| `closed` | Callback function called after the child table is closed. |

---

### deleteRecord(options)

Deletes an existing record programmatically.

**Options:**

| Option | Type | Default | Description |
|---|---|---|---|
| `key` | any | *(required)* | The key (primary key) value of the record to delete. |
| `clientOnly` | boolean | `false` | When `true`, only removes the row from the UI without posting to the server. |
| `animationsEnabled` | boolean | table default | Set to `false` to skip the delete animation. |
| `url` | string | `deleteAction` URL | Override the server URL used to delete the record. |
| `success` | function | none | Callback fired after the record is successfully deleted. |
| `error` | function | none | Callback fired if an error occurs. |

```javascript
$('#StudentTableContainer').jtable('deleteRecord', {
    key: 42
});
```

---

### deleteRows(rows)

Deletes one or more rows from both the server and the table.

| Argument | Description |
|---|---|
| `rows` | jQuery selection of `<tr>` elements to delete. |

Commonly combined with [`selectedRows`](#selectedrows):

```javascript
var $selected = $('#PersonTable').jtable('selectedRows');
$('#PersonTable').jtable('deleteRows', $selected);
```

---

### destroy()

Completely removes the jTable instance and its generated HTML from the container element.

---

### getChildRow(row)

Returns the child `<tr>` element for the given parent row, so you can inject custom content into it. Use after calling [`openChildRow`](#openchildrow).

---

### getRowByKey(key)

Returns the jQuery `<tr>` selection for the record whose key field value matches `key`.

---

### isChildRowOpen(row)

Returns `true` if the child row for the given parent row is currently open.

---

### load(postData, completeCallback)

Fetches records from the server and populates the table. Both arguments are optional.

Pass additional filter parameters via `postData`:

```javascript
$('#PersonTable').jtable('load', { CityId: 2, Name: 'Halil' });
```

The server receives these alongside the standard paging/sorting parameters. Pass `completeCallback` to be notified when loading finishes successfully.

---

### openChildRow(row)

Opens a custom child row beneath the given parent row. Returns the opened child `<tr>` element so you can fill it with any HTML content.

The child row is automatically removed if its parent row is removed from the table.

> If you want to open a child **jTable** instance rather than a generic child row, use [`openChildTable`](#openchildtable) instead.

---

### openChildTable(row, tableOptions, opened)

Creates and opens a child jTable beneath the given parent row.

| Argument | Description |
|---|---|
| `row` | jQuery `<tr>` selection of the parent row. |
| `tableOptions` | Standard jTable options for the child table. |
| `opened` | Callback fired after the child table's open animation completes. Receives a `data` object with `data.childTable` (jQuery reference to the child container). |

**Example — opening a child table from a custom display column:**

```javascript
Phones: {
    title: '',
    width: '5%',
    sorting: false,
    edit: false,
    create: false,
    display: function (personData) {
        var $img = $('<img src="/Content/images/phone.png" title="Edit phone numbers" />');
        $img.click(function () {
            $('#PersonTable').jtable('openChildTable',
                $img.closest('tr'),
                {
                    title: personData.record.Name + ' - Phone numbers',
                    actions: {
                        listAction:   '/Person/PhoneList?PersonId='   + personData.record.PersonId,
                        deleteAction: '/Person/DeletePhone',
                        updateAction: '/Person/UpdatePhone',
                        createAction: '/Person/CreatePhone?PersonId=' + personData.record.PersonId
                    },
                    fields: {
                        PhoneId: { key: true, create: false, edit: false, list: false },
                        PhoneType: {
                            title: 'Phone type',
                            width: '30%',
                            options: { '1': 'Home phone', '2': 'Office phone', '3': 'Cell phone' }
                        },
                        Number: { title: 'Phone Number', width: '30%' },
                        RecordDate: {
                            title: 'Record date', width: '20%',
                            type: 'date', displayFormat: 'dd.mm.yy',
                            create: false, edit: false
                        }
                    }
                },
                function (data) {
                    data.childTable.jtable('load');
                }
            );
        });
        return $img;
    }
}
```

---

### reload(completeCallback)

Re-fetches records from the server using the same `postData` that was used in the last `load()` call. Preserves the current page and sort order.

Use this to refresh table data without resetting pagination or filters. Pass `completeCallback` to be notified when reloading completes.

---

### selectedRows()

Returns a jQuery selection of all currently selected `<tr>` elements.

```javascript
var $selectedRows = $('#PersonTable').jtable('selectedRows');
$selectedRows.each(function () {
    var record = $(this).data('record');
    console.log(record.PersonId, record.Name);
});
```

---

### selectRows(rows)

Programmatically selects one or more rows.

| Argument | Description |
|---|---|
| `rows` | jQuery selection of `<tr>` elements to select. |

---

### showCreateForm()

Programmatically opens the "Create new record" dialog, equivalent to the user clicking the "Add new record" button.

---

### updateRecord(options)

Updates an existing record programmatically.

**Options:**

| Option | Type | Default | Description |
|---|---|---|---|
| `record` | object | *(required)* | Record to update. Must include the key field value to identify which row to update. |
| `clientOnly` | boolean | `false` | When `true`, only updates the UI without posting to the server. |
| `animationsEnabled` | boolean | table default | Set to `false` to skip the update animation. |
| `url` | string | `updateAction` URL | Override the server URL used to update the record. |
| `success` | function | none | Callback fired after the record is successfully updated. |
| `error` | function | none | Callback fired if an error occurs. |

```javascript
$('#StudentTableContainer').jtable('updateRecord', {
    record: {
        StudentId: 42,
        Name: 'Halil Kalkan',
        EmailAddress: 'halil@jtable.org',
        Password: '123456',
        Gender: 'M',
        CityId: 4,
        BirthDate: '2001-11-18',
        Education: '3',
        About: 'Updated record',
        IsActive: true,
        RecordDate: '2012-01-05'
    }
});
```

---

## Events

Event handlers are registered as options during jTable initialization:

```javascript
$('#MyTableContainer').jtable({
    // options...
    recordAdded: function (event, data) {
        console.log('Record added:', data.record);
    }
});
```

---

### closeRequested(event, data)

Fired when the user clicks the table's close button or icon. The close button is only visible when [`showCloseButton`](./02-general-options.md#showclosebutton) is `true`.

This event has no extra `data` properties.

---

### formClosed(event, data)

Fired when a create or edit form dialog is **closed**.

| `data` property | Description |
|---|---|
| `data.form` | The form element as a jQuery selection. |
| `data.formType` | `'create'` or `'edit'`. |
| `data.row` | The edited table row (jQuery selection); only set for `'edit'` forms. |

---

### formCreated(event, data)

Fired when a create or edit form dialog is **rendered**.

| `data` property | Description |
|---|---|
| `data.form` | The form element as a jQuery selection. |
| `data.formType` | `'create'` or `'edit'`. |
| `data.record` | The record being edited; only set for `'edit'` forms. Access fields via `data.record.Name`, etc. |
| `data.row` | The edited table row (jQuery selection); only set for `'edit'` forms. |

---

### formSubmitting(event, data)

Fired when the save/submit button is clicked on a create or edit form.

| `data` property | Description |
|---|---|
| `data.form` | The form element as a jQuery selection. |
| `data.formType` | `'create'` or `'edit'`. |
| `data.row` | The edited table row (jQuery selection); only set for `'edit'` forms. |

> **Validation hook:** Return `false` from this handler to cancel the submit operation.

```javascript
formSubmitting: function (event, data) {
    if (!data.form.find('#Name').val()) {
        alert('Name is required.');
        return false; // cancel submit
    }
}
```

---

### loadingRecords(event, data)

Fired immediately before jTable sends the AJAX request to load records from the server. Has no extra `data` properties.

---

### recordAdded(event, data)

Fired after a new record is successfully created and saved.

| `data` property | Description |
|---|---|
| `data.record` | The newly added record object. |
| `data.serverResponse` | The raw JSON response object returned by the server. |

---

### recordDeleted(event, data)

Fired after a record is successfully deleted.

| `data` property | Description |
|---|---|
| `data.record` | The deleted record object. |
| `data.row` | The deleted table row (jQuery selection). |
| `data.serverResponse` | The raw JSON response object returned by the server. |

---

### recordsLoaded(event, data)

Fired after jTable loads records from the server and refreshes the table. Also fired on every page change when paging is enabled.

| `data` property | Description |
|---|---|
| `data.records` | Array of all record objects loaded from the server. |
| `data.serverResponse` | The raw JSON response object returned by the server. |

---

### recordUpdated(event, data)

Fired after a record is successfully updated.

| `data` property | Description |
|---|---|
| `data.record` | The updated record object. |
| `data.row` | The updated table row (jQuery selection). |
| `data.serverResponse` | The raw JSON response object returned by the server. |

---

### rowInserted(event, data)

Fired each time a row is inserted into the visible table — both when the user adds a new record and for every row rendered during a records-load operation.

| `data` property | Description |
|---|---|
| `data.row` | The inserted `<tr>` element as a jQuery selection. |
| `data.record` | The record associated with this row. |
| `data.isNewRow` | `true` when the row was inserted because the user created a new record; `false` during load. |

---

### rowsRemoved(event, data)

Fired when one or more rows are removed from the table — either because records were deleted or because the table is being re-loaded (all rows are cleared before new ones are inserted).

| `data` property | Description |
|---|---|
| `data.rows` | All removed rows as a jQuery selection. |
| `data.reason` | `'deleted'` when rows were permanently deleted; `'reloading'` when rows were cleared as part of a reload. |

---

### rowUpdated(event, data)

Fired after a row is updated in the table following a successful record update. This event fires after [`recordUpdated`](#recordupdated).

| `data` property | Description |
|---|---|
| `data.row` | The updated `<tr>` element as a jQuery selection. |
| `data.record` | The updated record object. |

---

### selectionChanged(event, data)

Fired whenever the set of selected rows changes — for example, when a row is selected or deselected, a selected row is deleted, or the page changes while rows are selected.

Use the [`selectedRows`](./05-methods.md#selectedrows) method inside this handler to retrieve the current selection.

---

## Localization

jTable supports full UI localization either through ready-made translation files or by supplying a custom message object.

---

### Using a Localization File

Add a localization script from the `localization/` folder of the library, immediately after the main jTable script:

```html
<script src="/Scripts/jtable/jquery.jtable.js"></script>
<script src="/Scripts/jtable/localization/jquery.jtable.tr.js"></script>
```

The example above loads the Turkish (`tr`) translation. The library ships with translations for several languages. You can also write your own and share it with the community on [GitHub](https://github.com/hikalkan/jtable).

---

### Using Custom Messages

Pass a `messages` object when initialising a single jTable instance:

```javascript
$('#MyTableContainer').jtable({
    messages: {
        serverCommunicationError: 'An error occurred while communicating with the server.',
        loadingMessage:           'Loading records...',
        // ... other keys
    }
    // other options...
});
```

To apply custom messages to **all** jTable instances on the page, extend the prototype defaults:

```javascript
$.extend(true, $.hik.jtable.prototype.options.messages, myCustomMessages);
```

See [How to set general options](./02-general-options.md#how-to-set-general-options) for more detail on prototype-level configuration.

---

### Default Messages

These are the built-in English message keys and their default values:

```javascript
messages: {
    serverCommunicationError: 'An error occured while communicating to the server.',
    loadingMessage:           'Loading records...',
    noDataAvailable:          'No data available!',
    addNewRecord:             'Add new record',
    editRecord:               'Edit Record',
    areYouSure:               'Are you sure?',
    deleteConfirmation:       'This record will be deleted. Are you sure?',
    save:                     'Save',
    saving:                   'Saving',
    cancel:                   'Cancel',
    deleteText:               'Delete',
    deleting:                 'Deleting',
    error:                    'Error',
    close:                    'Close',
    cannotLoadOptionsFor:     'Can not load options for field {0}',
    pagingInfo:               'Showing {0}-{1} of {2}',
    pageSizeChangeLabel:      'Row count',
    gotoPageLabel:            'Go to page',
    canNotDeletedRecords:     'Can not deleted {0} of {1} records!',
    deleteProggress:          'Deleted {0} of {1} records, processing...'
}
```

| Key | Description |
|---|---|
| `serverCommunicationError` | Shown when an AJAX request fails. |
| `loadingMessage` | Shown while records are being fetched. |
| `noDataAvailable` | Shown when the server returns an empty record set. |
| `addNewRecord` | Label for the "add new record" toolbar button. |
| `editRecord` | Title of the edit dialog. |
| `areYouSure` | Generic confirmation prompt. |
| `deleteConfirmation` | Delete confirmation message. |
| `save` | Save button label. |
| `saving` | Save button label while saving. |
| `cancel` | Cancel button label. |
| `deleteText` | Delete button label. |
| `deleting` | Delete button label while deleting. |
| `error` | Generic error label used in dialogs. |
| `close` | Close button label. |
| `cannotLoadOptionsFor` | Error shown when option-list loading fails. `{0}` = field name. |
| `pagingInfo` | Paging status text. `{0}` = first record, `{1}` = last record, `{2}` = total. |
| `pageSizeChangeLabel` | Label next to the page-size dropdown. |
| `gotoPageLabel` | Label next to the go-to-page input. |
| `canNotDeletedRecords` | Shown after a batch delete when some records could not be deleted. `{0}` = failed, `{1}` = total. |
| `deleteProggress` | Shown during a batch delete in progress. `{0}` = deleted so far, `{1}` = total. |

---

### Example — Turkish Localization

```javascript
var turkishMessages = {
    serverCommunicationError: 'Sunucu ile iletişim kurulurken bir hata oluştu.',
    loadingMessage:           'Kayıtlar yükleniyor...',
    noDataAvailable:          'Hiç kayıt bulunmamaktadır!',
    addNewRecord:             'Yeni kayıt ekle',
    editRecord:               'Kayıt düzenle',
    areYouSure:               'Emin misiniz?',
    deleteConfirmation:       'Bu kayıt silinecektir. Emin misiniz?',
    save:                     'Kaydet',
    saving:                   'Kaydediyor',
    cancel:                   'İptal',
    deleteText:               'Sil',
    deleting:                 'Siliyor',
    error:                    'Hata',
    close:                    'Kapat',
    cannotLoadOptionsFor:     '{0} alanı için seçenekler yüklenemedi!',
    pagingInfo:               'Görüntülenen: {0}-{1}, Toplam: {2}',
    pageSizeChangeLabel:      'Satır sayısı',
    gotoPageLabel:            'Sayfaya git',
    canNotDeletedRecords:     '{1} kayıttan {0} adedi silinemedi!',
    deleteProggress:          '{1} kayıttan {0} adedi silindi, devam ediliyor...'
};

// Apply to all instances
$.extend(true, $.hik.jtable.prototype.options.messages, turkishMessages);
```

---

