# 🔬 CT Voxel VR: 3D Micro-CT Pin & Defect Inspector 🥽

An interactive, browser-based **WebVR & 3D Tomography Inspection Tool** engineered for non-destructive testing (NDT) analysis. This application visualizes real reconstructed computed tomography (CT) datasets of an engineered pin, allowing users to inspect internal porosity and structural defects in an immersive Virtual Reality environment directly through a smartphone or desktop web browser.

## 📸 Key Features 🚀

* 🕶️ **Full WebVR & Mobile Headset Support:** Built with A-Frame and Three.js. Fully compatible with Google Cardboard, VR Box, and mobile stereoscopic headsets with zero installation required.

* 🔍 **Real Tomography Data Integration:** Visualizes dual-mesh volumetric segmentations: the semi-transparent outer metal pin shell and internal high-contrast defect micropores (`pin_model.glb`).

* 🔄 **Dual Inspection Perspectives & 360° Circular Translation:**
  * **Standard Lab View:** Inspect the rotating pin from an exterior vantage point on an illuminated laboratory pedestal.
  * **Center Stage / Orbit Mode ($R = 10\,\text{m}$):** Step directly into the center of the inspection circle. The pin is calibrated at **eye level** and travels along an expanded circular path with **fixed spatial orientation** (pure translational movement without local self-rotation). This enables the viewer in the center to examine all $360^\circ$ angles of the pin simply by turning their head.

* ⚡ **Dynamic Sharpness & Buffer Scaling:** An ultra-flexible resolution slider ranging from **0.01x to 2.00x**, enabling smooth 60+ FPS playback across mobile GPUs.

* 🎛️ **Variable Orbit Speed Controller:** Smooth speed slider scaling from **0.2x to 5.0x** (with a balanced default at 1.0x), supporting both meticulous flaw evaluation and high-speed overviews.

* 🎯 **Pore Cloud Decimation / Level of Detail (LOD):** Real-time triangle buffer sampling (5%–100%) with uniform spatial decimation, ensuring defects remain sharp across the entire volume without truncating the pin geometry.

* 🩻 **Diagnostic Inspection Toolkit:**
  * **Orbit View Switch:** Toggle between exterior pedestal inspection and center-stage circular trajectory.
  * **Speed Controller:** Regulate translational velocity and rotation rate in real time.
  * **X-Ray Mode:** Strips surface reflections and increases transparency to emphasize deep-seated porosity clusters.
  * **Wireframe Mode:** Inspect underlying polygonal density, triangle topology, and mesh decimation.
  * **Live Opacity & Emission Tuners:** Adjust outer metal transparency and micropore glow intensity on the fly.
  * **Motion Toggle:** Pause and resume orbital translation at any position.

* 📊 **Real-Time Performance Monitor:** Displays a live FPS counter, dynamic render resolution, and active inspection status.

---

## 🛠️ Step-by-Step Development Workflow 📋

Below is the complete engineering pipeline executed throughout the project—spanning from raw micro-computed tomography slices to a live WebVR deployment:

1. **Micro-CT Data Acquisition & Volume Evaluation:**
   * Ingested the raw industrial computed tomography slice stack of the engineered metal pin in DICOM/TIFF format.
   * Analyzed attenuation grayscale histograms corresponding to the solid metal matrix and void regions (micropores).

2. **Segmentation & Volumetric Reconstruction (Fiji / ImageJ):**
   * Imported the slice sequence into Fiji (ImageJ).
   * Applied threshold segmentation to isolate the pin casing from internal defect clusters.
   * Generated dual-layer polygonal surface meshes using the *Marching Cubes* 3D viewer algorithm and exported them as `.stl`/`.obj` assets.

3. **Geometry Optimization & PBR Shading (Blender):**
   * Imported both the outer casing and the defect pore clouds into Blender.
   * Applied decimation modifiers to reduce polygon density, ensuring compatibility with mobile WebGL/GPU constraints.
   * Configured Physically Based Rendering (PBR) materials:
     * *Metal_Transparent* (semi-transparent metallic shell with alpha blending and depth-write controls).
     * *Pory_Glow* (high-visibility emissive shader utilizing the `KHR_materials_emissive_strength` extension).
   * Centered the object coordinates and exported the final scene as a unified binary GLTF asset (`pin_model.glb`).

4. **WebVR Core Architecture & Diagnostics (A-Frame / Three.js):**
   * Implemented the 3D scene graph using A-Frame and Three.js.
   * Built a responsive HUD diagnostic overlay featuring controls for X-Ray rendering, wireframe modes, animation toggles, and dynamic pixel-ratio buffer scaling.

5. **360° Circular Translation Engine:**
   * Designed the center-stage inspection mode, positioning the camera at eye level ($Y = 1.6\,\text{m}$) inside an orbit track ($R = 10\,\text{m}$).
   * Programmed circular translation mechanics with a fixed spatial world orientation (zero local self-rotation). The pin moves along the circumference while preserving its axial direction, allowing users to inspect all lateral sides through natural head tracking.

6. **Volumetric Index-Buffer LOD Sampling:**
   * Replaced linear draw-range truncation (`setDrawRange`) with dynamic index-buffer sampling (`BufferAttribute`).
   * Designed a decimation algorithm that samples triangle index triplets uniformly across the entire length of the pin, preventing model height reduction when lowering pore density.

7. **Deployment & Mobile Headset Testing (GitHub Pages):**
   * Configured continuous deployment through GitHub Pages over secure **HTTPS**, fulfilling mobile browser requirements for WebXR device-orientation and gyroscope APIs.
   * Verified stereoscopic Side-by-Side (SBS) rendering performance and tracking stability on mobile VR headsets (Google Cardboard and VR Box).

---

## 📂 Repository Structure 📁


```

├── pin_model.glb      # Reconstructed 3D binary model (Pin body + micropore cloud)
├── webvr_app.html     # Single-file WebVR inspection application
└── README.md          # Project documentation and user guide

```


---

## 🛠️ Getting Started & Usage Guide 📖

### 1. Launch the Live WebVR App (Recommended) 🌐

No installation, builds, or package managers required! The application runs directly via GitHub Pages over a secure **HTTPS** connection:

👉 [**Launch 3D CT Pin Inspector**](https://drpepperjunkerqueen.github.io/pin-vr/webvr_app.html)

1. Open the link above in a mobile or desktop web browser (**Google Chrome**, **Safari**, or **Mozilla Firefox**).
2. The 3D model will automatically load, calibrate, and initialize at eye level.

### 2. Local Testing (Optional for Developers) 💻

To clone this repository and run it locally:

```bash
# Clone the repository
git clone [https://github.com/drpepperjunkerqueen/pin-vr.git](https://github.com/drpepperjunkerqueen/pin-vr.git)
cd pin-vr

# Start a lightweight local web server using Python 3
python -m http.server 8000

```

Navigate to `http://localhost:8000/webvr_app.html` in your web browser.

---

## 🎮 Navigation & Controls 🕹️

### 🖥️ Desktop / Laptop

| Action | Control |
| --- | --- |
| **Look Around** | Click and drag the left mouse button |
| **Move in Scene** | `W`, `A`, `S`, `D` keys |
| **Center Orbit Toggle** | Click **"Pozycja: Środek"** to step inside the $10\,\text{m}$ ring |
| **Orbit Speed** | Adjust the **"Szybkość obrotu"** slider to speed up or slow down movement |
| **Inspect Parameters** | Use on-screen floating control sliders and toggles |
| **Upload Custom GLB** | Click **"Wczytaj pin_model.glb"** or drag-and-drop a `.glb`/`.gltf` file directly into the viewport |

### 📱 Mobile & VR Headsets (Google Cardboard / VR Box)

1. Open the application link in landscape orientation on your smartphone.
2. Select your preferred inspection mode:
* Keep **"Pozycja: Środek"** active to remain in the center while the pin circles around you at eye level.
* Toggle it off to inspect the pin on its pedestal from an exterior vantage point.


3. Adjust the **Szybkość obrotu** slider to your preferred inspection speed.
4. Tap the **VR Goggles Icon** 🥽 in the bottom-right corner.
5. The display will split into a stereoscopic Side-by-Side (SBS) view.
6. Place your phone into the VR headset and examine the pin and defect clusters using natural head movements.

---

## ⚙️ Optimization & Troubleshooting 💡

* **Experiencing low frame rates on mobile hardware?**
* Move the **Ostrość** (sharpness) slider down to `0.75x` or `0.50x` to reduce GPU fill-rate overhead.
* Lower the **Próbkowanie porów** slider to `30%`–`50%`. The engine will sample the index buffers uniformly without hiding defect clusters or clipping model height.


* **Model fails to load automatically?**
* Verify that `pin_model.glb` and `webvr_app.html` reside in the same root directory.
* Tap the **"Wczytaj pin_model.glb"** button in the top-right corner to select the file manually from local storage.



---

## 📜 Technology Stack 🧰

* [A-Frame 1.5.0](https://aframe.io/) – WebVR / WebXR declarative 3D framework
* [Three.js](https://threejs.org/) – WebGL graphics rendering pipeline
* **Micro-CT Pipeline:** Micro-CT slice stack $\rightarrow$ Fiji/ImageJ Marching Cubes $\rightarrow$ Blender decimation & GLTF 2.0 export

---

## 📄 License ⚖️

This project is licensed under the [MIT License](https://www.google.com/search?q=LICENSE)—feel free to adapt it for scientific research, engineering analysis, or educational exhibits!