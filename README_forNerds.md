# Technical Readme: "🎪 Is The Circus Open? 🎪"

This project uses facial detection to determine if the "circus is open" by detecting a user's nose in real-time using the front-facing camera.
When a face is detected it draws on it a red nose 🔴
To try it out, just click [here](https://alvarofergar.github.io/ITCO/).


---

## **Key Components 🤹**

### **1. Face API**
- [face-api.js](https://github.com/justadudewhohacks/face-api.js) is a lightweight api to develop face detection in browsers, built on top of the tensorflow.js core API 
- To make it work, pre-trained models were directly downloaded into the _models_ folder of the repository. You can find these and similar models [here](https://github.com/justadudewhohacks/face-api.js/tree/master/weights)  
- Loads pre-trained models for facial detection and landmark tracking (`tinyFaceDetector` and `faceLandmark68TinyNet`). 
- Detects the nose using landmark index `30`.

```javascript
await faceapi.nets.tinyFaceDetector.load('models');
await faceapi.nets.faceLandmark68TinyNet.load('models');

...

const detections = await faceapi.detectAllFaces(video).withFaceLandmarks(true);
const noseCenter = detections[0]?.landmarks.positions[30]; // Nose landmark
```

### 2. **Access selfie camera**

Requests access to the front-facing camera of the mobile using facingMode: 'user'.

```javascript
if (!navigator.mediaDevices || !navigator.mediaDevices.getUserMedia) {
    throw new Error('Your browser does not support camera access.');
}

// Request permission to access the camera
stream = await navigator.mediaDevices.getUserMedia({
    video: {
        facingMode: 'user' // Use the selfie camera
    },
    audio: false
});
```

## **Project Structure 🤡**

```
ITCO/
├── index.html
├── models/
│   └── (face-api.js models)
├── assets/
│   └── (web logo)
└── README_forNerds.md
└── README.md
```
