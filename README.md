# Smart-voting-system-using-fingerprint-and-facial-recognition-

🗳️ EVM Multi-Factor Authentication System

🔐 Face + Aadhaar + Fingerprint Based Voter Authentication

A Python-based Electronic Voting Machine (EVM) authentication system designed to verify a voter through multiple authentication stages before authorizing the voting process.

The system combines Face Recognition, Aadhaar verification, Fingerprint verification, local voter records, and Firebase communication into a single desktop application.



🚀 Project Overview

The system provides a multi-stage voter authentication workflow:

Voter Registration
       ↓
Face Data Capture
       ↓
Face Model Training
       ↓
Face Authentication
       ↓
Aadhaar Verification
       ↓
Identity Matching
       ↓
Vote Status Check
       ↓
Fingerprint Verification
       ↓
Voting Authorization
       ↓
Firebase / EVM Status

The application also provides a Voting Dashboard that retrieves vote-count information from Firebase.



✨ Key Features

- 👤 Voter registration with:
  - Voter ID
  - Full Name
  - Aadhaar Number
- 📷 Face image capture using OpenCV
- 🧠 LBPH-based face recognition
- 🪪 Aadhaar number validation and matching
- 🔐 Multi-stage authentication
- 👆 Fingerprint verification workflow
- 🚫 Prevents a registered voter from proceeding if their vote status is already marked as cast
- ☁️ Firebase Realtime Database integration
- 📊 Voting statistics dashboard
- 📝 Authentication logs stored in CSV files
- 🕒 Date and real-time clock display
- 🖥️ Graphical user interface using Tkinter
- ⚡ Background Firebase updates using Python threading

The project captures up to 25 face samples during registration and trains an LBPH face-recognition model using the collected images.



🛠️ Technologies Used

Technology| Purpose
Python| Core application development
Tkinter| Desktop GUI
OpenCV| Face detection and image processing
OpenCV Contrib| LBPH face recognition
NumPy| Numerical/image-data processing
Pandas| Voter data handling
Pillow (PIL)| Image loading and processing
CSV| Local voter and authentication records
Firebase Realtime Database| EVM status and voting data
Pyrebase4| Python-Firebase integration
Threading| Non-blocking Firebase updates

The code explicitly checks for "pyrebase4" and "opencv-contrib-python", while importing Tkinter, OpenCV, NumPy, Pillow, Pandas and other standard Python modules.



🔐 Authentication Process

1️⃣ Face Authentication

The application accesses the camera and detects a face using the Haar Cascade classifier.

The detected face is resized and passed to the trained LBPH Face Recognizer.

If the recognized voter matches a registered record, the system retrieves the associated:

- Voter ID
- Name
- Aadhaar number

The face-authentication stage has a timeout and checks the recognition confidence before accepting the result.



2️⃣ Aadhaar Verification

After successful face authentication, the voter enters their Aadhaar number.

The application:

1. Validates that the input contains 12 digits.
2. Searches the voter database.
3. Handles different stored Aadhaar representations.
4. Retrieves the corresponding voter ID and name.
5. Compares the Aadhaar and voter ID information obtained from both authentication stages.

Only when the records correspond to the same voter does the process continue.



3️⃣ Vote Status Verification

Before proceeding to fingerprint verification, the system checks the voter's "VOTE" status in "VoterDetails.csv".

VOTE = 0
   ↓
Voting process can proceed

VOTE = 1
   ↓
Vote already cast
   ↓
Authentication stopped

When a voter is allowed to proceed, the local vote-status field is updated to "1".



4️⃣ Fingerprint Verification

After successful Face + Aadhaar authentication, the application starts the fingerprint-verification stage.

The current implementation uses a 10-second timed simulation and communicates the fingerprint-verification status to Firebase.

After completion, the system marks the voter as authorized and updates the relevant Firebase status values.

«Note: The current Python implementation does not contain direct fingerprint-sensor communication; the fingerprint stage is simulated through the application workflow.»



☁️ Firebase Integration

Firebase Realtime Database is used for communication between the authentication application and the connected EVM system.

The application updates and retrieves information such as:

EVM Start Status
Fingerprint Verification Status
Blink / Scanning Status
Voting Log
Vote Count

The voting dashboard retrieves candidate vote counts from Firebase and refreshes the displayed statistics periodically.



📊 Voting Dashboard

The application contains a separate dashboard view for displaying voting statistics.

Example:

Voting Statistics:

Candidate 1: 25 votes
Candidate 2: 18 votes
Candidate 3: 31 votes

The dashboard reads the vote-count data from Firebase and updates the display every 5 seconds.



🗂️ Data Storage

Voter Details

Voter information is stored locally in:

VoterDetails/
└── VoterDetails.csv

The database contains information including:

Serial Number
Voter ID
Name
Aadhaar
Fingerprint Status
Vote Status



Face Training Data

Captured face images are stored in:

TrainingImage/

The trained LBPH model is stored in:

TrainingImageLabel/
└── Trainner.yml

The application loads the captured images, converts them to grayscale arrays, associates them with voter IDs, and trains the LBPH recognizer.



Authentication Logs

Authentication events are stored in:

AuthenticationLog/
└── Authentication_DD-MM-YYYY.csv

The logs can record events such as:

- Authorized authentication
- Authentication mismatch
- Already voted
- Face + Aadhaar mismatch

The code writes authentication records to date-based CSV files.



🖥️ Graphical User Interface

The application is built using Tkinter and contains:

Authentication Panel

- Start Face Authentication
- Aadhaar input
- Verify Aadhaar
- Reset Authentication
- Authentication status

Voter Registration Panel

- Voter ID input
- Name input
- Aadhaar input
- Face-image capture
- Fingerprint scanning workflow
- Profile/model training

Voting Dashboard

- Candidate vote counts
- Refresh Data button
- Firebase-based statistics

The main application window is designed at "1280 × 720" and contains separate authentication, registration and dashboard sections.



📁 Project Structure

EVM-Dual-Authentication/
│
├── vote1.py
├── haarcascade_frontalface_default.xml
│
├── VoterDetails/
│   └── VoterDetails.csv
│
├── TrainingImage/
│   ├── voter_face_images.jpg
│   └── ...
│
├── TrainingImageLabel/
│   └── Trainner.yml
│
└── AuthenticationLog/
    ├── Authentication_DD-MM-YYYY.csv
    └── ...



⚙️ Installation

1. Clone the repository

git clone https://github.com/your-username/EVM-Dual-Authentication.git
cd EVM-Dual-Authentication

2. Install Python dependencies

pip install opencv-python
pip install opencv-contrib-python
pip install numpy
pip install pandas
pip install pillow
pip install pyrebase4

Tkinter is normally included with standard Python installations on Windows.

3. Required Haar Cascade

Place:

haarcascade_frontalface_default.xml

in the same directory as "vote1.py".

The application checks for this file before performing face-related operations.



▶️ Running the Project

Run:

python vote1.py

Then follow the application workflow:

Register Voter
     ↓
Capture Face Images
     ↓
Train Face Model
     ↓
Start Face Authentication
     ↓
Enter Aadhaar
     ↓
Verify Identity
     ↓
Check Vote Status
     ↓
Fingerprint Verification
     ↓
Voting Authorization



🔄 System Workflow

                 ┌──────────────────┐
                 │ Voter Registration│
                 └────────┬─────────┘
                          ↓
                 ┌──────────────────┐
                 │ Face Data Capture│
                 └────────┬─────────┘
                          ↓
                 ┌──────────────────┐
                 │ LBPH Model Train │
                 └────────┬─────────┘
                          ↓
                 ┌──────────────────┐
                 │ Face Recognition │
                 └────────┬─────────┘
                          ↓
                 ┌──────────────────┐
                 │ Aadhaar Verify   │
                 └────────┬─────────┘
                          ↓
                ┌────────────────────┐
                │ Identity Match?    │
                └───────┬─────┬──────┘
                        │Yes  │No
                        ↓     ↓
               ┌────────────┐  Reject
               │ Vote Status│
               │   Check    │
               └─────┬──────┘
                     ↓
             ┌──────────────────┐
             │ Fingerprint Step │
             └────────┬─────────┘
                      ↓
             ┌──────────────────┐
             │ Voting Authorized│
             └────────┬─────────┘
                      ↓
                 ┌──────────┐
                 │ Firebase │
                 └──────────┘



🎯 Project Objectives

- Develop a multi-factor voter authentication workflow.
- Combine computer vision with voter-data verification.
- Maintain a local voter registration database.
- Prevent a voter from proceeding after their vote status is already marked as cast.
- Communicate authentication states with an EVM through Firebase.
- Provide a simple desktop interface for registration and authentication.
- Display voting statistics through a Firebase-connected dashboard.


🧠 Concepts Demonstrated

This project demonstrates practical implementation of:

- Python GUI programming
- File handling
- CSV data management
- Pandas DataFrames
- Computer vision
- Face detection
- Face recognition
- LBPH algorithm implementation through OpenCV
- Image preprocessing
- Input validation
- Authentication state management
- Firebase Realtime Database
- Multithreading
- Event-driven programming
- Exception handling
- Local logging
- Real-time dashboard updates



🔮 Future Improvements

Possible improvements to the current implementation include:

- 🔐 Integrate a real fingerprint sensor instead of the current timed simulation.
- 🔒 Move sensitive voter information away from plain CSV storage.
- 🔑 Store Firebase credentials securely using environment variables.
- 🛡️ Add stronger authentication and access-control mechanisms.
- 📱 Add an administrator authentication system.
- 📈 Improve the voting dashboard with graphical statistics.
- 🗄️ Use a proper database instead of relying primarily on CSV files.
- 🔏 Encrypt sensitive voter information.
- 🧪 Add automated testing for authentication and voter-status logic.
- 🌐 Separate the GUI, authentication logic and database layer into independent modules.


⚠️ Security Note

This project is an educational/prototype implementation, not a production-ready electronic voting system.

The source code currently contains Firebase configuration information directly in the Python file. Before publishing this repository publicly, remove exposed credentials/configuration and move sensitive configuration to environment variables or another secure configuration mechanism.

Similarly, Aadhaar and biometric-related information should not be exposed in a public repository.


📌 Project Status

Current Status: Prototype / Academic Project

Implemented

- [x] Voter registration
- [x] Face image capture
- [x] Face model training
- [x] Face authentication
- [x] Aadhaar validation
- [x] Face + Aadhaar identity matching
- [x] Vote-status checking
- [x] Fingerprint-verification workflow
- [x] Firebase communication
- [x] Authentication logging
- [x] Voting dashboard

Planned / Hardware Integration

- [ ] Real fingerprint sensor integration
- [ ] Complete EVM hardware integration
- [ ] Production-grade secure database
- [ ] Secure credential management
- [ ] Stronger biometric security mechanisms



👨‍💻 Author

Kiran kumar

Electronics & Communication Engineering
Embedded Systems & VLSI Technologies


⭐ Acknowledgement

Built as an academic/project implementation exploring the integration of:

Python + Computer Vision + Biometrics + Firebase + EVM Authentication
