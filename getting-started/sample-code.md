# Sample Code

## A prototype in 2 minutes <a href="#a-prototype-in-2-minutes" id="a-prototype-in-2-minutes"></a>

Using this simple, client-side example, you can literally try out Beefree SDK in 2 minutes…

1. Obtain your application keys (**Client ID** and **Client Secret**) [by signing up here](https://devportal.beefree.io/hc/en-ussignup) (there is a free plan).
2. Create a new application: you will find your keys in the project’s details page
3. [Download](https://github.com/BeefreeSDK/beefree-sdk-sample-client) the client-side sample code.
4. Open `index.html` with your favorite code editor
5. Locate `client_id` and replace **“YOUR\_CLIENT\_ID”** with yours
6. Locate `client_secret` and replace **“YOUR\_CLIENT\_SECRET”** with yours
7. Save the file
8. Open it in your browser and get creative ![(smile)](https://mailup.atlassian.net/wiki/s/en_GB/6105/7d738a52bdb6676b96419199dc18454c6082dfc5.26/_/images/icons/emoticons/smile.png)

## Embedding the builder <a href="#embedding-the-builder" id="embedding-the-builder"></a>

Before using the code samples listed below in a production environment, please consider the following:

1. Make sure you first [sign up](https://devportal.beefree.io/hc/en-ussignup) and get your application keys (**Client ID** and **Client Secret**).
2. The client-side sample is not safe for a production environment (it was conceived as a quick way for you to test the application). Someone would be able to easily steal your application credentials (just viewing the source code of the page). To keep those credentials safe, authorization must be managed sever-side, as the .NET sample does.
3. These code samples use a limited set of features and configurations: they can be a good starting point to start developing around Beefree SDK, but they are not an exhaustive showcase of everything you can do.
4. All sample code is provided “as is”: it may contain defects, it may not follow best practices (although we try to!), and it should only be considered as point of reference.

## GitHub Repositories <a href="#embedding-the-builder" id="embedding-the-builder"></a>

Here's our ever-growing library of sample code that shows key Beefree SDK functionality in action so you can get up and running faster:

### Sample code to help you get started

| Name and Link                                                                                                        | Description                                                                                                                                                                                                                             | Stack                  |
| -------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| [Beefree SDK: Official NPM Package](https://github.com/BeefreeSDK/beefree-sdk-npm-official)                          | The official NPM package for Beefree SDK, complete with installation instructions and configuration tips.                                                                                                                               | Typescript             |
| [Beefree SDK: React Email Builder (React Wrapper)](https://github.com/BeefreeSDK/react-email-builder)                | React wrapper for the Beefree SDK that provides React components and hooks to integrate the Beefree SDK (Email Builder, Page Builder, File Manager, Popup Builder) into React applications                                              | React, Typescript      |
| [SDK Sample: Full-stack NextJS App](https://github.com/BeefreeSDK/beefree-sdk-sample-nextjs)                         | Demonstrates integrating the Beefree SDK into a full-stack NextJS application with database integration and user authentication.                                                                                                        | NextJS, Python, SQLite |
| [Beefree SDK: Angular Email Builder (Angular Wrapper)](https://github.com/BeefreeSDK/angular-email-builder)          | Angular wrapper for the Beefree SDK – A framework-specific package that provides Angular components to integrate the Beefree SDK (Email Builder, Page Builder, File Manager, Popup Builder) into Angular applications.                  | Angular, Typescript    |
| [Beefree SDK: Vue Email Builder (Vue Wrapper)](https://github.com/BeefreeSDK/vue-email-builder)                      | Vue.js wrapper for the Beefree SDK – A framework-specific package that provides the Builder component and composables to integrate the Beefree SDK (Email Builder, Page Builder, Popup Builder, File Manager) into Vue.js applications. | Vue, Typescript        |
| [SDK Sample: Simple Client HTML App](https://github.com/BeefreeSDK/beefree-sdk-sample-client)                        | A simple HTML app demonstrating the basic implementation of the Beefree SDK for client-side applications.                                                                                                                               | HTML, JavaScript       |
| [Beefree SDK: Email and Landing Page Templates](https://github.com/BeefreeSDK/beefree-sdk-assets-templates)          | A collection of free email, landing page, and popup templates designed for easy integration with the Beefree SDK.                                                                                                                       | JSON                   |
| [Beefree SDK: Secure Auth Example](https://github.com/BeefreeSDK/beefree-sdk-examples/tree/main/secure-auth-example) | This example demonstrates secure, production-ready authentication for the Beefree SDK. It showcases best practices for handling authentication tokens, automatic token refresh, and secure credential management.                       | React, TypeScript      |

### Sample code for advanced Beefree SDK functionality

This selection of sample code shows sample implementations of some of the more advanced Beefree SDK features so you can use them as inspiration (or as a starting point for your own implementation):

| Name and Link                                                                                                             | Description                                                                                                                                                                                                                                                                                                              | Stack                   |
| ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------- |
| [Saved and Synced Rows](https://github.com/BeefreeSDK/beefree-sdk-demos)                                                  | Code from our webinars showcasing how to use Saved and Synced Rows feature within the Beefree SDK.                                                                                                                                                                                                                       | ReactJS                 |
| [Autosave Versioning Example](https://github.com/BeefreeSDK/beefree-sdk-examples/tree/main/autosave-versioning-example)   | A ready-to-run example demonstrating how to implement automatic template versioning with auto-save. It shows how to automatically save template versions, maintain version history, and restore previous versions.                                                                                                       | React, TypeScript, Vite |
| [Commenting Example](https://github.com/BeefreeSDK/beefree-sdk-examples/tree/main/commenting-example)                     | An example that shows how to use the [Beefree SDK's Commenting feature](https://docs.beefree.io/beefree-sdk/other-customizations/advanced-options/commenting) to enable real-time collaboration, allowing your users to add comments, start threaded discussions, and manage feedback directly within the email builder. | React, TypeScript, Vite |
| [Conditional Rows Example](https://github.com/BeefreeSDK/beefree-sdk-examples/tree/main/conditional-rows-example)         | A ready-to-run example demonstrating how to integrate the [Beefree SDK Display Conditions feature](https://docs.beefree.io/beefree-sdk/other-customizations/advanced-options/display-conditions) into your application to enable personalized email content that adapts based on recipient attributes.                   | React, TypeScript, Vite |
| [Custom CSS Example](https://github.com/BeefreeSDK/beefree-sdk-examples/tree/main/custom-css-example)                     | An example showing how you can apply [Custom CSS](https://docs.beefree.io/beefree-sdk/other-customizations/appearance/custom-css) to customize the Beefree SDK editor's look and feel                                                                                                                                    | React, TypeScript       |
| [Multi-Builder Switch Example](https://github.com/BeefreeSDK/beefree-sdk-examples/tree/main/multi-builder-switch-example) | <p>This example showcases how to dynamically switch between Email, Page, and Popup builders within a single application interface.<br></p>                                                                                                                                                                               | React, TypeScript       |
| [PDF Export Example](https://github.com/BeefreeSDK/beefree-sdk-examples/tree/main/template-export-pdf-example)            | An example illustrating how to use the [Content Services API PDF export](https://docs.beefree.io/beefree-sdk/apis/content-services-api/export#pdf) functionality to power PDF exports with different export options, progress tracking, and export history management.                                                   | React, TypeScript       |
| [Template Load Example](https://github.com/BeefreeSDK/beefree-sdk-examples/tree/main/template-load-example)               | A complete demo showcasing Beefree SDK integration with a full-stack template management system with persistent storage, user authentication, and more.                                                                                                                                                                  |                         |

