# jTable API Reference — Field Options

A field definition describes the structure and behaviour of a single record field. Fields are declared inside the `fields` object of the jTable initialization options:

```javascript
fields: {
    FieldName: {
        // field options
    }
}
```

**Table of Contents**

- [columnResizable](#columnresizable)
- [create](#create)
- [edit](#edit)
- [defaultValue](#defaultvalue)
- [dependsOn](#dependson)
- [display](#display)
- [input](#input)
- [inputClass](#inputclass)
- [inputTitle](#inputtitle)
- [key](#key)
- [list](#list)
- [listClass](#listclass)
- [options](#options)
- [optionsSorting](#optionssorting)
- [sorting](#sorting)
- [title](#title)
- [type](#type)
- [visibility](#visibility)
- [width](#width)

---

## Option Reference

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
