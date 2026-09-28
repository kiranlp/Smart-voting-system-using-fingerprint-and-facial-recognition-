 Smart-voting-system-using-fingerprint-and-facial-recognition

🗳️ EVM Dual Authentication System

A Python-based Electronic Voting Machine (EVM) authentication system that combines face recognition, Aadhaar verification, and fingerprint verification before authorizing a voter.

🔐 Authentication Flow

Face Recognition → Aadhaar Verification → Identity Matching → Fingerprint Verification → Voting Authorization

✨ Features

- 👤 Voter registration with Voter ID, Name and Aadhaar
- 📷 Face image capture and recognition using OpenCV
- 🧠 LBPH-based face recognition model
- 🪪 12-digit Aadhaar validation and verification
- 🔗 Face and Aadhaar identity matching
- 🖐️ Fingerprint verification workflow with Firebase status updates
- 🚫 Prevents a registered voter from voting more than once
- ☁️ Firebase integration for EVM and voting status
- 📊 Voting dashboard with vote-count display
- 📝 Authentication logs stored in CSV files
- 🖥️ Tkinter-based graphical user interface

⚙️ How It Works

1. Register voter details and capture face images.
2. Train the face recognition model using the registered images.
3. Authenticate the voter using face recognition.
4. Enter and verify the registered Aadhaar number.
5. Compare the face and Aadhaar details to confirm they belong to the same voter.
6. Check whether the voter has already cast a vote.
7. Complete the fingerprint verification workflow.
8. Authorize the voter and update the relevant Firebase status.

🛠️ Technologies Used

- Python
- Tkinter – GUI
- OpenCV – Face detection and recognition
- LBPH Face Recognizer – Face model
- Firebase / Pyrebase4 – Database and status communication
- Pandas & NumPy – Data processing
- CSV – Voter details and authentication logs
- Pillow (PIL) – Image processing

📁 Main Data

- "VoterDetails/" – Registered voter information
- "TrainingImage/" – Captured face images
- "TrainingImageLabel/" – Trained face-recognition model
- "AuthenticationLog/" – Authentication records

🎯 Project Objective

To demonstrate a multi-step voter authentication workflow using computer vision, identity verification, biometric verification, local data storage, and Firebase communication.
