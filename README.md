# Dinner, Please

A mobile-first dinner inspiration PWA. All meal history and seven-day mutes are stored in first-party cookies on the device. Nothing is sent to a database. The meal catalog lives in `meals.json`, separately from the app code.

## Edit the meal catalog

You normally only need to edit `meals.json`. Every entry has this structure:

```json
{
  "id": "chicken-bacon-ranch",
  "name": "Chicken bacon ranch sandwiches",
  "proteins": ["chicken"],
  "description": "Grilled chicken thighs, bacon, cheese and ranch on toasted rolls.",
  "tags": ["sandwich", "crowd-pleaser"],
  "quick": true,
  "noProtein": "defrost",
  "recipe": [
    "chicken-bacon-ranch",
    "https://www.thepioneerwoman.com/food-cooking/"
  ]
}
```

- `id`: A permanent unique identifier. Use lowercase words separated by hyphens. Do not change an existing ID after using the app, because history and mutes refer to it.
- `name`: The name displayed in the app.
- `proteins`: Any combination of `chicken`, `beef`, `pork`, `seafood`, and `vegetarian`.
- `description`: The sentence shown beneath the meal name.
- `tags`: Short descriptive labels displayed on the meal card.
- `quick`: Set to `true` to include it in the **Quick meals only** filter; otherwise use `false`.
- `noProtein`: Use `"ready"` when no thawing is required, `"defrost"` when it works by defrosting a freezer staple, or `null` to keep it out of **No protein ready**.
- `recipe`: Optional array. Each item is either a local recipe id (loads `recipe.html?id=...` from `recipes/id.json`) or an `http`/`https` link. Omit the field when you do not have a recipe yet. Simple dinners like pizza, nuggets, and nachos can stay without one.

Local recipes live in the `recipes/` folder. `recipe.html` renders one file at a time and always includes the original source link. The write-ups on that page are short home-cook versions so you can cook without the ads.

To add a meal, copy an entire meal object, place a comma between it and the neighboring object, then give it a new unique `id`. JSON does not allow comments or a comma after the final meal object.

After editing, commit the updated `meals.json` to the repository root. GitHub Pages may take a few minutes to publish the new version. The app requests the current file whenever it opens and uses its cached copy when offline.

## Publish with GitHub Pages

1. Create a new public GitHub repository, such as `dinner-please`.
2. Upload every file from this folder to the repository root. `index.html` and `meals.json` must be at the top level—not inside another folder.
3. In the repository, open **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**.
5. Select the `main` branch and `/ (root)`, then save.
6. Once deployment finishes, open `https://YOUR-USERNAME.github.io/dinner-please/` on the iPhone.

## Install on iPhone

1. Open the deployed URL in Safari.
2. Tap **Share**.
3. Tap **Add to Home Screen**. If it is hidden, scroll down or use **Edit Actions**.
4. Turn on **Open as Web App** if Safari offers the option, then tap **Add**.

Open the new **Dinner, Please** icon once while online so the offline files are cached.

## Important storage behavior

- History and mutes exist only in the browser data on that iPhone.
- They do not sync to another device.
- Deleting the web app or clearing Safari website data can erase them.
- A chosen meal is excluded for 14 days. A muted meal is excluded for 7 days.
