# Stability AI

## AI Stable Diffusion XL AddOn Text-to-Image

The Stability AI AddOn converts text to images. This feature allows your end users to submit descriptions of what they would like to see in their AI-generated images, and to also submit negative prompts of what they do not want to see in their image. Once they submit the prompt and negative prompt, they'll receive an AI-generated image that they can use directly within their designs. Visit the [AI-generated white label end user guide](https://docs.beefree.io/end-user-guide/ai-generated-images) to learn more about how this feature works for your application's end users.

{% embed url="https://drive.google.com/file/d/1waaMV9dDwUqpIOcDzEnJC5PfzQgElK6l/view?usp=sharing" %}

### How to activate

This section discusses the prerequisites and steps you need to take to get started with this feature.

Prerequisites

* [Stability AI](https://stability.ai/) API key
* Stability AI addOn installed in the Beefree SDK Developer Console

Take the following steps to activate this feature:

1. Log in to the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website\_menu).
2. Navigate to the application you'd like install the addOn in.
3. Install the [Stability AI](https://stability.ai/) addOn.
4. Provide the requested details.
5. Save your changes.

The addOn is now activated.

### Configuration settings

The Stability AI text-to-image AddOn uses a new handle.&#x20;

This handle is `ai-image-generation`.

Consider the following settings when configuring this feature in your code:

| Parameter              | Type    | Description                                                              | Additional Information                                                                         |
| ---------------------- | ------- | ------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------- |
| `imagesAvailable`      | number  | Images available.                                                        | If not provided images are not counted and the user can generate an infinite number of images. |
| `imagesUsed`           | number  | The images used.                                                         |                                                                                                |
| `isGenerationDisabled` | boolean | Disable the generation.                                                  | False by default.                                                                              |
| `upsellTrigger`        | number  | Represents the number of remaining images that will show the upsell CTA. | Default is 3.                                                                                  |
| `isUpsellEnabled`      | boolean | Enable or disable the upsell.                                            | Default is false.                                                                              |
| `folderName`           | string  | The name of the folder where the images will be saved.                   | Default is “AI Generated Images".                                                              |

### Sample code

This section includes sample code you can use to configure this AddOn.

<details>

<summary>onInfo example</summary>

Use the following code sample to configure this feature for your application.

```javascript
onInfo: function (infoMessage) {
  if (infoMessage.code === 1000) {
    var handle = infoMessage.detail.handle

    if (handle === 'ai-image-generation') {
      imagesCounter += infoMessage.detail.consumedImages
        const refreshedUsageSettings = {
          addOns: [
            {
              id: "ai-image-generation",
              settings: {
                imagesAvailable: imagesAvailable,
                imagesUsed: imagesCounter,
                isGenerationDisabled: (imagesCounter >= imagesAvailable) ? true : false,
                upsellTrigger: 3,
                isUpsellEnabled: isUpsellEnabled,
              }
            },
          ],
        }
        // Reload Config
        bee.loadConfig(refreshedUsageSettings)
      }
  }
},
```

</details>

<details>

<summary>Upsell example</summary>

Use the following code to communicate to your end users when they have used all of their available image generations for this feature and need to purchase more.&#x20;

```javascript
upsell: {
  label: 'upsell',
  handler:(resolve, reject, args)=>{
    if(args.handle === 'ai-image-generation'){
      imagesAvailable+=5
      resolve({
        addOns:[{
          id: "ai-image-generation",
          settings: {
            imagesAvailable: imagesAvailable,
            imagesUsed: imagesCounter,
            isGenerationDisabled: (imagesCounter >= imagesAvailable) ? true : false,
            upsellTrigger: 3,
            isUpsellEnabled: isUpsellEnabled,
          }}]
        })
    }
  }
},
```

</details>

<details>

<summary>Disable generation per user example</summary>

Use the following code to disable this text-to-image generation for a user of your application. This feature will still be visible within the builder, but they will not be able to use this. A potential use case for this is if you'd like to motivate an end user to upgrade for access to this feature.

```javascript
addOns: [
  {
    id: "ai-image-generation",
    settings:{
      isGenerationDisabled: true,
    }
  },
],
```

</details>

<details>

<summary>Disable AddOn per user</summary>

Use the following code to disable this feature for a user of your application.

```javascript
addOns: [
  {
    id: "ai-image-generation",
    enabled: false,
  },
],
```

</details>
