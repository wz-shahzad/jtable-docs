# jTable Documentation

Welcome to the official documentation for **jTable** — a jQuery plugin for building AJAX-powered CRUD tables with minimal effort.

> This is the enhanced version of jTable with new UI themes and adapter support including Bootstrap 5, Bulma, Semantic UI, and more.

---

## What is jTable?

jTable lets you create fully functional data tables — with listing, sorting, paging, and create/edit/delete dialogs — without writing repetitive HTML or JavaScript boilerplate.

```javascript
$('#StudentsTable').jtable({
    title: 'Students',
    paging: true,
    sorting: true,
    actions: {
        listAction:   '/api/students/list',
        createAction: '/api/students/create',
        updateAction: '/api/students/update',
        deleteAction: '/api/students/delete'
    },
    fields: {
        StudentId: { key: true, list: false },
        Name:      { title: 'Name', width: '30%' },
        City:      { title: 'City', width: '20%' }
    }
});

$('#StudentsTable').jtable('load');
```

---

## Where to Start

<table>
  <tr>
    <td><strong>🚀 New to jTable?</strong><br/>Start with the <a href="getting-started/introduction.md">Introduction</a> and follow the Quick Start guide.</td>
    <td><strong>📖 Looking for a specific option?</strong><br/>Jump to the <a href="api-reference/overview.md">API Reference</a>.</td>
  </tr>
  <tr>
    <td><strong>🎨 Setting up a theme?</strong><br/>See the <a href="themes-ui/overview.md">Themes & UI</a> section.</td>
    <td><strong>⚡ Already know jTable?</strong><br/>Go straight to <a href="api-reference/methods.md">Methods</a> or <a href="api-reference/events.md">Events</a>.</td>
  </tr>
</table>
