# Custom Adapter

If you are using a CSS framework not covered by the bundled adapters, you can write your own adapter in a few minutes.

---

## Register an Adapter

Call `jQuery.hik.jtable.adapters.register()` after loading jTable:

```javascript
jQuery.hik.jtable.adapters.register('mylib', {

    // ── CSS class mappings ─────────────────────────────────────────────────

    buttonClass:        'mylib-btn mylib-btn-primary',
    dangerButtonClass:  'mylib-btn mylib-btn-danger',
    inputClass:         'mylib-input',
    selectClass:        'mylib-select',
    textareaClass:      'mylib-textarea',
    checkboxClass:      'mylib-checkbox',

    // ── Layout renderers ───────────────────────────────────────────────────

    renderHeader: function ($wrap, opts) {
        $wrap.addClass('mylib-panel-header');
        // opts.title is the table title string
    },

    renderFooter: function ($wrap, opts) {
        $wrap.addClass('mylib-panel-footer');
    },

    renderRowCommand: function ($cell, cmd) {
        // cmd.name  → 'edit' | 'delete' | custom name
        // cmd.label → display text
        // cmd.icon  → icon URL or class string
        $cell.append(
            $('<button>')
                .addClass('mylib-btn mylib-btn-sm')
                .text(cmd.label)
                .on('click', cmd.onClick)
        );
    },

    // ── Modal lifecycle ────────────────────────────────────────────────────

    openDialog: function ($modal) {
        // $modal is the dialog jQuery element jTable built
        // Show it using your framework's modal API
        MyLib.modal.open($modal[0]);
    },

    closeDialog: function ($modal) {
        MyLib.modal.close($modal[0]);
    }

});
```

Then use it with `ui: 'mylib'`:

```javascript
$('#MyTable').jtable({
    ui: 'mylib',
    // ...
});
```

---

## Adapter Contract

| Property / Method | Type | Required | Description |
|---|---|---|---|
| `buttonClass` | string | ✅ | CSS classes for primary action buttons. |
| `dangerButtonClass` | string | ✅ | CSS classes for delete / danger buttons. |
| `inputClass` | string | ✅ | CSS classes applied to text inputs. |
| `selectClass` | string | ✅ | CSS classes applied to `<select>` elements. |
| `textareaClass` | string | ✅ | CSS classes applied to `<textarea>` elements. |
| `checkboxClass` | string | ✅ | CSS classes applied to checkboxes. |
| `renderHeader($wrap, opts)` | function | ✅ | Render the table header bar. |
| `renderFooter($wrap, opts)` | function | ✅ | Render the table footer / pager bar. |
| `renderRowCommand($cell, cmd)` | function | ✅ | Render edit/delete buttons in each row. |
| `openDialog($modal)` | function | ✅ | Open the create/edit dialog. |
| `closeDialog($modal)` | function | ✅ | Close the create/edit dialog. |

---

## Minimal Example — Plain CSS Adapter

If you just want to apply your own plain CSS classes without a UI framework:

```javascript
jQuery.hik.jtable.adapters.register('plain', {
    buttonClass:       'btn btn-primary',
    dangerButtonClass: 'btn btn-danger',
    inputClass:        'form-input',
    selectClass:       'form-select',
    textareaClass:     'form-textarea',
    checkboxClass:     'form-checkbox',

    renderHeader:     function ($w) { $w.addClass('jtable-header'); },
    renderFooter:     function ($w) { $w.addClass('jtable-footer'); },
    renderRowCommand: function ($cell, cmd) {
        $('<button>').text(cmd.label).on('click', cmd.onClick).appendTo($cell);
    },
    openDialog:  function ($m) { $m.show(); },
    closeDialog: function ($m) { $m.hide(); }
});
```

---

## Sharing Your Adapter

If you build an adapter for a popular framework, consider contributing it back via a [Pull Request on GitHub](https://github.com/wz-shahzad/jtable-docs) so others can use it too.
