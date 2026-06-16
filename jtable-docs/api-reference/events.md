# jTable API Reference — Events

Event handlers are registered as options during jTable initialization:

```javascript
$('#MyTableContainer').jtable({
    // options...
    recordAdded: function (event, data) {
        console.log('Record added:', data.record);
    }
});
```

## closeRequested(event, data)

Fired when the user clicks the table's close button or icon. The close button is only visible when [`showCloseButton`](./02-general-options.md#showclosebutton) is `true`.

This event has no extra `data` properties.

---

## formClosed(event, data)

Fired when a create or edit form dialog is **closed**.

| `data` property | Description |
|---|---|
| `data.form` | The form element as a jQuery selection. |
| `data.formType` | `'create'` or `'edit'`. |
| `data.row` | The edited table row (jQuery selection); only set for `'edit'` forms. |

---

## formCreated(event, data)

Fired when a create or edit form dialog is **rendered**.

| `data` property | Description |
|---|---|
| `data.form` | The form element as a jQuery selection. |
| `data.formType` | `'create'` or `'edit'`. |
| `data.record` | The record being edited; only set for `'edit'` forms. Access fields via `data.record.Name`, etc. |
| `data.row` | The edited table row (jQuery selection); only set for `'edit'` forms. |

---

## formSubmitting(event, data)

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

## loadingRecords(event, data)

Fired immediately before jTable sends the AJAX request to load records from the server. Has no extra `data` properties.

---

## recordAdded(event, data)

Fired after a new record is successfully created and saved.

| `data` property | Description |
|---|---|
| `data.record` | The newly added record object. |
| `data.serverResponse` | The raw JSON response object returned by the server. |

---

## recordDeleted(event, data)

Fired after a record is successfully deleted.

| `data` property | Description |
|---|---|
| `data.record` | The deleted record object. |
| `data.row` | The deleted table row (jQuery selection). |
| `data.serverResponse` | The raw JSON response object returned by the server. |

---

## recordsLoaded(event, data)

Fired after jTable loads records from the server and refreshes the table. Also fired on every page change when paging is enabled.

| `data` property | Description |
|---|---|
| `data.records` | Array of all record objects loaded from the server. |
| `data.serverResponse` | The raw JSON response object returned by the server. |

---

## recordUpdated(event, data)

Fired after a record is successfully updated.

| `data` property | Description |
|---|---|
| `data.record` | The updated record object. |
| `data.row` | The updated table row (jQuery selection). |
| `data.serverResponse` | The raw JSON response object returned by the server. |

---

## rowInserted(event, data)

Fired each time a row is inserted into the visible table — both when the user adds a new record and for every row rendered during a records-load operation.

| `data` property | Description |
|---|---|
| `data.row` | The inserted `<tr>` element as a jQuery selection. |
| `data.record` | The record associated with this row. |
| `data.isNewRow` | `true` when the row was inserted because the user created a new record; `false` during load. |

---

## rowsRemoved(event, data)

Fired when one or more rows are removed from the table — either because records were deleted or because the table is being re-loaded (all rows are cleared before new ones are inserted).

| `data` property | Description |
|---|---|
| `data.rows` | All removed rows as a jQuery selection. |
| `data.reason` | `'deleted'` when rows were permanently deleted; `'reloading'` when rows were cleared as part of a reload. |

---

## rowUpdated(event, data)

Fired after a row is updated in the table following a successful record update. This event fires after [`recordUpdated`](#recordupdated).

| `data` property | Description |
|---|---|
| `data.row` | The updated `<tr>` element as a jQuery selection. |
| `data.record` | The updated record object. |

---

## selectionChanged(event, data)

Fired whenever the set of selected rows changes — for example, when a row is selected or deselected, a selected row is deleted, or the page changes while rows are selected.

Use the [`selectedRows`](./05-methods.md#selectedrows) method inside this handler to retrieve the current selection.
