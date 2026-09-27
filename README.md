# 🔬 CT Voxel VR: 3D Micro-CT Pin & Defect Inspector 🥽

An interactive, browser-based **WebVR & 3D Tomography Inspection Tool** designed for non-destructive testing (NDT) analysis. This application renders real reconstructed computed tomography (CT) datasets of an engineered pin, allowing users to inspect internal porosity and structural defects in immersive Virtual Reality directly through a smartphone or desktop web browser.

## 📸 Key Features 🚀

* 🕶️ **Full WebVR & Mobile Headset Support:** Built with A-Frame & Three.js. Compatible with Google Cardboard, VR Box, and mobile stereoscopic headsets with zero installation needed.

* 🔍 **Real Tomography Data Integration:** Visualizes dual-mesh volumetric segmentations: the semi-transparent outer metal pin shell and internal high-contrast defect micropores (`pin_model.glb`).

* 🔄 **Dual Inspection Perspectives:**
  * **Standard Lab View:** Inspect the rotating pin from an exterior vantage point on an illuminated laboratory pedestal.
  * **Center Stage / 360° Orbit Mode:** Step directly into the center of the ring. The pin drops to exact eye level and revolves around you in a full 360° trajectory, allowing seamless gyro-head-tracked defect inspection.

* ⚡ **Dynamic Sharpness & Buffer Scaling:** An ultra-flexible resolution slider ranging from **0.01x to 2.00x**, allowing smooth 60+ FPS playback on mobile GPUs.

* 🎯 **Pore Cloud Decimation / Level of Detail (LOD):** Real-time triangle buffer sampling (10%–100%) with automatic glow compensation so defects remain sharp and visible without lagging mobile devices.

* 🩻 **Inspection Tools:**
  * **Orbit View Switch:** Toggle between exterior pedestal inspection and center-stage orbital sweep.
  * **X-Ray Mode:** Strips surface reflections and increases opacity transparency to emphasize deep-seated porosity clusters.
  * **Wireframe Mode:** Inspect underlying polygonal density and surface topology.
  * **Live Opacity & Emission Tuners:** Adjust outer metal transparency and micropore glow intensity on the fly.
  * **Auto-Rotation Control:** 360° inspection pivot with pause/resume functionality.

* 📊 **Real-time Performance Monitor:** Displays real-time FPS counter, dynamic render resolution, and an automated drop-protection safeguard (Auto-DRS).

## 📂 Repository Structure 📁

```
├── pin_model.glb      # Reconstructed 3D binary model (Pin body + micropore cloud)
├── webvr_app.html     # Single-file WebVR inspection application
└── README.md          # Project documentation and user guide
```

## 🛠️ Getting Started & Usage Guide 📖

### 1. Launch the Live WebVR App (Recommended) 🌐

No installation, setup, or builds required! The application is hosted directly via GitHub Pages over a secure **HTTPS** connection (mandatory for mobile browsers to access gyroscope and orientation sensors):

👉 [**Launch 3D CT Pin Inspector**](https://drpepperjunkerqueen.github.io/pin-vr/webvr_app.html)

1. Open the link above in your mobile web browser (**Chrome**, **Safari**, or **Firefox**).
2. The 3D model loads and centers automatically on the inspection stage.

### 2. Local Testing (Optional for Developers) 💻

If you want to clone this repository and run it locally on your computer:

```bash
# Clone the repository
git clone https://github.com/drpepperjunkerqueen/pin-vr.git
cd pin-vr

# Start a quick local web server using Python 3
python -m http.server 8000
```

Then navigate to `http://localhost:8000/webvr_app.html` in your browser.

## 🎮 Navigation & Controls 🕹️

### 🖥️ Desktop / Laptop

| Action | Control |
| :--- | :--- |
| **Look Around** | Click and drag the left mouse button |
| **Move in Lab Space** | `W`, `A`, `S`, `D` keys |
| **Center Orbit Toggle** | Click **"Pozycja: Środek okręgu"** to step inside the ring |
| **Inspect Parameters** | Use on-screen floating control sliders and toggles |
| **Drag & Drop** | Drag any custom `.glb` / `.gltf` model straight into the viewport |

### 📱 Mobile & VR Headsets (Google Cardboard / VR Box)

1. Open the web link in landscape mode on your smartphone.
2. Choose your preferred inspection perspective:
   * Leave it on **Standard View** to inspect the pin on its pedestal in front of you.
   * Tap **"Pozycja: Środek okręgu"** to stand in the center and have the pin revolve around you at eye level.
3. Tap the **VR Goggles Icon** 🥽 at the bottom-right corner of the screen.
4. The viewport automatically divides into a stereoscopic Side-by-Side (SBS) view.
5. Insert your smartphone into the VR headset and look around using natural head movements (gyro-tracking).

## ⚙️ Optimization & Troubleshooting 💡

* **Encountering low FPS on your phone?**
  * Slide the **VR Sharpness** slider down to `0.75x` or `0.50x`.
  * Adjust the **Pore Cloud LOD** slider to `30%` – `50%`. The app will sample the pore distribution uniformly without hiding clusters.

* **Model doesn't load automatically?**
  * Ensure `pin_model.glb` and `webvr_app.html` reside in the exact same directory.
  * Alternatively, tap the **"Wczytaj .GLB"** button on the top-right and select the file from your local storage.

## 📜 Technology Stack 🧰

* [A-Frame 1.6.0](https://aframe.io/) – WebVR / WebXR framework
* [Three.js](https://threejs.org/) – WebGL 3D rendering pipeline
* [Tailwind CSS](https://tailwindcss.com/) – Responsive HUD interface overlay
* **CT Pipeline:** Micro-CT slice stack $\rightarrow$ Fiji/ImageJ Marching Cubes $\rightarrow$ Blender Decimation & GLTF 2.0 Export

## 📄 License ⚖️

This project is licensed under the [MIT License](LICENSE) – feel free to adapt it for scientific research, engineering analysis, or educational exhibits!