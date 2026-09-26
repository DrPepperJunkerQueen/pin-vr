# 🔬 CT Voxel VR: 3D Micro-CT Pin & Defect Inspector 🥽

[![WebVR](https://img.shields.io/badge/WebVR-A--Frame%201.6.0-38bdf8?style=for-the-badge&logo=virtualreality)](https://aframe.io/)
[![Three.js](https://img.shields.io/badge/Three.js-WebGL-black?style=for-the-badge&logo=three.js)](https://threejs.org/)
[![License](https://img.shields.io/badge/License-MIT-emerald?style=for-the-badge)](LICENSE)

An interactive, browser-based **WebVR & 3D Tomography Inspection Tool** designed for non-destructive testing (NDT) analysis. This application renders real reconstructed computed tomography (CT) datasets of an engineered pin, allowing users to inspect internal porosity and structural defects in immersive Virtual Reality directly through a smartphone or desktop web browser.

---

## 📸 Key Features 🚀

- 🕶️ **Full WebVR & Mobile Headset Support:** Built with A-Frame & Three.js. Compatible with Google Cardboard, VR Box, and mobile stereoscopic headsets with zero installation needed.
- 🔍 **Real Tomography Data Integration:** Visualizes dual-mesh volumetric segmentations: the semi-transparent outer metal pin shell and internal high-contrast defect micropores (`pin_model.glb`).
- ⚡ **Dynamic Sharpness & Buffer Scaling:** An ultra-flexible resolution slider ranging from **0.01x to 2.00x**, allowing smooth 60+ FPS playback on mobile GPUs.
- 🎯 **Pore Cloud Decimation / Level of Detail (LOD):** Real-time triangle buffer sampling (10%–100%) with automatic glow compensation so defects remain sharp and visible without lagging mobile devices.
- 🩻 **Inspection Tools:**
  - **X-Ray Mode:** Strips surface reflections to emphasize deep-seated porosity clusters.
  - **Wireframe Mode:** Inspect underlying polygonal density and surface topology.
  - **Live Opacity & Emission Tuners:** Adjust outer metal transparency and micropore glow intensity on the fly.
  - **Auto-Rotation:** 360° inspection pivot with pause/resume functionality.
- 📊 **Real-time Performance Monitor:** Displays real-time FPS counter, dynamic render resolution, and an automated drop-protection safeguard (Auto-DRS).

---

## 📂 Repository Structure 📁

```text
├── pin_model.glb      # Reconstructed 3D binary model (Pin body + micropore cloud)
├── webvr_app.html     # Single-file WebVR inspection application
└── README.md          # Project documentation and manual
```

---

## 🛠️ Getting Started & Usage Guide 📖

### 1. Launching via GitHub Pages (Recommended) 🌐
Because mobile browsers enforce strict HTTPS security policies to grant access to device orientation (gyroscope) sensors:
1. Enable **GitHub Pages** in your repository settings:
   - Navigate to **Settings** ⚙️ $\rightarrow$ **Pages**.
   - Under **Build and deployment**, select branch: `main` (or `master`) and folder: `/ (root)`.
   - Click **Save**.
2. Open the published link on your mobile browser (Safari, Chrome, or Firefox).
3. If your main file is named `webvr_app.html`, visit:
   ```url
   https://<your-username>.github.io/<your-repo-name>/webvr_app.html
   ```

### 2. Local Testing (Desktop / Local Network) 💻
You can spin up a local development server with Live Server or Python:
```bash
# Using Python 3
python -m http.server 8000
```
Open `http://localhost:8000/webvr_app.html` in your browser.

---

## 🎮 Navigation & Controls 🕹️

### 🖥️ Desktop / Laptop
| Action | Control |
| :--- | :--- |
| **Look Around** | Click and drag the left mouse button |
| **Move in Lab Space** | `W`, `A`, `S`, `D` keys |
| **Inspect Parameters** | Use on-screen floating control sliders and toggles |
| **Drag & Drop** | Drag any custom `.glb` / `.gltf` model straight into the viewport |

### 📱 Mobile & VR Headsets (Google Cardboard / VR Box)
1. Open the web link in landscape mode on your smartphone.
2. Tap the **VR Goggles Icon** 🥽 at the bottom-right corner of the screen.
3. The viewport automatically divides into a stereoscopic Side-by-Side (SBS) view.
4. Insert your smartphone into the VR headset and look around using head movement (gyro-tracking).

---

## ⚙️ Optimization & Troubleshooting 💡

- **Encountering low FPS on your phone?**
  - Slide the **VR Sharpness** slider down to `0.75x` or `0.50x`.
  - Adjust the **Pore Cloud LOD** slider to `30%` – `50%`. The app will sample the pore distribution uniformly without hiding clusters.
- **Model doesn't load automatically?**
  - Ensure `pin_model.glb` and `webvr_app.html` reside in the exact same directory.
  - Alternatively, tap the **"Load .GLB"** button on the top-right and select the file from your local storage.

---

## 📜 Technology Stack 🧰

- [A-Frame 1.6.0](https://aframe.io/) – WebVR / WebXR framework
- [Three.js](https://threejs.org/) – WebGL 3D rendering pipeline
- [Tailwind CSS](https://tailwindcss.com/) – Responsive HUD interface overlay
- **CT Pipeline:** Micro-CT slice stack $\rightarrow$ Fiji/ImageJ Marching Cubes $\rightarrow$ Blender Decimation & GLTF 2.0 Export

---

## 📄 License ⚖️

This project is licensed under the [MIT License](LICENSE) – feel free to adapt it for scientific research, engineering analysis, or educational exhibits!