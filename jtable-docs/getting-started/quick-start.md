# Quick Start

This guide walks you through building a complete CRUD table — list, create, edit, delete — from scratch.

---

## 1. Add the Container

Add a single `<div>` where you want the table to appear:

```html
<div id="PersonTable"></div>
```

---

## 2. Initialize jTable

Inside `$(document).ready`, call `.jtable()` on the container:

```javascript
$(document).ready(function () {
    $('#PersonTable').jtable({
        title: 'People',
        paging: true,
        pageSize: 10,
        sorting: true,
        defaultSorting: 'Name ASC',

        actions: {
            listAction:   '/Person/List',
            createAction: '/Person/Create',
            updateAction: '/Person/Update',
            deleteAction: '/Person/Delete'
        },

        fields: {
            PersonId: {
                key: true,
                create: false,
                edit: false,
                list: false
            },
            Name: {
                title: 'Name',
                width: '30%'
            },
            Age: {
                title: 'Age',
                width: '10%'
            },
            Gender: {
                title: 'Gender',
                width: '15%',
                options: { 'M': 'Male', 'F': 'Female' }
            },
            IsActive: {
                title: 'Active',
                width: '10%',
                type: 'checkbox',
                values: { 'false': 'Passive', 'true': 'Active' }
            },
            RecordDate: {
                title: 'Created',
                width: '15%',
                type: 'date',
                displayFormat: 'yy-mm-dd',
                create: false,
                edit: false
            }
        }
    });
});
```

---

## 3. Load Data

After initialization, call `load()` to fetch and display records:

```javascript
$('#PersonTable').jtable('load');
```

You can pass extra filter parameters to narrow results:

```javascript
$('#PersonTable').jtable('load', { CityId: 3 });
```

---

## 4. Server-Side Endpoints

Each action expects a specific JSON response format.

### listAction

```json
{
  "Result": "OK",
  "TotalRecordCount": 45,
  "Records": [
    { "PersonId": 1, "Name": "Alice", "Age": 30, "Gender": "F", "IsActive": true },
    { "PersonId": 2, "Name": "Bob",   "Age": 25, "Gender": "M", "IsActive": true }
  ]
}
```

> `TotalRecordCount` is required when paging is enabled.

### createAction

```json
{
  "Result": "OK",
  "Record": { "PersonId": 42, "Name": "Charlie", "Age": 28, "Gender": "M", "IsActive": true }
}
```

### updateAction

```json
{ "Result": "OK" }
```

### deleteAction

```json
{ "Result": "OK" }
```

### Error response (any action)

```json
{ "Result": "ERROR", "Message": "Something went wrong." }
```

---

## 5. Server-Side Example (ASP.NET MVC)

```csharp
[HttpPost]
public JsonResult List(int jtStartIndex = 0, int jtPageSize = 0, string jtSorting = null)
{
    try {
        int count = _repo.GetPersonCount();
        var people = _repo.GetPersons(jtStartIndex, jtPageSize, jtSorting);
        return Json(new { Result = "OK", Records = people, TotalRecordCount = count });
    } catch (Exception ex) {
        return Json(new { Result = "ERROR", Message = ex.Message });
    }
}

[HttpPost]
public JsonResult Create(Person person)
{
    try {
        var added = _repo.AddPerson(person);
        return Json(new { Result = "OK", Record = added });
    } catch (Exception ex) {
        return Json(new { Result = "ERROR", Message = ex.Message });
    }
}

[HttpPost]
public JsonResult Update(Person person)
{
    try {
        _repo.UpdatePerson(person);
        return Json(new { Result = "OK" });
    } catch (Exception ex) {
        return Json(new { Result = "ERROR", Message = ex.Message });
    }
}

[HttpPost]
public JsonResult Delete(int personId)
{
    try {
        _repo.DeletePerson(personId);
        return Json(new { Result = "OK" });
    } catch (Exception ex) {
        return Json(new { Result = "ERROR", Message = ex.Message });
    }
}
```

---

## What's Next

| Topic | Link |
|---|---|
| All table-level options | [General Options](../api-reference/general-options.md) |
| All field options | [Field Options](../api-reference/field-options.md) |
| Calling methods from code | [Methods](../api-reference/methods.md) |
| Reacting to table events | [Events](../api-reference/events.md) |
| Changing the UI theme | [Themes & UI](../themes-ui/overview.md) |
