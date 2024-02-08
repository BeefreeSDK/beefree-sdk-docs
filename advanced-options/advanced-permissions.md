# Advanced Permissions

{% hint style="info" %}
This feature is available on Beefree SDK [Superpowers plan](https://beefree.io/bee-plugin/pricing/) and above. If you're on the Core or Essentials plan, [upgrade a development application](../readme/development-applications.md) for free to try this and other Superpowers-level features.
{% endhint %}

## Overview <a href="#overview" id="overview"></a>

With Advanced permissions, you can tailor permissions for users of your Beefree application by hiding or locking UI elements related to:

* content tiles
* content settings
* layout settings
* row & content actions (clone, delete, drag, save)
* basically anything in the editor!

These advanced permissions grant total customization of the experience you want to present. Since you set them in the configuration parameters passed to your Beefree app after you’ve initialized it, they could be different each time the editor starts, and have different setups for different users.

## Use cases <a href="#use-cases" id="use-cases"></a>

The absolute flexibility of these permissions makes it easy to address specific needs, not achievable with the [Roles and Permissions](roles-and-permissions.md) feature that is available in the Beefree SDK Console.

## **Create skill-based roles**

You can create roles that can act only on a content type. For example, you may want a “copywriter” role for people in an organization that only need to touch copy for editing or translation purposes. To do so, you can:

* hide any action that doesn’t involve working on the copy of an email or page.&#x20;
* limit style options for the text itself, by&#x20;
  * locking/hiding the side tab;
  * hiding specific settings in the text toolbar.

## **Customize image & file management workflows**

You can limit how users upload and manage images and files inside the plugin; for example, you want some users – e.g., external collaborators – to select pre-approved images and files uploaded by “admin” users. You can do so by:

* disabling drag-and-drop of images onto the stage;
* limit actions in the file manager (either the built-in one or your [custom file picker](custom-file-picker.md)) by disabling actions like upload, import, and create a folder.

Another interesting case for using advanced permissions is the possibility to set a **maximum size** **for uploads, per user**. The maximum size set per user must not exceed the **custom limitation** size set on the [Activate Custom Limitation on File Manager](../server-side-options/services-options.md). **The default limit is 20 Mb** unless otherwise stated.\
When this permission is configured, the system will check if a file exceeds the set size before uploading it; if so, the plugin will return an error message, which you may customize using [Custom languages](custom-languages.md).

## **Create custom, secondary roles**

When customers of your applications are structured businesses, typically with a headquarter and a locally-deployed organization (e.g., Real Estate, Travel, Retail), their administrators can create custom, secondary roles to match any internal policy they might have. In this scenario, admins typically want to reduce disruptions of centrally-deployed templates for external communication, while allowing a specific degree of freedom.

**Initialize different versions of the editor**

By combining multiple permissions, you can load the plugin with radically different experiences, based on the user that starts it. For example:

* a “stripped-down” version of the content builder for lower-level subscribers;
* a “simplified” version of the builder for new users of an account.

### How it works <a href="#how-it-works" id="how-it-works"></a>

To set up the advanced permissions, you will need to add the `advancedPermissions` object to `beeConfig`:

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  ...
  advancedPermissions: {
    content: {
      button: { ... },
      image: { ... },
      form: { ... },
      text: { ... },
      title: { ... },
      paragraph: { ... },
      list: { ... },
      html: { ... },
      spacer: { ... },
      icons: { ... },
      divider: { ... },
      social: { ... },
      dynamic: { ... },
      menu: { ... },
      video: { ... },
    },
    settings: {
      contentAreaWidth: { ... },
      contentAreaAlign: { ... },
      containerBackgroundColor: { ... },
      contentBackgroundColor: { ... },
      defaultFontFamily: { ... },
      linkColor: { ... },
    },
    tabs: {
      rows: { ... },
      settings: { ... },
      content: { ... }
    },
    rows: {
      behaviors: { ... },
      backgroundColorRow: { ... },
      backgroundColorContent: { ... },
      doNotStackOnMobile: { ... },
      backgroundImage: { ... },
      displayConditions: { ... },
      columnTabs: { ... },
      contentBorder: { ... },
      roundedCorners: { ... },
      verticalAlign: { ... },
  }
}

```

## Available permissions and behaviors <a href="#available-permissions-and-behaviors" id="available-permissions-and-behaviors"></a>

You can add all the permissions, some of them, or just one. It is up to your application to create them for all users or a segment, as there are no related server-side settings. You may have a different setup each time the editor starts.

All the permissions use a similar pattern, but the object must match the content schema for the type of content (described in the following section).

### Defaults

Each content type below contains a parameter for “behaviors” and “properties”. The behaviors control what someone can, or can’t, do. The properties parameter is an array of sidebar property widgets (e.g., the width slider), and each widget has its default permissions.

### **Sidebar property widget permissions**

All sidebar property widgets (e.g. width slider, alignment, color, etc.) accept the following basic permissions:

| Name   | Type    | Value         |
| ------ | ------- | ------------- |
| locked | boolean | true or false |
| show   | boolean | true or false |

Let’s look at an example of these permissions applied to an image module. The following example will hide the image width property widget and lock the text alignment widget.  We’ll cover more of the available settings below.

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  ...
  advancedPermissions: {
    content: {
      image: {
        properties: {
          imageWidth: {
            show: false,
          },
          textAlign: {
            show: true,
            locked: true
          },
        }
      },
    },
  }
}  

```

### **Default behaviors**

All contents and rows (e.g. image module, video module, stage row, etc.) accept the following basic behaviors:

| Name             | Type    | Value         | Description                                                       |
| ---------------- | ------- | ------------- | ----------------------------------------------------------------- |
| `canSelect`      | boolean | true or false | Can select a row or module to edit its properties                 |
| `canAdd`         | boolean | true or false | Can drag and drop the content tile or row onto the stage          |
| `canViewSidebar` | boolean | true or false | Can view the content in the sidebar                               |
| `canClone`       | boolean | true or false | Can clone a content or row on the stage                           |
| `canMove`        | boolean | true or false | Can drag content to another location on the stage                 |
| `canDelete`      | boolean | true or false | Can remove the content or row from the stage                      |
| `canResetMobile` | boolean | true or false | Can reset mobile style for content properties that make use of it |

Let’s look at an example of these behaviors applied to an image module. The following example will hide the image content tile on the sidebar.  We’ll cover more of the available settings below.

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  ...
  advancedPermissions: {
    content: {
      image: {
        behaviors: {
          canViewSidebar: false,
        }
      },
    },
  }
}  

```

## Components

### **filePicker**

```javascript

filePicker: {
  canUpload: true,
  maxUploadFileSize: 20 * 1024 * 1024,
  canChangeImage: true
  canApplyEffects: false, 
  canCreateFolder: false, 
  canDeleteFolder: false, 
  canDeleteFile: false, 
  canImportFile: false, 
  canSearchFreePhotos: false,
  canChangeVideo: true,
  canSearchFreeVideos: true,
}

```

### rows

```javascript

rows: {
    behaviors: {
        canSelect: true,
        canAdd: false,
        canViewSidebar: true,
        canClone: true,
        canMove: true,
        canDelete: true,
        canViewComments: true,
        canResetMobile: false,
    },
    backgroundColorContent: {
        show: true,
        locked: false
    },
    backgroundColorRow: {
        show: true,
        locked: false
    },
    backgroundImage: {
        show: true,
        locked: false
    },
    backgroundVideo: {
        show: true,
        locked: false
    },
    columnTabs: {
        show: true,
        locked: false
    },
    contentBorder: {
        show: true,
        locked: false,
    },
    displayConditions: {
        show: true,
        locked: false
    },
    doNotStackOnMobile: {
        show: true,
        locked: false
    },
    hideOnMobile: {
        show: true,
        locked: false,
    },
    roundedCorners: {
        show: true,
        locked: false,
    },
    rowLayout: {
        show: true,
        locked: false,
    },
    toolbar: {
        close: {
            show: true,
            locked: false,
        },
        save: {
            show: true,
            locked: false,
        },
        editSyncedRow: {
            show: true,
            locked: false,
        },
    },
    verticalAlign: {
        show: true,
        locked: false,
    },
}

```

### columns

```javascript

  columns: {
    behaviors: {
      canResize: true,
      canAdd: true,
      canDelete: true,
      canResetMobile: false,
    }
  },
},

```

### tabs

```javascript

tabs: {
    rows: {
      show: true,
      locked: false
    },
    settings: {
      show: true,
      locked: false
    },
    content: {
      show: true,
      locked: false
    },
  },

```

### settings

```javascript

settings: {
    contentAreaWidth: {
      show: true,
      locked: false
    },
    contentAreaAlign: {
      show: true,
      locked: false
    },
    containerBackgroundColor: {
      show: true,
      locked: false
    },
    containerBackgroundImage: {
      show: true,
      locked: false
    },
    contentBackgroundColor: {
      show: true,
      locked: false
    },
    defaultFontFamily: {
      show: true,
      locked: false
    },
    linkColor: {
      show: true,
      locked: false
    },
},

```

## Content

### **title**

```javascript

title: {
  textEditor: {
    toolbar: [
      'bold italic underline strikethrough | superscript subscript | forecolor backcolor',
      'link unlink | specialLinks | mergeTags | externalItem'
    ],
	fontSizes: '10px 12px 14px 16px 18px 20px 24px 28px',
  },
  behaviors: {
    canSelect: true,
    canAdd: false,
    canViewSidebar: true,
    canClone: true,
    canMove: true,
    canDelete: true,
    canResetMobile: false,
  },
  properties: {
    title: {
      show: true,
      locked: false
    },
	fontFamily: {
      show: true,
      locked: false
    },
	fontSize: {
      show: true,
      locked: false
    },
	textColor: {
      show: true,
      locked: false
    },
	linkColor: {
      show: true,
      locked: false
    },
	textAlign: {
      show: true,
      locked: false
    },
    lineHeight: {
      show: true,
      locked: false
    },
	letterSpacing: {
      show: true,
      locked: false
    },
	direction: {
      show: true,
      locked: false
    },
    padding: {
      show: true,
      locked: false
    },
    hideOnMobile: {
      show: true,
      locked: false
    },
  },
}

```

### **text**

```javascript

text: {
  textEditor: {
    toolbar: [
      'fontselect fontsizeselect | bold italic underline strikethrough superscript subscript removeformat | alignleft aligncenter alignright alignjustify | charmap | undo redo',
      'numlist bullist | forecolor backcolor | ltr rtl | link unlink | specialLinks | mergeTags | externalItem'
    ],
    fontSizes: '10px 12px 14px 16px 18px 20px 24px 28px',
  },
  behaviors: {
    canSelect: true,
    canAdd: false,
    canViewSidebar: true,
    canClone: true,
    canMove: true,
    canDelete: true,
    canResetMobile: false,
  },
  properties: {
    textColor: {
      show: true,
      locked: false
    },
    linkColor: {
      show: true,
      locked: false
    },
    lineHeight: {
      show: true,
      locked: false
    },
    padding: {
      show: true,
      locked: false
    },
    hideOnMobile: {
      show: true,
      locked: false
    },
  },
}

```

### **image**

```javascript

image: {
  behaviors: {
    canSelect: true,
    canAdd: false,
    canViewSidebar: true,
    canClone: true,
    canMove: true,
    canDelete: true,
    canResetMobile: false,
  },
  properties: {
    imageWidth: {
      show: true,
      locked: false
    },
    textAlign: {
      show: true,
      locked: false
    },
    dynamicImage: {
      show: true,
      locked: false
    },
    imageSelector: {
      show: true,
      locked: false
    },
    inputText: {
      show: true,
      locked: false
    },
    link: {
      show: true,
      locked: false
    },
    padding: {
      show: true,
      locked: false
    },
  }
}

```

### **button**

```javascript

button: {
  textEditor: {
    toolbar: [
      'fontselect fontsizeselect | bold italic underline strikethrough superscript subscript removeformat | undo redo | ltr rtl'
    ],
   fontSizes: '10px 12px 14px 16px 18px 20px 24px 28px',
  },
  behaviors: {
    canSelect: true,
    canAdd: false,
    canViewSidebar: true,
    canClone: true,
    canMove: true,
    canDelete: true,
    canResetMobile: false,
  },
  properties: {
    link: {
      show: true,
      locked: false
    },
    buttonWidth: {
      show: true,
      locked: false
    },
    padding: {
      show: true,
      locked: false
    },
    backgroundColor: {
      show: true,
      locked: false
    },
    textColor: {
      show: true,
      locked: false
    },
    textAlign: {
      show: true,
      locked: false
    },
    buttonLineHeight: {
      show: true,
      locked: false
    },
    borderRadius: {
      show: true,
      locked: false
    },
    contentPadding: {
      show: true,
      locked: false
    },
    border: {
      show: true,
      locked: false
    },
    hideOnMobile: {
      show: true,
      locked: false
    },
  },
}

```

### **divider**

```javascript

divider: {
  behaviors: {
    canSelect: true,
    canAdd: false,
    canViewSidebar: true,
    canClone: true,
    canMove: true,
    canDelete: true,
    canResetMobile: false,
  },
  properties: {
    textColor: {
      show: true,
      locked: false
    },
    linkColor: {
      show: true,
      locked: false
    },
    lineHeight: {
      show: true,
      locked: false
    },
    padding: {
      show: true,
      locked: false
    },
    hideOnMobile: {
      show: true,
      locked: false
    },
  },
}

```

### **social**

```javascript

social: {
  behaviors: {
    canSelect: true,
    canAdd: false,
    canViewSidebar: true,
    canClone: true,
    canMove: true,
    canDelete: true,
    canResetMobile: false,
  },
  properties: {
    iconsMode: {
      show: true,
      locked: false
    },
    icons: {
      show: true,
      locked: false
    },
    align: {
      show: true,
      locked: false
    },
    iconSpacing: {
      show: true,
      locked: false
    },
    padding: {
      show: true,
      locked: false
    },
    hideOnMobile: {
      show: true,
      locked: false
    },
  },
}

```

### **dynamic**

<pre class="language-javascript"><code class="lang-javascript">
dynamic: {
  behaviors: {
    canSelect: true,
    canAdd: false,
    canViewSidebar: true,
    canClone: true,
    canMove: true,
    canDelete: true,
    canResetMobile: false,
  },
  properties: {
    mergeContent: {
      show: true,
      locked: false
    },
    hideOnMobile: {
      show: true,
      locked: false
    },
  },
}
<strong>
</strong></code></pre>

### **html**

```javascript

html: {
  behaviors: {
    canSelect: true,
    canAdd: false,
    canViewSidebar: true,
    canClone: true,
    canMove: true,
    canDelete: true,
    canResetMobile: false,
  },
  properties: {
    htmlEditor: {
      show: true,
      locked: false
    },
    hideOnMobile: {
      show: true,
      locked: false
    },
  },
}

```

### **video (email builder block)**

```javascript

video: {
  behaviors: {
    canSelect: true,
    canAdd: false,
    canViewSidebar: true,
    canClone: true,
    canMove: true,
    canDelete: true,
    canResetMobile: false,
  },
  properties: {
    videoUrl: {
      show: true,
      locked: false
    },
    videoIcon: {
      show: true,
      locked: false
    },
    padding: {
      show: true,
      locked: false
    },
    hideOnMobile: {
      show: true,
      locked: false
    },
    padding: {
      show: true,
      locked: false
    },
  },
}

```

### **form**

```javascript

form: {
 properties: {
  editField: {
   show: false,
  },
   fontWeight: {
    show: true,
    locked: false
   }
 }
}

```

### **icon**

```javascript

icons: {
  icons: { 
    show: true,
     locked: true
   },
 properties: {
   fontWeight: {
    show: true,
    locked: false
   },
  align : { ... },
  fontFamily: { ... },
  fontSize: { ... },
  textColor: { ... },
  iconSize: { ... },
  itemsSpacing: { ... },
  iconSpacing: { ... },
  padding : { ... },
  hideOnMobile: { ... },
  hideOnAmp: { ... },
  id: { ... },
  letterSpacing: { ... },
}

```

### **paragraph**

```javascript

content: {
  paragraph: {
    properties: {
      hideOnAmp,
      hideOnMobile,
      fontFamily,
      fontSize,
      fontWeight,
      textColor,
      linkColor,
      padding,
      lineHeight,
      textAlign,
      id,
      direction,
      letterSpacing,
      paragraphSpacing,
      aiIntegration,
    },
    textEditor: {
      toolbar: [
        'bold italic underline strikethrough | superscript subscript removeformat | forecolor backcolor | charmap',
        'nonbreaking |  link unlink | specialLinks | mergeTags | externalItem | externalTags',      
      ],
    },
  },
}

```

### **list**

```javascript

content: {
  list: {
    properties: {
      tag,
      listStyleType,
      hideOnAmp,
      hideOnMobile,
      fontFamily,
      fontSize,
      fontWeight,
      textColor,
      linkColor,
      padding,
      lineHeight,
      textAlign,
      id,
      direction,
      letterSpacing,
      startList,
      liSpacing,
      liIndent,
    },
    textEditor: {
      toolbar: [
        'bold italic underline strikethrough | superscript subscript removeformat | forecolor backcolor | outdent indent | nonbreaking | charmap',
        ' link unlink | specialLinks | mergeTags | externalItem | externalTags',      
      ],
    },
  },
}

```

### **linktypes**

```javascript

linkTypes: {
      webAddress: {
        show: true,
      },
      emailAddress: {
        show: true,
      },
      telephone: {
        show: false,
      },
      text: {
        show: false,
      },
      anchor: {
        show: false,
      },
    },

```

### **menu**

```javascript

menu: {
  behaviors: {
    canSelect: true,
    canAdd: false,
    canViewSidebar: true,
    canClone: true,
    canMove: true,
    canDelete: true,
    canResetMobile: false,
  },
  properties: {
    menuItems: {
      show: true,
      locked: false
    },
    fontFamily: {
      show: true,
      locked: false
    },
    fontWeight: {
      show: true,
      locked: false
    },
    fontSize: {
      show: true,
      locked: false
    },
    textColor: {
      show: true,
      locked: false
    },
    linkColor: {
      show: true,
      locked: false
    },
    align: {
      show: true,
      locked: false
    },
    layout: {
      show: true,
      locked: false
    },
    separator: {
      show: true,
      locked: false
    },
    hamburger: {
      show: true,
      locked: false
    },
    itemSpacing: {
      show: true,
      locked: false
    },
    padding: {
      show: true,
      locked: false
    },
    hideOnMobile: {
      show: true,
      locked: false
    },
    id: {
      show: true,
      locked: false
    },
    letterSpacing: {
      show: true,
      locked: false
    }
  }
}

```

### **addon**

To assign permissions, you can make use of the addon’s ID. Based on the type of addon, you can assign relevant permissions. For instance, if your addon is an image type, you can assign permissions specific to the image content block. The advanced permissions structure will be as follows:

```javascript

image: { /**/ },
button: { /**/ },
social: { /**/ },
addon: {
  'addons-id': { /**/ },
}

```

```javascript

addon: {
  'b17dc240-b226-415c-af71-246fc51bd088': { /**/ 
    behaviors: {
      canViewSidebar: true,
    },
  },
}

```

## Add Condition and Edit Condition Buttons

You can choose to display or hide the "Add Condition" and "Edit Condition" buttons when using the [Content Dialog](content-dialog.md) with [Display Conditions](display-conditions.md).

The following code shows an example config for how you can display or hide these buttons using advanced permissions.

```json
{
...
  rows: {
    displayConditions: {
      CanEditDisplayConditions: false,
      CanSelectDisplayConditions: false,
    },
  },
...
}
```

To hide the buttons, set the `CanEditDisplayConditions` and `CanSelectDisplayConditions` parameters to `false`.&#x20;

## Role templates <a href="#role-templates" id="role-templates"></a>

We’ve put together a few JSON templates of custom roles created with Advanced permissions, so you can get started experimenting with this powerful feature.

You can find them in our [GitHub account.](https://github.com/BEE-Plugin/bee-advanced-permissions)
