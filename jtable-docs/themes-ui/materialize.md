# Materialize Theme

jTable's Materialize adapter renders all UI components using Materialize CSS 2.x (Material Design). Date fields use bootstrap-datepicker. Dialogs use the native HTML `popover` API.

---

## Dependencies

| Library | Version | CDN |
|---|---|---|
| jQuery | 3.1.1 | `ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js` |
| Materialize CSS | 2.1.0 | `cdn.jsdelivr.net/npm/@materializecss/materialize@2.1.0` |
| Bootstrap Datepicker | 1.9.0 | `cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.9.0` |
| Material Icons | latest | `fonts.googleapis.com/icon?family=Material+Icons` |

---

## Setup

```html
<!-- Materialize CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@materializecss/materialize@2.1.0/dist/css/materialize.min.css" />
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.9.0/css/bootstrap-datepicker.min.css" />
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" />

<!-- jTable Materialize CSS -->
<link href="~/dev/ui/Materialize-UI/jtable.ui.materialize.css" rel="stylesheet" />

<!-- jQuery -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>

<!-- Materialize JS -->
<script src="https://cdn.jsdelivr.net/npm/@materializecss/materialize@2.1.0/dist/js/materialize.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.9.0/js/bootstrap-datepicker.min.js"></script>

<!-- jTable core -->
<script src="~/dev/jquery.jtable-vnext.js"></script>

<!-- jTable Materialize adapter -->
<script src="~/dev/ui/Materialize-UI/jquery.jtable.ui.materialize-ui.js"></script>
```

---

## Initialization

```javascript
$(document).ready(function () {
    $('#MyTableContainer').jtable({
        title: 'My Table',
        paging: true,
        sorting: true,
        multiSorting: true,
        pageSize: 10,
        columnResizable: false,
        columnSelectable: true,
        smallSize: true,
        selecting: true,
        multiselect: true,
        selectingCheckboxes: true,
        actions: {
            listAction:   '/api/list',
            createAction: '/api/create',
            updateAction: '/api/update',
            deleteAction: '/api/delete'
        },
        fields: {
            id:   { key: true, create: false, edit: false, list: false },
            name: { title: 'Name', width: '30%' }
        },

        // Required for Materialize: initialize dynamic form components
        formCreated: function (event, data) {
            var form = data.form;

            // Reorder labels after inputs for Materialize floating labels
            form.find('.input-field .jtable-input-label').each(function () {
                var $label = $(this);
                var $input = $label.closest('.input-field')
                    .find('input:not([type="checkbox"]):not([type="radio"]), select, textarea')
                    .first();
                if ($input.length) { $input.after($label); }
            });

            // Initialize Materialize select components
            M.FormSelect.init(form[0].querySelectorAll('select'));
            form.find('select').trigger('change');

            // Fix visibility of checkboxes and radio buttons
            form.find('input[type="checkbox"].filled-in, input[type="radio"].with-gap').each(function () {
                $(this).css({ opacity: '1', position: 'static', border: '0' });
            });
        }
    });

    $('#MyTableContainer').jtable('load');
});
```

---

## Dialog Styling

The Materialize adapter uses the native HTML `popover` API for create/edit dialogs. Optional custom dialog CSS:

```css
[popover] {
    border: none;
    padding: 0;
    border-radius: 28px;
    box-shadow: 0 24px 38px 3px rgba(0,0,0,0.14);
    max-width: 400px;
    width: 90%;
}

[popover]::backdrop {
    backdrop-filter: blur(2px);
    background-color: rgba(0,0,0,0.3);
}
```

---

## Notes

- The `formCreated` event handler is **required** to properly initialize Materialize form components (floating labels, select dropdowns, checkboxes).
- `smallSize: true` is recommended for a compact Material Design table.
- RTL is not supported in this adapter.
