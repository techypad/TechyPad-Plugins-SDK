<div align="center">
  <img src="https://cdn.techypad.in/images/logo.png" alt="TechyPad Logo" width="200"/>
</div>

# 🚀 TechyPad Plugins SDK

Welcome to the TechyPad Plugins SDK! TechyPad supports two types of plugins:
1. **Script-based Plugins** (Easy/Elgato-style) - Run any script or command. Use this for 90% of use cases.
2. **Native C++ Plugins** (Advanced) - Full control, custom UI settings, and deep integration.

> [!IMPORTANT]
> **Security & Publishing Policy**
> To protect TechyPad users from malware, we **do not** accept pre-compiled `.dll` or `.techypadplugin` files directly. 
> * **Script Plugins:** Submit your raw scripts and `manifest.json`.
> * **Native Plugins:** Submit a link to your open-source GitHub repository. The TechyPad team will review your C++ code, compile it, and officially sign/hash it for distribution.
> 
> 📤 **Submit your plugins at:** [submit.techypad.in](https://submit.techypad.in)
> 🛒 **Approved plugins will be available on:** [marketplace.techypad.in](https://marketplace.techypad.in)

> [!WARNING]
> **User Disclaimer & Integrity Verification**
> For your safety, ONLY install plugins downloaded from the official [marketplace.techypad.in](https://marketplace.techypad.in). TechyPad is not responsible for third-party plugins downloaded from unverified sources. 
> 
> All officially published `.techypadplugin` files are secured with a cryptographic API hash. When a user installs a plugin, the TechyPad application automatically verifies this hash during the extraction process to guarantee that the plugin has not been tampered with or modified by a malicious third party.

---

## 1. Script-based Plugins (The Easy Way)

Script plugins are just folders containing your code and a `manifest.json`. No compiling is required! This is the highly recommended approach for most developers.

### Step 1: Create a Folder
Create a new folder in `C:\Users\YOURNAME\Desktop\TechyPad\plugins\` (or wherever your TechyPad is installed).
Example: `plugins/my-smart-light/`

### Step 2: Create `manifest.json`
Inside your folder, create a file named `manifest.json`. This tells TechyPad about your plugin. Here is a complete template you can copy and paste:

```json
{
    "id": "com.user.my_plugin",
    "name": "My Smart Light",
    "version": "1.0.0",
    "author": "Your Name",
    "type": "script",
    "actions": [
        {
            "id": "toggle_light",
            "name": "Toggle Light",
            "description": "Runs a python script to toggle light",
            "command": "python run.py toggle",
            "icon": "icon.png"
        }
    ]
}
```

### Step 3: Create your Script (`run.py`)
You can use Python, Batch (`.bat`), or PowerShell. Here is a starter template for `run.py` that you can copy and paste into your folder:

```python
import sys

def toggle_light():
    print("Light toggled!")
    # Add your smart home API code here

if __name__ == "__main__":
    # TechyPad passes the action ID as the first argument
    if len(sys.argv) > 1:
        action = sys.argv[1]
        
        if action == "toggle":
            toggle_light()
        else:
            print(f"Unknown action: {action}")
    else:
        print("No action provided.")
```

### Step 4: Add Your Icon
For icons, simply place any `.png` image (e.g., `icon.png`) into your plugin folder alongside your script. 
Make sure the filename matches the `"icon"` field in your `manifest.json`! TechyPad will automatically load it.

* **Pro Tip:** Use `%BUTTON_ID%` in your `manifest.json` command if you need to pass exactly which button was pressed on the physical deck to your script!

---

## 2. Native C++ Plugins (The Power Way)

If you need advanced features like a custom configuration window or real-time status updates (like Home Assistant or OBS), you need to create a Native Plugin using C++ and Qt 6.x. 

### Development Workflow
1. Develop your plugin locally using CMake and MSVC.
2. Embed all assets (like icons) using the **Qt Resource System (QRC)** with a unique prefix (e.g., `/com.yourname.yourplugin`).
3. Inherit from `IPlugin` and export your plugin using `Q_EXPORT_PLUGIN2`.

### Publishing Native Plugins
As per our security policy, **do not package your `.dll` for distribution**. 
Instead:
1. Push your plugin's source code to a public GitHub repository.
2. Submit your repository link to [submit.techypad.in](https://submit.techypad.in).
3. The TechyPad admin team will review the code for malicious activity.
4. If approved, we will securely compile, package, and hash the plugin, making it available on [marketplace.techypad.in](https://marketplace.techypad.in).

---

## 📂 Testing Your Plugins Locally
While developing, you can test your plugins by placing your folder (or compiled `.dll` for native developers) in:
`C:\Users\YOURNAME\Desktop\TechyPad\plugins\`

> [!CAUTION]
> **Developer Mode Required!**
> By default, TechyPad blocks any unverified or unsigned scripts and plugins for security. To test your plugin locally, you must open the TechyPad settings and toggle **Developer Mode** to **ON**. 

Restart TechyPad, and your new actions will appear in the **Button Configuration** menu!


## 🌐 TechyPad Ecosystem

The Plugin SDK is just one part of the complete TechyPad development ecosystem. Depending on what you're building, you may also need these repositories:

### 🛠️ TechyPad Setup
Install drivers, the desktop application, and everything required to get your TechyPad up and running before developing plugins.

➡️ https://github.com/techypad/techy-pad-setup

---

### 🎨 TechyPad Icon SDK
Create beautiful, consistent icons for your plugins with the official icon templates, guidelines, and export tools.

➡️ https://github.com/techypad/TechyPad-Icon-SDK

---

⭐ If this SDK helps you build something awesome, consider starring the repository and sharing your plugin with the community!
