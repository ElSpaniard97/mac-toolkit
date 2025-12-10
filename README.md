📦 Mac Toolkit – macOS System Diagnostic Utility

Mac Toolkit is a standalone macOS desktop application written in SwiftUI that provides a full suite of hardware and system diagnostic tests.
It includes:

CPU stress test

Memory stress test

Disk stress test

Battery load test

Network diagnostics

Audio test (left, right, center, multi-channel)

Keyboard test

Display color cycling

Camera verification

Integrated bash toolkit backend (optional tests run via .sh script)

This tool is designed for IT technicians, repair shops, Mac refurbishers, and tech support operations.

⭐ Features
🧠 CPU Stress Test

Generates load across all CPU cores

Monitors response behavior

Provides Pass / Needs Attention result prompt

🧵 Memory Stress Test

Allocates RAM in controlled blocks

Monitors memory pressure

Handles 60s test duration

💾 Disk Stress Test

Performs write/read verification

Measures basic performance

Detects stall or slow I/O patterns

🔋 Battery Test

Puts system under load on battery

Compares battery drop before/after

Useful for quick battery health estimation

🌐 Network Test

Ping test

Traceroute

Basic connectivity checks

🔊 Audio Test

3× center beeps

Left speaker

Right speaker

Both speakers

Uses AVAudioEngine + panning

⌨️ Keyboard Test

Opens KeyboardChecker.com

User confirms pass/fail

🖥 Display Test

Full-screen overlay

Cycles through Green → Blue → Red

Exposes pixel issues, stuck pixels, burn-in

📷 Camera Test

Launches FaceTime or Photo Booth

Verify image quality + camera detection

🛠 Project Structure
MacSystemTestGUI/
│
├── MacSystemTestGUIApp.swift
├── ContentView.swift
├── mac_system_test_toolkit.sh   # optional CLI backend
├── Assets.xcassets/
│     └── AppIcon.appiconset     # your custom Mac Toolkit icon
└── README.md

🚀 How to Build This App From Scratch
1️⃣ Requirements

macOS 12+ recommended

Xcode 14 or later

SwiftUI

Basic understanding of Terminal (optional)

2️⃣ Clone the Repository
git clone https://github.com/<your-username>/<your-repo>.git
cd MacToolkit

3️⃣ Open the Project in Xcode

Double-click the project file:

MacSystemTestGUI.xcodeproj


Xcode will load the SwiftUI project.

4️⃣ Make Sure the Toolkit Script Is Included

In Xcode:

Check the left Project Navigator

You should see:

mac_system_test_toolkit.sh


If not:

Drag it into the project tree

When prompted → check Copy items if needed

Make sure Target Membership is checked for the Mac Toolkit target

This ensures the script is bundled inside the .app.

5️⃣ Import the App Icon

Place your Mac Toolkit icon into:

Assets.xcassets/AppIcon.appiconset/


Make sure:

Devices = Mac

The 512x512 (2x) slot contains your 1024×1024 PNG

Xcode scales the rest automatically

6️⃣ Build the App

In Xcode:

At the top, select My Mac as the run destination

Press ⌘B to build

Press ⌘R to run and test

📤 Exporting the App for Real Use

There are two supported export methods.

✅ Method 1 — Simple Build (local use)

In Xcode:

Product → Show Build Folder in Finder

Go to:

…/Build/Products/Debug/


Copy:

MacSystemTestGUI.app


Rename it:

Mac Toolkit.app


Move it to:

/Applications


Now you can run it like any normal app.

✅ Method 2 — Archive → Copy App (recommended for distribution)

In Xcode:

Product → Archive


In Organizer:

Click Distribute App

Choose Custom

Choose Copy App

Xcode exports a clean, portable:

Mac Toolkit.app


This is the correct version to give other users or deploy on multiple Macs.

💾 Running the App from USB

macOS may block unsigned apps on removable media.

To avoid issues:

Recommended Workflow:

✔ Right-click the app → Compress
✔ Copy the .zip to USB
✔ On the destination Mac, copy the .zip to Desktop and unzip it
✔ Then run the app

This preserves permissions and prevents structure damage on exFAT drives.

🔐 Gatekeeper Notes

Since the app is unsigned and un-notarized:

macOS will block it the first time on each Mac

To bypass:

Try opening once

Go to:

System Settings → Privacy & Security

Scroll to bottom

Click Allow Anyway

Re-open the app

Choose Open

After that, the app launches normally on that machine.

🧪 Toolkit Script Notes

mac_system_test_toolkit.sh is the CLI backend used for:

CPU test

Memory test

Disk test

Battery test

Network test

Camera test

Audio (if not handled by Swift)

It is embedded inside the app bundle and executed via:

/bin/zsh -lc MODE=gui "path/to/mac_system_test_toolkit.sh <arg>"


This allows the app to run terminal tests while keeping the UI clean.

🛠 Development Tips
Changing the app name in menu bar

Edit:

MacSystemTestGUIApp.swift


Change:

@main
struct MacSystemTestGUIApp: App {


to:

@main
struct MacToolkitApp: App {


And update the target name in Xcode.

Updating the app icon everywhere

Make sure:

The icon is set in Assets.xcassets

The target’s General → App Icon is set to AppIcon

Display overlay behavior

The display test uses a full-window overlay:

ZStack {
    colors[step].ignoresSafeArea()
}


This avoids full-screen API limitations on macOS.

🧯 Troubleshooting
❌ App bounces but won’t open

Copy the app from USB → Desktop and run it there.

If needed:

xattr -d com.apple.quarantine "/path/to/Mac Toolkit.app"

❌ App gives “damaged or incomplete”

You copied the wrong file.

Always export using:

Archive → Distribute → Custom → Copy App

❌ Script not found inside the app

Make sure:

mac_system_test_toolkit.sh exists in the project

Target Membership is enabled

The file is set to “Copy Bundle Resources”
