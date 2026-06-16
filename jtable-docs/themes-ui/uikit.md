# UIkit Theme

jTable's UIkit adapter renders all UI components using UIkit 3 classes and utilities. Date fields use flatpickr. Icons are provided by Font Awesome 6.

---

## Dependencies

| Library | Version | CDN |
|---|---|---|
| jQuery | 3.1.1 | `ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js` |
| UIkit | 3.25.5 | `cdn.jsdelivr.net/npm/uikit@3.25.5` |
| UIkit Icons | 3.25.5 | `cdn.jsdelivr.net/npm/uikit@3.25.5/dist/js/uikit-icons.min.js` |
| Font Awesome | 6.4.0 | `cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0` |
| flatpickr | latest | `cdn.jsdelivr.net/npm/flatpickr` |

---

## Setup

```html
<!-- UIkit CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/uikit@3.25.5/dist/css/uikit.min.css" />
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/flatpickr/dist/flatpickr.min.css">

<!-- jTable UIkit CSS -->
<link href="~/dev/ui/UIKit-UI/jtable.ui.uikit-ui.css" rel="stylesheet" />

<!-- jQuery -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>

<!-- UIkit JS -->
<script src="https://cdn.jsdelivr.net/npm/uikit@3.25.5/dist/js/uikit.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/uikit@3.25.5/dist/js/uikit-icons.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/flatpickr"></script>

<!-- jTable core -->
<script src="~/dev/jquery.jtable-vnext.js"></script>

<!-- jTable UIkit adapter -->
<script src="~/dev/ui/UIKit-UI/jquery.jtable.ui.uikit-ui.js"></script>
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
        }
    });

    $('#MyTableContainer').jtable('load');
});
```

---

## Notes

- Add `style="padding: 5px;"` to the container div for comfortable spacing.
- flatpickr handles date input for `type: 'date'` fields — no jQuery UI required.
- UIkit icons (`uikit-icons.min.js`) must be loaded after `uikit.min.js`.
- `smallSize: true` is recommended for a clean UIkit table appearance.
- RTL is not supported in this adapter.
