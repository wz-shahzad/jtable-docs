# jTable API Reference — Actions

Actions define how the jTable client communicates with the server. All action definitions go inside the `actions` object:

```javascript
$('#MyTableContainer').jtable({
    actions: {
        // Action definitions here
    }
    // ...
});
```

**Table of Contents**

- [listAction](#listaction)
- [createAction](#createaction)
- [updateAction](#updateaction)
- [deleteAction](#deleteaction)

Each action can be set to either a **URL string** or a **function**.

---

## listAction

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

## createAction

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

## updateAction

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

## deleteAction

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
