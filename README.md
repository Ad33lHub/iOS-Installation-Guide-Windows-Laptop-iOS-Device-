video: https://drive.google.com/file/d/1sfj0V5t_vhQch2JqWqsOzFRJGhG_CxSY/view?usp=sharing

# iOS Installation Guide (Windows Laptop → iOS Device using Codemagic)

This guide explains how to build a Flutter iOS app using **GitHub + Codemagic Free Plan** on Windows and then install the **IPA** on your iPhone using **Sideloadly** or **iTunes**.

---

## **1. Upload Your Project to GitHub**

1. Initialize git in your project:

   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   ```
2. Create a GitHub repository.
3. Push your project:

   ```bash
   git remote add origin https://github.com/your-username/your-repo.git
   git branch -M main
   git push -u origin main
   ```

---

## **2. Connect GitHub Repo to Codemagic**

1. Go to **[https://codemagic.io/](https://codemagic.io/)**
2. Sign in with your GitHub account.
3. Codemagic will ask for GitHub permissions. Allow access.
4. Select your Flutter repository from the list.
5. Click **Set up build**.

---

## **3. Configure Codemagic Free Plan Settings**

Codemagic free plan has limitations, so configure it carefully.

### Enable Flutter iOS Build

1. Go to **Workflow Editor**.
2. Select **Flutter App**.
3. Under **Build for platforms**, select:

   * **iOS**
4. Under **Build mode**, choose:

   * **Release**
5. In **Apple Developer Account**, select **Manual code signing** (free plan does not support automatic signing).
6. Upload:

   * Your **development certificate (.p12)**
   * Your **provisioning profile (.mobileprovision)**
     (You must create these using an Apple ID on a Mac or borrowed Mac.)

### Environment

* Leave default Flutter & Xcode versions.
* Disable tests to avoid wasting build minutes.

### Artifacts

Enable:

* **.ipa**
* **Runner.app.zip**

Save the workflow.

---

## **4. Build the App on Codemagic**

1. Click **Start Build**.
2. Wait for the build to complete.
3. After success, download:

   * **Runner.app.zip**
   * **YourApp.ipa** (if free plan package is available; otherwise create yourself)

---

## **5. Create IPA Manually (If Codemagic Didn’t Provide IPA)**

If you only got **Runner.app.zip**, do this:

### **Step 1: Unzip**

Extract:

```
Runner.app/
```

### **Step 2: Create the correct folder structure**

Make directories like this:

```
Payload/
   Runner.app
```

### **Step 3: Zip the folder**

Right-click → Send to ZIP
Name it:

```
app.zip
```

### **Step 4: Convert ZIP to IPA**

Rename:

```
app.zip → app.ipa
```

Done. You now have a valid iOS IPA file.

---

## **6. Connect iPhone to iTunes (Optional but useful for trust)**

1. Install **iTunes for Windows**.
2. Connect your iPhone via USB.
3. Press *Trust This Computer* on your phone.

This step ensures the device is fully recognized before sideloading.

---

## **7. Install the IPA on iPhone using Sideloadly**

1. Download Sideloadly (Windows):
   [https://sideloadly.io](https://sideloadly.io)
2. Open it.
3. Connect iPhone.
4. Drag your **app.ipa** into Sideloadly.
5. Login with your Apple ID.
6. Press **Start**.
7. Wait for installation to finish.
8. On your iPhone:

   * Go to **Settings → General → VPN & Device Management**
   * Trust the developer profile.

Your app is now installed on the iPhone.

---

## **DONE. Your iOS app can now run from a Windows machine using GitHub + Codemagic + Sideloadly.**

If you want, I can also generate a **perfect README.md file** with formatting, screenshots sections, badges, etc.
