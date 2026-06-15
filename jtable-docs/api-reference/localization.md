# jTable API Reference — Localization

jTable supports full UI localization either through ready-made translation files or by supplying a custom message object.

---

## Using a Localization File

Add a localization script from the `localization/` folder of the library, immediately after the main jTable script:

```html
<script src="/Scripts/jtable/jquery.jtable.js"></script>
<script src="/Scripts/jtable/localization/jquery.jtable.tr.js"></script>
```

The example above loads the Turkish (`tr`) translation. The library ships with translations for several languages. You can also write your own and share it with the community on [GitHub](https://github.com/hikalkan/jtable).

---

## Using Custom Messages

Pass a `messages` object when initialising a single jTable instance:

```javascript
$('#MyTableContainer').jtable({
    messages: {
        serverCommunicationError: 'An error occurred while communicating with the server.',
        loadingMessage:           'Loading records...',
        // ... other keys
    }
    // other options...
});
```

To apply custom messages to **all** jTable instances on the page, extend the prototype defaults:

```javascript
$.extend(true, $.hik.jtable.prototype.options.messages, myCustomMessages);
```

See [How to set general options](./02-general-options.md#how-to-set-general-options) for more detail on prototype-level configuration.

---

## Default Messages

These are the built-in English message keys and their default values:

```javascript
messages: {
    serverCommunicationError: 'An error occured while communicating to the server.',
    loadingMessage:           'Loading records...',
    noDataAvailable:          'No data available!',
    addNewRecord:             'Add new record',
    editRecord:               'Edit Record',
    areYouSure:               'Are you sure?',
    deleteConfirmation:       'This record will be deleted. Are you sure?',
    save:                     'Save',
    saving:                   'Saving',
    cancel:                   'Cancel',
    deleteText:               'Delete',
    deleting:                 'Deleting',
    error:                    'Error',
    close:                    'Close',
    cannotLoadOptionsFor:     'Can not load options for field {0}',
    pagingInfo:               'Showing {0}-{1} of {2}',
    pageSizeChangeLabel:      'Row count',
    gotoPageLabel:            'Go to page',
    canNotDeletedRecords:     'Can not deleted {0} of {1} records!',
    deleteProggress:          'Deleted {0} of {1} records, processing...'
}
```

| Key | Description |
|---|---|
| `serverCommunicationError` | Shown when an AJAX request fails. |
| `loadingMessage` | Shown while records are being fetched. |
| `noDataAvailable` | Shown when the server returns an empty record set. |
| `addNewRecord` | Label for the "add new record" toolbar button. |
| `editRecord` | Title of the edit dialog. |
| `areYouSure` | Generic confirmation prompt. |
| `deleteConfirmation` | Delete confirmation message. |
| `save` | Save button label. |
| `saving` | Save button label while saving. |
| `cancel` | Cancel button label. |
| `deleteText` | Delete button label. |
| `deleting` | Delete button label while deleting. |
| `error` | Generic error label used in dialogs. |
| `close` | Close button label. |
| `cannotLoadOptionsFor` | Error shown when option-list loading fails. `{0}` = field name. |
| `pagingInfo` | Paging status text. `{0}` = first record, `{1}` = last record, `{2}` = total. |
| `pageSizeChangeLabel` | Label next to the page-size dropdown. |
| `gotoPageLabel` | Label next to the go-to-page input. |
| `canNotDeletedRecords` | Shown after a batch delete when some records could not be deleted. `{0}` = failed, `{1}` = total. |
| `deleteProggress` | Shown during a batch delete in progress. `{0}` = deleted so far, `{1}` = total. |

---

## Example — Turkish Localization

```javascript
var turkishMessages = {
    serverCommunicationError: 'Sunucu ile iletişim kurulurken bir hata oluştu.',
    loadingMessage:           'Kayıtlar yükleniyor...',
    noDataAvailable:          'Hiç kayıt bulunmamaktadır!',
    addNewRecord:             'Yeni kayıt ekle',
    editRecord:               'Kayıt düzenle',
    areYouSure:               'Emin misiniz?',
    deleteConfirmation:       'Bu kayıt silinecektir. Emin misiniz?',
    save:                     'Kaydet',
    saving:                   'Kaydediyor',
    cancel:                   'İptal',
    deleteText:               'Sil',
    deleting:                 'Siliyor',
    error:                    'Hata',
    close:                    'Kapat',
    cannotLoadOptionsFor:     '{0} alanı için seçenekler yüklenemedi!',
    pagingInfo:               'Görüntülenen: {0}-{1}, Toplam: {2}',
    pageSizeChangeLabel:      'Satır sayısı',
    gotoPageLabel:            'Sayfaya git',
    canNotDeletedRecords:     '{1} kayıttan {0} adedi silinemedi!',
    deleteProggress:          '{1} kayıttan {0} adedi silindi, devam ediliyor...'
};

// Apply to all instances
$.extend(true, $.hik.jtable.prototype.options.messages, turkishMessages);
```
