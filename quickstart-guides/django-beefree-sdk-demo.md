---
description: A demo of Beefree SDK embedded within a Django application.
---

# Django Beefree SDK Demo

## Introduction

This demo includes a [Django app](https://docs.djangoproject.com/en/5.2/) that embeds [Beefree SDK's](https://docs.beefree.io/beefree-sdk) no‑code email builder using Django [templates](https://docs.djangoproject.com/en/5.2/ref/templates/) and [static files](https://docs.djangoproject.com/en/5.2/howto/static-files/). This project demonstrates a Python‑first backend that securely obtains Beefree SDK tokens, while the browser loads and runs the SDK.

* Docs: [Beefree SDK](https://docs.beefree.io/beefree-sdk)

Reference this project's code in the [django-beefree-app-demo GitHub repository](https://github.com/BeefreeSDK/beefree-django-app-demo).

{% embed url="https://github.com/BeefreeSDK/beefree-django-app-demo" %}

The following diagram shows the project's architecture at a high level.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

While Django applications are Python‑based and commonly server‑rendered, you can still embed JavaScript libraries like Beefree SDK. The key is to split responsibilities:

* Django (server): securely requests a token from `loginV2` using `BEE_CLIENT_ID` and `BEE_CLIENT_SECRET` and returns the full JSON to the browser.
* Browser (client): loads [Beefree SDK](https://docs.beefree.io/beefree-sdk) via a script, initializes it with the server‑provided token, and mounts the editor in a container div.

This [project](https://github.com/BeefreeSDK/beefree-django-app-demo) provides:

* A minimal Django app with an endpoint for token generation.
* A template with a container and a “Read the Docs” button.
* A small frontend script that loads the SDK, starts it, and then loads a starter template for a smooth, interactive experience.

### Quick start (clone and run)

```bash
# 1) Clone
git clone https://github.com/BeefreeSDK/beefree-django-app-demo.git
cd Django-beefree-demo

# 2) Create venv and install deps
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

# 3) Configure environment (recommended: .env at project root)
# Create .env with your credentials
cat > .env << 'EOF'
DJANGO_SECRET_KEY=change-me
DJANGO_DEBUG=1
DJANGO_ALLOWED_HOSTS=*
BEE_CLIENT_ID=YOUR-CLIENT-ID
BEE_CLIENT_SECRET=YOUR-CLIENT-SECRET
EOF

# 4) Migrate and run (default host/port)
python manage.py migrate
python manage.py runserver

# Optional: run on a custom host/port
# (set DJANGO_ALLOWED_HOSTS accordingly, e.g., to your domain or IP)
# python manage.py runserver 9000
# python manage.py runserver 0.0.0.0:8080
```

Open your server URL in the browser (for local dev, use the address shown by `runserver`).

* You’ll see a header with a “Read the Docs” button linking to the SDK docs.
* The Beefree SDK editor loads in the container and then loads the sample template from `/static/editor/initial-template.json`.
* If you see any cached assets, do a hard refresh (Shift + Reload).

### How it works

This section discusses how the Django applicatons works with Beefree SDK.

#### High‑level

* The SDK is a JavaScript widget that runs client‑side in the user’s browser.
* Django securely generates a BEE token server‑side via `https://auth.getbee.io/loginV2` using `BEE_CLIENT_ID` and `BEE_CLIENT_SECRET`.
* The server returns the full JSON response to the browser.
* The browser initializes the SDK with that JSON: `new BeefreeSDK({ ...token, v2: true })`, then calls `sdk.start(beeConfig, user, template, options)` and/or `sdk.load(template)` as needed.

#### Django pieces

* `editor/views.py`
  * `index` renders `templates/editor/index.html`.
  * `bee_auth` exposes `POST /api/bee-auth`: sends `client_id`, `client_secret`, and `uid` to Beefree `loginV2` and returns the full JSON to the client.
* `beefree_demo/settings.py` loads environment variables via `python-dotenv` (`.env` in project root recommended).

#### Frontend pieces

* `templates/editor/index.html`: page structure, docs button, editor container div (`id="beefree-editor-container"`), and a `<script type="module">` inclusion for `static/editor/editor.js`.
* `static/editor/editor.js`:
  * Fetches the token from `/api/bee-auth` using `async/await`.
  * Dynamically loads the Beefree SDK.
  * Builds `beeConfig` with required `container` parameter, and optional `language`, `onSave`, and `onError` parameters.
  * Starts the editor with an empty template, then calls `sdk.load(templateJson)` to load `/static/editor/initial-template.json`.

#### Template initialization

* The starter template is served at `/static/editor/initial-template.json` (also embedded as a fallback).
* Update the file or edit `initialTemplate` in `static/editor/editor.js` to change the default content.

### Django architecture (explanation)

This section references concepts from [this article](https://www.interviewbit.com/blog/django-architecture/) to explain how Django architectures work at a high level. Reference [this article](https://www.interviewbit.com/blog/django-architecture/) for more information.

{% hint style="info" %}
**Note:** The content in this section is not specific to this project, but all Django architectures in general. Skip if you are already familiar with these concepts.
{% endhint %}

At a high level, web apps separate concerns into three kinds of logic: input, business, and presentation. Django follows a pragmatic variant known as MTV (Model‑Template‑View):

* **Model:** defines and manages your data and business rules.
* **Template:** renders the user interface (HTML/CSS/JS) based on data passed from views.
* **View:** handles HTTP requests, orchestrates business logic, and returns responses.

URLs map incoming requests to views; views may talk to models and then render templates. This separation keeps code maintainable and testable while allowing each piece to evolve independently. For a deeper dive, see Django architecture overviews like [this article](https://www.interviewbit.com/blog/django-architecture/).

### Best practices for Beefree SDK in Django

* Generate tokens server‑side only; never expose `BEE_CLIENT_SECRET` in the browser.
* Return the entire `loginV2` JSON to the client and construct the SDK with `{ ...token, v2: true }`.
* Use `sdk.start` and include a valid `container` id in `beeConfig`.
* Load a design via `sdk.load(template)` after `sdk.start(...)`.

### How a JS SDK works in Django

Django renders HTML and serves static files, but the browser runs JavaScript. [Beefree SDK](https://docs.beefree.io/beefree-sdk) is a client‑side library. Django’s job is to:

* Render the page and serve static assets.
* Securely fetch and return the Beefree SDK token from `loginV2`.
* Provide endpoints and persistence for your app’s data (if needed). The browser then loads the SDK and opens the editor with the server‑provided token.

### File map

```
beefree_demo/
  settings.py       # loads .env, configures apps/static/templates
  urls.py           # routes root to the editor app
editor/
  views.py          # index page + /api/bee-auth (loginV2 proxy)
  urls.py           # app URL patterns
templates/editor/
  index.html        # container + docs button, includes editor.js
static/editor/
  editor.js         # fetch token, load SDK, start editor, then load template
  styles.css        # basic layout
  initial-template.json # starter design
```

### Troubleshooting

* Editor stuck on loading spinner:
  * Start with an empty template and call `sdk.load(templateJson)` after `sdk.start(...)`. This project already does this in `static/editor/editor.js`.
  * Hard refresh (Shift + Reload) to avoid cached assets.
  * Confirm `GET /static/editor/initial-template.json` is 200/304 and `POST /api/bee-auth` is 200.
* SDK 404/CORS from CDN:
  * The loader tries jsDelivr +esm, esm.sh, Skypack, and UMD fallbacks. If your network blocks these, self‑host the SDK file and reference it directly.
* Token errors (401/403):
  * Verify `BEE_CLIENT_ID` and `BEE_CLIENT_SECRET` in `.env`, restart the server.

### References

* Official docs: [Beefree SDK](https://docs.beefree.io/beefree-sdk)
