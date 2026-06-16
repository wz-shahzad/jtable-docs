# jTable API Reference — General Options

General options control the overall behavior of a jTable instance.

## How to Set General Options

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

## Option Reference

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
