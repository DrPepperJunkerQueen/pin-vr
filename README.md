# 🔬 CT Voxel VR: 3D Micro-CT Pin & Defect Inspector 🥽

An interactive, browser-based **WebVR & 3D Tomography Inspection Tool** designed for non-destructive testing (NDT) analysis[cite: 7]. This application renders real reconstructed computed tomography (CT) datasets of an engineered pin, allowing users to inspect internal porosity and structural defects in immersive Virtual Reality directly through a smartphone or desktop web browser[cite: 7].

## 📸 Key Features 🚀

* 🕶️ **Full WebVR & Mobile Headset Support:** Built with A-Frame & Three.js[cite: 7]. Compatible with Google Cardboard, VR Box, and mobile stereoscopic headsets with zero installation needed[cite: 7].

* 🔍 **Real Tomography Data Integration:** Visualizes dual-mesh volumetric segmentations: the semi-transparent outer metal pin shell and internal high-contrast defect micropores (`pin_model.glb`)[cite: 7].

* 🔄 **Dual Inspection Perspectives & 360° Circular Translation:**
  * **Standard Lab View:** Inspect the rotating pin from an exterior vantage point on an illuminated laboratory pedestal[cite: 7].
  * **Center Stage / Orbit Mode ($R = 5\,\text{m}$):** Step directly into the center of the inspection circle[cite: 7]. The pin is calibrated right at **eye level** and travels along an expanded circular path with **fixed spatial orientation** (translational movement without local self-rotation). This enables the viewer in the center to examine all $360^\circ$ angles of the pin simply by turning their head.

* ⚡ **Dynamic Sharpness & Buffer Scaling:** An ultra-flexible resolution slider ranging from **0.01x to 2.00x**, allowing smooth 60+ FPS playback on mobile GPUs[cite: 7].

* 🎛️ **Variable Orbit Speed Controller:** Smooth speed slider scaling from **0.2x to 5.0x** (with a balanced default at 1.0x), enabling everything from slow, meticulous flaw inspection to quick overviews.

* 🎯 **Pore Cloud Decimation / Level of Detail (LOD):** Real-time triangle buffer sampling (5%–100%) with automatic glow compensation so defects remain sharp and visible without lagging mobile devices[cite: 7].

* 🩻 **Inspection Tools:**
  * **Orbit View Switch:** Toggle between exterior pedestal inspection and center-stage circular trajectory.
  * **Speed Slider:** Control the translation and rotation speed in real-time.
  * **X-Ray Mode:** Strips surface reflections and increases opacity transparency to emphasize deep-seated porosity clusters[cite: 7].
  * **Wireframe Mode:** Inspect underlying polygonal density and surface topology[cite: 7].
  * **Live Opacity & Emission Tuners:** Adjust outer metal transparency and micropore glow intensity on the fly[cite: 7].
  * **Motion Toggle:** Pause/resume translation and orbital sweep at any position.

* 📊 **Real-time Performance Monitor:** Displays a live FPS counter, dynamic render resolution, and active inspection status[cite: 7].

## 📂 Repository Structure 📁


```

├── pin_model.glb      # Reconstructed 3D binary model (Pin body + micropore cloud)
├── webvr_app.html     # Single-file WebVR inspection application
└── README.md          # Project documentation and user guide

```
[cite: 7]

## 🛠️ Getting Started & Usage Guide 📖

### 1. Launch the Live WebVR App (Recommended) 🌐

No installation, setup, or builds required![cite: 7] The application is hosted directly via GitHub Pages over a secure **HTTPS** connection (mandatory for mobile browsers to access gyroscope and orientation sensors)[cite: 7]:

👉 [**Launch 3D CT Pin Inspector**](https://drpepperjunkerqueen.github.io/pin-vr/webvr_app.html)[cite: 7]

1. Open the link above in your mobile web browser (**Chrome**, **Safari**, or **Firefox**)[cite: 7].
2. The 3D model loads and calibrates automatically at eye level on the stage[cite: 7].

### 2. Local Testing (Optional for Developers) 💻

If you want to clone this repository and run it locally on your computer[cite: 7]:

```bash
# Clone the repository
git clone [https://github.com/drpepperjunkerqueen/pin-vr.git](https://github.com/drpepperjunkerqueen/pin-vr.git)
cd pin-vr

# Start a quick local web server using Python 3
python -m http.server 8000

```

Then navigate to `http://localhost:8000/webvr_app.html` in your browser.

## 🎮 Navigation & Controls 🕹️

### 🖥️ Desktop / Laptop

| Action | Control |
| --- | --- |
| **Look Around** | Click and drag the left mouse button

 |
| **Move in Lab Space** | `W`, `A`, `S`, `D` keys

 |
| **Center Orbit Toggle** | Click **"Pozycja: Środek"** to step inside the $5\,\text{m}$ ring |
| **Orbit Speed** | Adjust the **"Szybkość obrotu"** slider to speed up or slow down movement |
| **Inspect Parameters** | Use on-screen floating control sliders and toggles

 |
| **Drag & Drop** | Drag any custom `.glb` / `.gltf` model straight into the viewport

 |

### 📱 Mobile & VR Headsets (Google Cardboard / VR Box)

1. Open the web link in landscape mode on your smartphone.


2. Choose your preferred inspection perspective:
* Keep **"Pozycja: Środek"** enabled to stand in the center and track the pin as it circles around you at eye level.
* Toggle it off to inspect the pin on its pedestal from an exterior viewpoint.




3. Adjust the **Szybkość obrotu** slider to your preferred inspection speed.
4. Tap the **VR Goggles Icon** 🥽 at the bottom-right corner of the screen.


5. The viewport automatically divides into a stereoscopic Side-by-Side (SBS) view.


6. Insert your smartphone into the VR headset and examine the pin and defect clusters using natural head movements (gyro-tracking).



## ⚙️ Optimization & Troubleshooting 💡

* **Encountering low FPS on your phone?**
* Slide the **VR Sharpness** slider down to `0.75x` or `0.50x`.


* Adjust the **Pore Cloud LOD** slider to `30%` – `50%`. The app will sample the pore distribution uniformly without hiding clusters.




* **Model doesn't load automatically?**
* Ensure `pin_model.glb` and `webvr_app.html` reside in the exact same directory.


* Alternatively, tap the **"Wczytaj pin_model.glb"** button on the top-right and select the file from your local storage.





## 📜 Technology Stack 🧰

* [A-Frame 1.5.0](https://aframe.io/?utm_source=gemini) – WebVR / WebXR framework
* [Three.js](https://threejs.org/?utm_source=gemini) – WebGL 3D rendering pipeline


* **CT Pipeline:** Micro-CT slice stack $\rightarrow$ Fiji/ImageJ Marching Cubes $\rightarrow$ Blender Decimation & GLTF 2.0 Export



## 📄 License ⚖️

This project is licensed under the [MIT License](https://www.google.com/search?q=LICENSE&utm_source=gemini) – feel free to adapt it for scientific research, engineering analysis, or educational exhibits!