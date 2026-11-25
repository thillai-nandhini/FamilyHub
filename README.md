# Family Hub

Family calendar (birthdays, anniversaries, insurance, rent, utilities and other payments, with repeats and amounts), chores with star points, shared shopping list with pantry import, message board and family members.

Backup: Family tab -> Download Excel backup (one sheet per section); Restore from Excel loads it back.

Works on its own: data is saved on the phone. Family sharing between phones is optional (Firebase, free).

## 1. Put it on GitHub Pages
1. Create a new repository (e.g. `family-hub`), public.
2. Upload everything in this folder: `index.html`, `manifest.webmanifest`, `sw.js`, `firebase-config.js`, and the `icons` folder.
3. Settings -> Pages -> Deploy from branch -> `main` / root. Your app will be at `https://YOUR-NAME.github.io/family-hub/`.
4. On the phone open that address, then Share -> Add to Home Screen. Updates show the second time you open the app.

## 2. Use it
Family tab -> add each person. Pick your name at the top right.

## 3. Share between phones (optional)
1. console.firebase.google.com -> Add project.
2. Build -> Authentication -> Get started -> Sign-in method -> turn on **Anonymous**.
3. Build -> Firestore Database -> Create database. Then open the Rules tab, paste the rules below, Publish.
4. Project settings (gear) -> Your apps -> Web `</>` -> register -> copy the config values into `firebase-config.js`, then upload that file to GitHub again.
5. In the app: Family tab -> Create family code. Send the invite link to the others; they open it and are joined.

Rules:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{db}/documents {
    match /families/{code}/items/{item} {
      allow read, write: if request.auth != null;
    }
  }
}
```
Anyone who has the family code can read and change your hub, so share it only with family. Pantry buy list: Shopping tab -> Import from Pantry app.
