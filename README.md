I couldnt find a bucket to install beeper through scoop so I made one Perfect foresight, 

---

# Maintaining the Beeper Scoop Bucket

This guide explains how to update and maintain the **Beeper Scoop manifest** when a new version is released.

---

## 1. Check for New Version

1. Visit the [Beeper download page](https://www.beeper.com/).
2. Look for the latest Windows x64 installer.
   Example filename:

   ```
   Beeper x64 4.2.100.exe
   ```

---

## 2. Download the Installer

* Save the `.exe` file somewhere temporary (e.g., `D:\downloads`).
* Keep the filename intact; Scoop will rename it internally during install.

---

## 3. Compute SHA256 Hash

Run this command in PowerShell:

```powershell
Get-FileHash "D:\downloads\Beeper x64 4.2.100.exe" -Algorithm SHA256
```

Copy the resulting **hash string**.

---

## 4. Update the Manifest (`Beeper.json`)

* Open `Beeper.json` in your bucket repo.
* Update the following fields:

  * `"version"` → e.g. `4.2.100`
  * `"url"` → update with the direct download link if needed
  * `"hash"` → paste the new SHA256 hash

Do **not** change the installer logic unless Beeper’s structure changes.

---

## 5. Test the Update 

## 6. Commit and Push


## 7. Install/Update from Bucket

On any machine with this bucket added:

```powershell
scoop update
scoop update Beeper
```

---

## Troubleshooting

* **Hash mismatch?** → Recalculate SHA256.
* **Shim not created?** → Ensure `Beeper.exe` exists in the extracted folder.
* **Extraction issues?** → Beeper may have changed its installer. Re-run with debug logging (`scoop install -g Beeper -k`) and adjust the install script.
