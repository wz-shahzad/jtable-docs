# jTable API Reference — Methods

All methods are called on a jTable instance using the jQuery plugin syntax:

```javascript
$('#MyTableContainer').jtable('methodName', arg1, arg2, ...);
```

## addRecord(options)

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

## changeColumnVisibility(columnName, visibility)

Changes the visibility of a column at runtime.

| Argument | Description |
|---|---|
| `columnName` | The field name of the column to change. |
| `visibility` | `'fixed'` (always visible), `'visible'` (visible by default), or `'hidden'` (hidden by default). |

See the field [`visibility`](./03-field-options.md#visibility) option for more detail.

---

## closeChildRow(row)

Closes an open child row for the given table row. `row` is a jQuery row (`<tr>`) selection. Used internally by jTable for child table management.

---

## closeChildTable(row, closed)

Closes an open child table for the given table row.

| Argument | Description |
|---|---|
| `row` | jQuery `<tr>` selection of the parent row. |
| `closed` | Callback function called after the child table is closed. |

---

## deleteRecord(options)

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

## deleteRows(rows)

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

## destroy()

Completely removes the jTable instance and its generated HTML from the container element.

---

## getChildRow(row)

Returns the child `<tr>` element for the given parent row, so you can inject custom content into it. Use after calling [`openChildRow`](#openchildrow).

---

## getRowByKey(key)

Returns the jQuery `<tr>` selection for the record whose key field value matches `key`.

---

## isChildRowOpen(row)

Returns `true` if the child row for the given parent row is currently open.

---

## load(postData, completeCallback)

Fetches records from the server and populates the table. Both arguments are optional.

Pass additional filter parameters via `postData`:

```javascript
$('#PersonTable').jtable('load', { CityId: 2, Name: 'Halil' });
```

The server receives these alongside the standard paging/sorting parameters. Pass `completeCallback` to be notified when loading finishes successfully.

---

## openChildRow(row)

Opens a custom child row beneath the given parent row. Returns the opened child `<tr>` element so you can fill it with any HTML content.

The child row is automatically removed if its parent row is removed from the table.

> If you want to open a child **jTable** instance rather than a generic child row, use [`openChildTable`](#openchildtable) instead.

---

## openChildTable(row, tableOptions, opened)

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

## reload(completeCallback)

Re-fetches records from the server using the same `postData` that was used in the last `load()` call. Preserves the current page and sort order.

Use this to refresh table data without resetting pagination or filters. Pass `completeCallback` to be notified when reloading completes.

---

## selectedRows()

Returns a jQuery selection of all currently selected `<tr>` elements.

```javascript
var $selectedRows = $('#PersonTable').jtable('selectedRows');
$selectedRows.each(function () {
    var record = $(this).data('record');
    console.log(record.PersonId, record.Name);
});
```

---

## selectRows(rows)

Programmatically selects one or more rows.

| Argument | Description |
|---|---|
| `rows` | jQuery selection of `<tr>` elements to select. |

---

## showCreateForm()

Programmatically opens the "Create new record" dialog, equivalent to the user clicking the "Add new record" button.

---

## updateRecord(options)

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
