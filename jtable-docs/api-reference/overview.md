# API Reference

Complete reference for all jTable options, methods, and events.

---

## Structure

A jTable instance is initialized with three main building blocks:

```javascript
$('#Container').jtable({

    // 1. General Options — control table-level behaviour
    title: 'My Table',
    paging: true,
    sorting: true,

    // 2. Actions — define server communication
    actions: {
        listAction:   '/api/list',
        createAction: '/api/create',
        updateAction: '/api/update',
        deleteAction: '/api/delete'
    },

    // 3. Fields — define columns and form inputs
    fields: {
        Id:   { key: true, list: false },
        Name: { title: 'Name', width: '50%' }
    }

});
```

---

## Reference Sections

| Section | Description |
|---|---|
| [General Options](general-options.md) | Table-level settings: paging, sorting, themes, toolbar, etc. |
| [Field Options](field-options.md) | Per-field settings: type, visibility, validation, custom inputs. |
| [Actions](actions.md) | Server endpoints for list, create, update, delete. |
| [Methods](methods.md) | JavaScript API: `load()`, `addRecord()`, `updateRecord()`, etc. |
| [Events](events.md) | Hooks: `recordAdded`, `formCreated`, `selectionChanged`, etc. |
| [Localization](localization.md) | Translating the UI to any language. |

---

## Server Response Format

Every server action must return a JSON object with a `Result` field:

```json
{ "Result": "OK" }
{ "Result": "ERROR", "Message": "Describe the error here." }
```

See the [Actions](actions.md) page for the full response contract per endpoint.
