# jTable Documentation

Welcome to the official documentation for **jTable** — a jQuery plugin for building AJAX-powered CRUD tables with minimal effort.

> This is the enhanced version of jTable with new UI themes and adapter support including Bootstrap 5, Bulma, Semantic UI, and more.

***

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

***

## Where to Start

| <p><strong>🚀 New to jTable?</strong><br>Start with the <a href="/broken/pages/cnynfHqAcsJ8yixXFgB1">Introduction</a> and follow the Quick Start guide.</p> | <p><strong>📖 Looking for a specific option?</strong><br>Jump to the <a href="jtable-docs/api-reference/overview.md">API Reference</a>.</p>                                              |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>🎨 Setting up a theme?</strong><br>See the <a href="jtable-docs/themes-ui/overview.md">Themes &#x26; UI</a> section.</p>                         | <p><strong>⚡ Already know jTable?</strong><br>Go straight to <a href="jtable-docs/api-reference/methods.md">Methods</a> or <a href="jtable-docs/api-reference/events.md">Events</a>.</p> |
