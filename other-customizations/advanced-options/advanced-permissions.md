# Advanced Permissions

{% hint style="info" %}
This feature is available on Beefree SDK [Superpowers plan](https://beefree.io/bee-plugin/pricing/) and above. If you're on the Core or Essentials plan, [upgrade a development application](../../getting-started/readme/development-applications.md) for free to try this and other Superpowers-level features.
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

Another interesting case for using advanced permissions is the possibility to set a **maximum size** **for uploads, per user**. The maximum size set per user must not exceed the **custom limitation** size set on the [Activate Custom Limitation on File Manager](../../server-side-configurations/server-side-options/services-options.md). **The default limit is 20 Mb** unless otherwise stated.\
When this permission is configured, the system will check if a file exceeds the set size before uploading it; if so, the plugin will return an error message, which you may customize using [Custom languages](custom-languages.md).

## **Create custom, secondary roles**

When customers of your applications are structured businesses, typically with a headquarter and a locally-deployed organization (e.g., Real Estate, Travel, Retail), their administrators can create custom, secondary roles to match any internal policy they might have. In this scenario, admins typically want to reduce disruptions of centrally-deployed templates for external communication, while allowing a specific degree of freedom.

**Initialize different versions of the editor**

By combining multiple permissions, you can load the plugin with radically different experiences, based on the user that starts it. For example:

* a “stripped-down” version of the content builder for lower-level subscribers;
* a “simplified” version of the builder for new users of an account.

### How it works <a href="#how-it-works" id="how-it-works"></a>

To set up the advanced permissions, you will need to add the `advancedPermissions` object to `beeConfig.`&#x20;

{% hint style="info" %}
**Note:** Click on the arrow next to the section title in the following section to expand the following sections and reference its corresponding content.
{% endhint %}

<details>

<summary>Steps to set up advanced permissions in your beeConfig</summary>

Take the following steps to set up **advanced permissions** in your `beeConfig` for Beefree SDK:

1. **Locate your `beeConfig` object:** This is where you configure the Beefree SDK with its basic settings, such as the user ID and container.
2. **Add the `advancedPermissions` object:** You will need to insert the `advancedPermissions` object within your `beeConfig` to specify which content types and settings can be customized with specific permissions.
3. **Define `content` permissions:** Inside `advancedPermissions`, you can specify what content blocks (e.g., `image`, `button`, `text`) are visible and what actions are allowed.
4. **Configure `settings` permissions:** This controls settings like content area width, background color, or fonts for different blocks.
5. **Control `tabs` visibility:** You can manage which tabs (such as rows or settings) are visible and editable in the editor interface.&#x20;
6. **Set `rows` behaviors:** You can control row-specific permissions, such as adding or hiding rows, background colors, and mobile visibility.
7. **Test the configuration:** After adding the `advancedPermissions` object to your `beeConfig`, test your configuration by launching the editor and checking if the permissions are applied correctly (e.g., specific settings are visible or locked as intended).

</details>

<details>

<summary>Sample code</summary>

Reference the following sample code to understand the structure of `advancedPermissions`.&#x20;

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    content: {
      button: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          link: { locked: false, show: true },
          buttonWidth: { locked: false, show: true },
          padding: { locked: false, show: true },
          backgroundColor: { locked: false, show: true },
          textColor: { locked: false, show: true },
          textAlign: { locked: false, show: true },
          buttonLineHeight: { locked: false, show: true },
          borderRadius: { locked: false, show: true },
          contentPadding: { locked: false, show: true },
          border: { locked: false, show: true },
          hideOnMobile: { locked: false, show: true },
          hideOnAmp: { locked: false, show: false }
        },
        textEditor: { toolbar: "bold italic underline" }
      },
      image: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          imageWidth: { locked: false, show: true },
          textAlign: { locked: false, show: true },
          dynamicImage: { locked: false, show: true },
          imageSelector: { locked: false, show: true },
          inputText: { locked: false, show: true },
          link: { locked: false, show: true },
          padding: { locked: false, show: true },
          hideOnMobile: { locked: false, show: true },
          hideOnAmp: { locked: false, show: false },
          borderRadius: { locked: false, show: true },
          id: { locked: false, show: true },
          customAttributes: { locked: false, show: true }
        }
      },
      // Repeat structure for other elements: form, text, title, etc.
    },
    settings: {
      contentAreaWidth: { locked: false, show: true },
      contentAreaAlign: { locked: false, show: true },
      containerBackgroundColor: { locked: false, show: true },
      contentBackgroundColor: { locked: false, show: true },
      defaultFontFamily: { locked: false, show: true },
      linkColor: { locked: false, show: true }
    },
    tabs: {
      rows: { locked: false, show: true },
      settings: { locked: false, show: true },
      content: { locked: false, show: true }
    },
    rows: {
      behaviors: {
        canSelect: true,
        canAdd: true,
        canViewSidebar: true,
        hiddenOnAmp: false,
        hiddenOnHtml: false,
        hiddenOnMobile: false,
        hiddenOnDesktop: false,
        canResize: true,
        canResetMobile: true
      },
      backgroundColorRow: { locked: false, show: true },
      backgroundVideo: { locked: false, show: true },
      backgroundColorContent: { locked: false, show: true },
      doNotStackOnMobile: { locked: false, show: true },
      hideOnMobile: { locked: false, show: true },
      backgroundImage: { locked: false, show: true },
      displayConditions: { locked: false, show: true },
      rowLayout: { locked: false, show: true },
      columnTabs: { locked: false, show: true },
      contentBorder: { locked: false, show: true },
      roundedCorners: { locked: false, show: true },
      verticalAlign: { locked: false, show: true },
      columnsSpacing: { show: true, locked: false },
      columnsBorderRadius: { show: true, locked: false }
    }
  },
  components: {
    filePicker: {
      canApplyEffects: true,
      canChangeImage: true,
      canChangeVideo: true,
      canCreateFolder: true,
      canDeleteFile: true,
      canDeleteFolder: true,
      canImportFile: true,
      canSearchFreePhotos: true,
      canSearchFreeVideos: true,
      canUpload: true,
      maxUploadFileSize: 20971520
    },
    linkTypes: {
      webAddress: { show: true },
      emailAddress: { show: true },
      telephone: { show: true },
      text: { show: true },
      anchor: { show: true }
    }
  },
  rowAddon: {
    customRowAddonHandle: {
      behaviors: {
        canSelect: true,
        canAdd: true,
        canViewSidebar: true,
        hiddenOnAmp: false,
        hiddenOnHtml: false,
        hiddenOnMobile: false,
        hiddenOnDesktop: false,
        canResize: true,
        canResetMobile: true
      }
    }
  },
  workspace: {
    stageToggle: { locked: false, show: true },
    historyButtons: { show: true }
  }
}
```

</details>

### First-level fields <a href="#available-permissions-and-behaviors" id="available-permissions-and-behaviors"></a>

The following table provides the name, data type, description, and an example value for the first-level fields for `advancedPermissions`.

| Name                   | Data Type | Description                                                                      | Example Value                                  |
| ---------------------- | --------- | -------------------------------------------------------------------------------- | ---------------------------------------------- |
| `uid`                  | `string`  | Unique identifier for the CMS user (mandatory).                                  | `'CmsUserName'`                                |
| `container`            | `string`  | HTML container element ID for embedding the BEE plugin (mandatory).              | `'bee-plugin-container'`                       |
| `advanced permissions` | `object`  | Contains settings for content elements, rows, settings, and tabs configurations. | See configuration object for details.          |
| `components`           | `object`  | Specifies available components like file picker and link types.                  | `{ filePicker: {...}, linkTypes: {...} }`      |
| `rowAddOn`             | `object`  | Settings for custom row add-ons, such as custom behaviors.                       | `{ customRowAddonHandle: {...} }`              |
| `workspace`            | `object`  | Defines workspace settings, such as stage toggle and history buttons visibility. | `{ stageToggle: {...}, historyButtons: true }` |

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
  advancedPermissions: {
    content: {
      image: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          imageWidth: {
            locked: false,
            show: false
          },
          textAlign: {
            locked: true,
            show: true
          },
          dynamicImage: {
            locked: false,
            show: true
          },
          imageSelector: {
            locked: false,
            show: true
          },
          inputText: {
            locked: false,
            show: true
          },
          link: {
            locked: false,
            show: true
          },
          padding: {
            locked: false,
            show: true
          },
          hideOnMobile: {
            locked: false,
            show: true
          },
          hideOnAmp: {
            locked: false,
            show: false
          },
          borderRadius: {
            locked: false,
            show: true
          },
          id: {
            locked: false,
            show: true
          },
          customAttributes: {
            locked: false,
            show: true
          }
        }
      }
    }
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

## Components

The **`components`** object lets you control the behavior and permissions for tools like file pickers and link types within the editor. You can define what actions users can take, such as uploading or deleting files, and specify which link types (e.g., web addresses, emails) are available. This section provides more information on the component object within advanced permissions.

### **filePicker**

The following code provides an example of the `filePicker` object.

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    components: {
      filePicker: {
        canApplyEffects: true,
        canChangeImage: true,
        canChangeVideo: true,
        canCreateFolder: true,
        canDeleteFile: true,
        canDeleteFolder: true,
        canImportFile: true,
        canSearchFreePhotos: true,
        canSearchFreeVideos: true,
        canUpload: true,
        maxUploadFileSize: 20971520 // 20 MB
      }
    }
  }
}

```

### **linktypes**

The following code provides an example of the `linkTypes` object.

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    components: {
      linkTypes: {
        webAddress: {
          show: true
        },
        emailAddress: {
          show: true
        },
        telephone: {
          show: true
        },
        text: {
          show: true
        },
        anchor: {
          show: true
        }
      }
    }
  }
}

```

## Rows

The **`rows`** object in **Beefree SDK** allows you to manage the behavior and appearance of rows in the editor. You can control what users can do with rows, such as adding, deleting, or moving them. Additionally, you can set permissions for properties like background color, stacking behavior on mobile, and visibility settings. Configuring the **`rows`** object ensures users can work with rows in a controlled way, customizing their content without altering crucial layout elements.

### Rows Addon

The following code demonstrates how to specify behavior settings for individual row addons. A custom row addon can have its behaviors set independently from the global row settings.

```javascript
beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    rows: {
      behaviors: {
        canSelect: true,
        canAdd: true,
        canViewSidebar: true,
        hiddenOnAmp: false,
        hiddenOnHtml: false,
        hiddenOnMobile: false,
        hiddenOnDesktop: false,
        canResize: true,
        canResetMobile: true
      },
      backgroundColorRow: {
        locked: false,
        show: true
      },
      backgroundVideo: {
        locked: false,
        show: true
      },
      backgroundColorContent: {
        locked: false,
        show: true
      },
      doNotStackOnMobile: {
        locked: false,
        show: true
      },
      hideOnMobile: {
        locked: false,
        show: true
      },
      backgroundImage: {
        locked: false,
        show: true
      },
      displayConditions: {
        locked: false,
        show: true
      },
      rowLayout: {
        locked: false,
        show: true
      },
      columnTabs: {
        locked: false,
        show: true
      },
      contentBorder: {
        locked: false,
        show: true
      },
      roundedCorners: {
        locked: false,
        show: true
      },
      verticalAlign: {
        locked: false,
        show: true
      },
      columnsSpacing: {
        show: true,
        locked: false
      },
      columnsBorderRadius: {
        show: true,
        locked: false
      }
    },
    rowAddon: {
      customRowAddonHandle: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        }
      }
    }
  }
}

```

## Columns

The **`columns`** object in the **Beefree SDK** lets you control the behavior and permissions for columns within the editor. You can define what users can do with columns, such as adding, selecting, moving, or deleting them. You can also set properties like column spacing and border radius. Configuring the **`columns`** object ensures that users can manage column layouts effectively, while maintaining control over the design and structure of the content.

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    columns: {
      behaviors: {
        canSelect: true,
        canAdd: true,
        canViewSidebar: true,
        canDelete: true,
        hiddenOnAmp: false,
        hiddenOnHtml: false,
        hiddenOnMobile: false,
        hiddenOnDesktop: false,
        canResize: true,
        canResetMobile: true
      },
      padding: {
        locked: false,
        show: true
      },
      backgroundColor: {
        locked: false,
        show: true
      },
      backgroundImage: {
        locked: false,
        show: true
      },
      verticalAlign: {
        locked: false,
        show: true
      },
      borderRadius: {
        locked: false,
        show: true
      },
      contentAlign: {
        locked: false,
        show: true
      }
    }
  }
}


```

## Tabs

The **`tabs`** object in the **Beefree SDK** allows you to manage the visibility and permissions of different tabs within the editor, such as the **Rows**, **Content**, and **Settings** tabs. You can control which tabs users can access and whether they can interact with them. By configuring the **`tabs`** object, you streamline the editor’s interface, ensuring users have access to only the relevant tabs they need for editing while maintaining control over what they can modify.

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    tabs: {
      rows: {
        locked: false,
        show: true
      },
      settings: {
        locked: false,
        show: true
      },
      content: {
        locked: false,
        show: true
      }
    }
  }
}


```

## Settings

The **`settings`** object in the **Beefree SDK** allows you to control various design-related settings within the editor, such as content area width, background colors, and default font styles. You can define which settings users can view or modify, such as enabling or locking background images or link colors. By configuring the **`settings`** object, you ensure that users can customize specific design elements while maintaining overall control over the layout and style of the content.

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    settings: {
      contentAreaWidth: {
        locked: false,
        show: true
      },
      contentAreaAlign: {
        locked: false,
        show: true
      },
      containerBackgroundColor: {
        locked: false,
        show: true
      },
      contentBackgroundColor: {
        locked: false,
        show: true
      },
      containerBackgroundImage: {
        locked: false,
        show: true
      },
      defaultFontFamily: {
        locked: false,
        show: true
      },
      linkColor: {
        locked: false,
        show: true
      },
      title: {
        locked: false,
        show: true
      },
      description: {
        locked: false,
        show: true
      },
      language: {
        locked: false,
        show: true
      },
      favicon: {
        locked: false,
        show: true
      }
    }
  }
}


```

## Content

The **`content`** object in the **Beefree SDK** controls the behavior and permissions for different types of content blocks, such as text, images, buttons, and more. You can specify what users can do with each content type, such as adding, editing, or selecting them, and set properties like alignment, padding, and visibility. By configuring the **`content`** object, you allow users to interact with content blocks while maintaining control over how each element can be modified within the design.

### **Title**

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    content: {
      title: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          direction: {
            locked: false,
            show: true
          },
          heading: {
            locked: false,
            show: true
          },
          title: {
            locked: false,
            show: true
          },
          textAlign: {
            locked: false,
            show: true
          },
          fontSize: {
            locked: false,
            show: true
          },
          fontWeight: {
            locked: false,
            show: true
          },
          fontFamily: {
            locked: false,
            show: true
          },
          letterSpacing: {
            locked: false,
            show: true
          },
          textColor: {
            locked: false,
            show: true
          },
          linkColor: {
            locked: false,
            show: true
          },
          lineHeight: {
            locked: false,
            show: true
          },
          padding: {
            locked: false,
            show: true
          },
          hideOnMobile: {
            locked: false,
            show: true
          },
          hideOnAmp: {
            locked: false,
            show: false
          },
          id: {
            locked: false,
            show: true
          },
          aiIntegration: {
            locked: false,
            show: true
          }
        },
        textEditor: {
          toolbar: "bold italic underline"
        }
      }
    }
  }
}


```

### **Text**

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    content: {
      text: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          textColor: {
            locked: false,
            show: true
          },
          linkColor: {
            locked: false,
            show: true
          },
          lineHeight: {
            locked: false,
            show: true
          },
          padding: {
            locked: false,
            show: true
          },
          hideOnMobile: {
            locked: false,
            show: true
          },
          hideOnAmp: {
            locked: false,
            show: false
          },
          id: {
            locked: false,
            show: true
          },
          letterSpacing: {
            locked: false,
            show: true
          }
        },
        textEditor: {
          toolbar: "bold italic underline"
        }
      }
    }
  }
}


```

### **Image**

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    content: {
      image: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          imageWidth: {
            locked: false,
            show: true
          },
          textAlign: {
            locked: false,
            show: true
          },
          dynamicImage: {
            locked: false,
            show: true
          },
          imageSelector: {
            locked: false,
            show: true
          },
          inputText: {
            locked: false,
            show: true
          },
          link: {
            locked: false,
            show: true
          },
          padding: {
            locked: false,
            show: true
          },
          hideOnMobile: {
            locked: false,
            show: true
          },
          hideOnAmp: {
            locked: false,
            show: false
          },
          borderRadius: {
            locked: false,
            show: true
          },
          id: {
            locked: false,
            show: true
          },
          customAttributes: {
            locked: false,
            show: true
          }
        }
      }
    }
  }
}


```

### **Button**

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    content: {
      button: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          link: {
            locked: false,
            show: true
          },
          buttonWidth: {
            locked: false,
            show: true
          },
          padding: {
            locked: false,
            show: true
          },
          backgroundColor: {
            locked: false,
            show: true
          },
          textColor: {
            locked: false,
            show: true
          },
          textAlign: {
            locked: false,
            show: true
          },
          buttonLineHeight: {
            locked: false,
            show: true
          },
          borderRadius: {
            locked: false,
            show: true
          },
          contentPadding: {
            locked: false,
            show: true
          },
          border: {
            locked: false,
            show: true
          },
          hideOnMobile: {
            locked: false,
            show: true
          },
          hideOnAmp: {
            locked: false,
            show: false
          }
        },
        textEditor: {
          toolbar: "bold italic underline"
        }
      }
    }
  }
}


```

### **Divider**

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    content: {
      divider: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          dividerMode: {
            locked: false,
            show: true
          },
          padding: {
            locked: false,
            show: true
          },
          hideOnMobile: {
            locked: false,
            show: true
          },
          hideOnAmp: {
            locked: false,
            show: false
          },
          id: {
            locked: false,
            show: true
          }
        }
      }
    }
  }
}

```

### **Social**

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    content: {
      social: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          iconsMode: {
            locked: false,
            show: true
          },
          icons: {
            locked: false,
            show: true
          },
          align: {
            locked: false,
            show: true
          },
          iconSpacing: {
            locked: false,
            show: true
          },
          padding: {
            locked: false,
            show: true
          },
          hideOnMobile: {
            locked: false,
            show: true
          },
          hideOnAmp: {
            locked: false,
            show: false
          },
          id: {
            locked: false,
            show: true
          }
        }
      }
    }
  }
}

```

### **Dynamic**

<pre class="language-javascript"><code class="lang-javascript">
beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    content: {
      dynamic: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          mergeContent: {
            locked: false,
            show: true
          },
          hideOnMobile: {
            locked: false,
            show: true
          },
          hideOnAmp: {
            locked: false,
            show: false
          },
          id: {
            locked: false,
            show: true
          }
        }
      }
    }
  }
}

<strong>
</strong></code></pre>

### **Html**

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    content: {
      html: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          htmlEditor: {
            locked: false,
            show: true
          },
          hideOnMobile: {
            locked: false,
            show: true
          },
          hideOnAmp: {
            locked: false,
            show: false
          },
          id: {
            locked: false,
            show: true
          }
        }
      }
    }
  }
}

```

### **Video (email builder block)**

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    content: {
      video: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          videoUrl: {
            locked: false,
            show: true
          },
          videoIcon: {
            locked: false,
            show: true
          },
          padding: {
            locked: false,
            show: true
          },
          hideOnMobile: {
            locked: false,
            show: true
          },
          hideOnAmp: {
            locked: false,
            show: false
          },
          id: {
            locked: false,
            show: true
          },
          customAttributes: {
            locked: false,
            show: true
          }
        }
      }
    }
  }
}


```

### **Form**

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    content: {
      form: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          beeButton: {
            locked: false,
            show: true
          },
          layOutFields: {
            locked: false,
            show: true
          },
          width: {
            locked: false,
            show: true
          },
          textAlign: {
            locked: false,
            show: true
          },
          fontFamily: {
            locked: false,
            show: true
          },
          fontSize: {
            locked: false,
            show: true
          },
          fontWeight: {
            locked: false,
            show: true
          },
          labelTextColor: {
            locked: false,
            show: true
          },
          labelLineHeight: {
            locked: false,
            show: true
          },
          labelTextAlign: {
            locked: false,
            show: true
          },
          fieldTextColor: {
            locked: false,
            show: true
          },
          fieldBackgroundColor: {
            locked: false,
            show: true
          },
          fieldPadding: {
            locked: false,
            show: true
          },
          buttonWidth: {
            locked: false,
            show: true
          },
          buttonTextColor: {
            locked: false,
            show: true
          },
          buttonBackgroundColor: {
            locked: false,
            show: true
          },
          buttonAlign: {
            locked: false,
            show: true
          },
          buttonPadding: {
            locked: false,
            show: true
          },
          padding: {
            locked: false,
            show: true
          },
          hideOnMobile: {
            locked: false,
            show: true
          },
          hideOnAmp: {
            locked: false,
            show: false
          },
          id: {
            locked: false,
            show: true
          }
        }
      }
    }
  }
}


```

### **Icon**

You should use the Icon object to set advanced permissions when you need granular control over the display and behavior of icon elements. This allows you to lock certain properties, such as the visibility and font weight, ensuring consistency across different devices and user interactions. Additionally, setting these permissions helps in maintaining a cohesive design by managing how icons respond to mobile and AMP environments.

```javascript
beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    content: {
      icons: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          icons: {
            locked: false,
            show: true
          },
          align: {
            locked: false,
            show: true
          },
          fontFamily: {
            locked: false,
            show: true
          },
          fontSize: {
            locked: false,
            show: true
          },
          fontWeight: {
            locked: false,
            show: true
          },
          textColor: {
            locked: false,
            show: true
          },
          iconSize: {
            locked: false,
            show: true
          },
          itemsSpacing: {
            locked: false,
            show: true
          },
          iconSpacing: {
            locked: false,
            show: true
          },
          letterSpacing: {
            locked: false,
            show: true
          },
          padding: {
            locked: false,
            show: true
          },
          hideOnMobile: {
            locked: false,
            show: true
          },
          hideOnAmp: {
            locked: false,
            show: true
          },
          id: {
            locked: false,
            show: true
          }
        }
      }
    }
  }
}

```

#### Icon Configuration Elements

In the given icon code, the structure is defined using objects, properties, and parameters to represent a detailed configuration. The main object, `icons`, encompasses two primary properties: `behaviors` and `properties`, each of which is an object itself. The `behaviors` object contains a property `canResetMobile` with a boolean parameter set to `false`, indicating a specific behavior setting. The `properties` object holds various properties such as `icons`, `fontWeight`, `align`, and more, each representing different characteristics and settings for the icons. Each of these properties has parameters assigned to them; for instance, the `icons` property has `show` and `locked` parameters set to `true`, determining the visibility and lock status of the icons. This nested structure using objects and properties with defined parameters represent the configuration settings in the code.

#### Behaviors Object

The table below outlines the configuration elements, their data types, descriptions, and default values for the behaviors object used in the icon configuration.

<table><thead><tr><th width="224">Configuration Elements</th><th>Data Type</th><th>Description</th><th>Default Value</th></tr></thead><tbody><tr><td><strong>canResetMobile</strong></td><td>boolean</td><td>Indicates whether icons can reset to default settings on mobile devices.</td><td>false</td></tr></tbody></table>

#### Properties Object

The table below outlines the configuration elements, their data types, descriptions, and default values for the properties object used in the icon configuration.

<table><thead><tr><th width="228">Configuration Elements</th><th>Data Type</th><th>Description</th><th>Default Value</th></tr></thead><tbody><tr><td><code>icons</code></td><td>object</td><td></td><td></td></tr><tr><td><code>show</code></td><td>boolean</td><td>Determines if the icons are visible.</td><td>true</td></tr><tr><td><code>locked</code></td><td>boolean</td><td>Indicates if the icons' visibility setting is locked.</td><td>true</td></tr><tr><td><code>fontWeight</code></td><td>object</td><td></td><td></td></tr><tr><td><code>show</code></td><td>boolean</td><td>Determines if the font weight option is visible for icons.</td><td>true</td></tr><tr><td><code>locked</code></td><td>boolean</td><td>Indicates if the font weight option is locked.</td><td>false</td></tr><tr><td><code>align</code></td><td>object</td><td>Aligns icons within their container.</td><td>NA</td></tr><tr><td><code>fontFamily</code></td><td>object</td><td>Sets the font family for icon labels.</td><td>NA</td></tr><tr><td><code>fontSize</code></td><td>object</td><td>Sets the font size for icon labels.</td><td>NA</td></tr><tr><td><code>textColor</code></td><td>object</td><td>Sets the text color for icon labels.</td><td>NA</td></tr><tr><td><code>iconSize</code></td><td>object</td><td>Sets the size of the icons.</td><td>NA</td></tr><tr><td><code>itemsSpacing</code></td><td>object</td><td>Sets the spacing between multiple icons.</td><td>NA</td></tr><tr><td><code>iconSpacing</code></td><td>object</td><td>Sets the spacing around individual icons.</td><td>NA</td></tr><tr><td><code>padding</code></td><td>object</td><td>Sets the padding around icons.</td><td>NA</td></tr><tr><td><code>hideOnMobile</code></td><td>object</td><td>Hides icons on mobile devices.</td><td>NA</td></tr><tr><td><code>hideOnAmp</code></td><td>object</td><td>Hides icons on AMP-format pages.</td><td>NA</td></tr><tr><td><code>id</code></td><td>object</td><td>Sets a unique identifier for icons.</td><td>NA</td></tr><tr><td><code>letterSpacing</code></td><td>object</td><td>Sets the space between letters in icon labels.</td><td>NA</td></tr></tbody></table>

### **Paragraph**

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    content: {
      paragraph: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          direction: {
            locked: false,
            show: true
          },
          paragraphSpacing: {
            locked: false,
            show: true
          },
          textAlign: {
            locked: false,
            show: true
          },
          fontSize: {
            locked: false,
            show: true
          },
          fontWeight: {
            locked: false,
            show: true
          },
          fontFamily: {
            locked: false,
            show: true
          },
          letterSpacing: {
            locked: false,
            show: true
          },
          textColor: {
            locked: false,
            show: true
          },
          linkColor: {
            locked: false,
            show: true
          },
          lineHeight: {
            locked: false,
            show: true
          },
          padding: {
            locked: false,
            show: true
          },
          hideOnMobile: {
            locked: false,
            show: true
          },
          hideOnAmp: {
            locked: false,
            show: false
          },
          id: {
            locked: false,
            show: true
          },
          aiIntegration: {
            locked: false,
            show: true
          }
        },
        textEditor: {
          toolbar: "bold italic underline"
        }
      }
    }
  }
}


```

### **List**

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    content: {
      list: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          direction: {
            locked: false,
            show: true
          },
          textAlign: {
            locked: false,
            show: true
          },
          tag: {
            locked: false,
            show: true
          },
          listStyleType: {
            locked: false,
            show: true
          },
          startList: {
            locked: false,
            show: true
          },
          liSpacing: {
            locked: false,
            show: true
          },
          liIndent: {
            locked: false,
            show: true
          },
          aiIntegration: {
            locked: false,
            show: true
          },
          fontSize: {
            locked: false,
            show: true
          },
          fontWeight: {
            locked: false,
            show: true
          },
          fontFamily: {
            locked: false,
            show: true
          },
          letterSpacing: {
            locked: false,
            show: true
          },
          textColor: {
            locked: false,
            show: true
          },
          linkColor: {
            locked: false,
            show: true
          },
          lineHeight: {
            locked: false,
            show: true
          },
          padding: {
            locked: false,
            show: true
          },
          hideOnMobile: {
            locked: false,
            show: true
          },
          hideOnAmp: {
            locked: false,
            show: false
          },
          id: {
            locked: false,
            show: true
          }
        },
        textEditor: {
          toolbar: "bold italic underline"
        }
      }
    }
  }
}


```

### **Menu**

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    content: {
      menu: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          menuItems: {
            locked: false,
            show: true
          },
          fontFamily: {
            locked: false,
            show: true
          },
          fontSize: {
            locked: false,
            show: true
          },
          fontWeight: {
            locked: false,
            show: true
          },
          letterSpacing: {
            locked: false,
            show: true
          },
          textColor: {
            locked: false,
            show: true
          },
          linkColor: {
            locked: false,
            show: true
          },
          align: {
            locked: false,
            show: true
          },
          layout: {
            locked: false,
            show: true
          },
          separator: {
            locked: false,
            show: true
          },
          hamburger: {
            locked: false,
            show: true
          },
          itemSpacing: {
            locked: false,
            show: true
          },
          padding: {
            locked: false,
            show: true
          },
          hideOnMobile: {
            locked: false,
            show: true
          },
          id: {
            locked: false,
            show: true
          }
        }
      }
    }
  }
}


```

### Table

```javascript
beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  advancedPermissions: {
    content: {
      table: {
        behaviors: {
          canSelect: true,
          canAdd: true,
          canViewSidebar: true,
          hiddenOnAmp: false,
          hiddenOnHtml: false,
          hiddenOnMobile: false,
          hiddenOnDesktop: false,
          canResize: true,
          canResetMobile: true
        },
        properties: {
          columns: {
            locked: false,
            show: true
          },
          rows: {
            locked: false,
            show: true
          },
          backgroundColor: {
            locked: false,
            show: true
          },
          border: {
            locked: false,
            show: true
          },
          textColor: {
            locked: false,
            show: true
          },
          linkColor: {
            locked: false,
            show: true
          },
          fontFamily: {
            locked: false,
            show: true
          },
          fontWeight: {
            locked: false,
            show: true
          },
          fontSize: {
            locked: false,
            show: true
          },
          textAlign: {
            locked: false,
            show: true
          },
          lineHeight: {
            locked: false,
            show: true
          },
          letterSpacing: {
            locked: false,
            show: true
          },
          direction: {
            locked: false,
            show: true
          },
          padding: {
            locked: false,
            show: true
          },
          hideOnMobile: {
            locked: false,
            show: true
          },
          hideOnAmp: {
            locked: false,
            show: true
          },
          id: {
            locked: false,
            show: true
          },
          alternateRowBackgroundColor: {
            locked: false,
            show: true
          },
          headers: {
            locked: false,
            show: true
          }
        },
        textEditor: {
          toolbar: "bold italic underline"
        }
      }
    }
  }
}

```

## **Addon**

In this section, we will explore how to assign advanced permissions and behaviors for various AddOn types, specifically focusing on how to customize permissions for [Custom AddOns](../../builder-addons/addons/custom-addons/) and [Row AddOns](advanced-permissions.md#rows-addon). These permissions can override default settings to provide granular control. For instance, an image addon can have specific permissions different from the default image block permissions.

To successfully use this feature, follow these steps:

1. **Identify the AddOn ID:** Obtain the unique ID of the addon you wish to assign permissions to.
2. **Define Custom Permissions:** Based on the type of addon, assign relevant permissions in your configuration file.
3. **Override Default Permissions:** Specify advanced permissions for the addon, ensuring they override the default ones if needed.
4. **Set Specific Behaviors:** For row addons, include permissions for individual modules like image blocks inside the row addon.
5. **Apply Global Restrictions:** Optionally, set global restrictions for all mixed and row content addons for consistent behavior.

By following these steps, you can effectively manage and customize addon permissions.

The following code provides an example of the different content modules and the `addons-id`.

```javascript
content: {
  image: { /**/ }, // The image block allows you to add and configure images in your content.
  button: { /**/ }, // The button block provides options for adding and styling call-to-action buttons.
  social: { /**/ }, // The social block enables you to include social media icons for sharing or linking.
  addon: {
    // The addon block supports custom addons content, such as custom images or mixed content addons.
    customImageHandle: { /**/ }, // A custom image addon to manage and configure image properties.
    customRowAddonHandle: { /**/ } // A custom row addon for managing entire row behaviors and properties.
  }
}
```

The following code shows an example AddOn with the `canViewSidebar` behavior set to `true`.

```javascript

content: {
  addon: {
    // This is where you define custom addons, such as a custom images addon.
    customImageHandle: {
      behaviors: {
        canViewSidebar: true, // Specifies that the sidebar is visible for this custom image addon.
      },
    },
  }
}

```

### Module inside row addon

The following code defines specific permissions and behaviors for different modules within a Row AddOn.&#x20;

```javascript
content: {
  addon: {
    // This block allows the addition of custom addons and controls their behaviors.
    customImageHandle: {
      behaviors: {
        canViewSidebar: true, // Enables the sidebar for this specific addon.
      },
    },
    customRowAddonHandle: {
      // Custom row-specific behaviors and permissions for an addon inside a row.
      behaviors: {
        canAdd: true, // Allows adding a new row.
        canClone: false, // Disables cloning of this row.
        canDelete: false // Disables deleting of this row.
      },
      image: {
        // Controls behaviors and properties for image modules within this row addon.
        behaviors: {
          canSelect: true // Allows image selection inside the row addon.
        },
        properties: {
          textAlign: {
            show: false // Hides the text alignment control for images in this row addon.
          }
        }
      }
    },
    mixed: {
      // Handles behaviors for mixed content addons (those containing multiple types of content).
      behaviors: {
        canAdd: false // Disables the ability to add mixed content.
      }
    },
    rowAddon: {
      // Controls behaviors for all row content addons.
      behaviors: {
        canAdd: false // Disables adding new row content addons.
      }
    }
  }
}
```

## Add Condition and Edit Condition Buttons

You can choose to display or hide the "Add Condition" and "Edit Condition" buttons when using the [Content Dialog](content-dialog.md) with [Display Conditions](display-conditions.md).

The following code shows an example config for how you can display or hide these buttons using advanced permissions.

```javascript
{
  rows: {
    // Controls the display conditions for rows in your design.
    displayConditions: {
      locked: false, // Specifies whether the display conditions can be edited. 'false' means it can be modified.
      show: true // Determines if the display conditions are visible to the user.
    }
  }
}

```

## Role templates <a href="#role-templates" id="role-templates"></a>

We’ve put together a few JSON templates of custom roles created with Advanced permissions, so you can get started experimenting with this powerful feature.

You can find them in our [GitHub account.](https://github.com/BEE-Plugin/bee-advanced-permissions)
