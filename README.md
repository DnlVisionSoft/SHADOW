# SHADOW
SHADOW: Secure Hidden Authenticating Digital Objects in the Wild

# What SHADOW Does
SHADOW implements cancellable biometric authentication on-device using Shadow Authentication Objects (SAOs). Instead of storing raw biometric templates, SHADOW transforms 128-dimensional FaceNet feature vectors through a double exponential-oscillation mapping, binding a revocable certificate to each user’s features. The result is:

Irreversible templates that reveal no raw biometric data
- **Revocable protection**:  simply generate new SAOs to revoke old ones
- **Unlinkability**: statistically isolated templates across enrollments
- **Robustness**: intrinsic defense against brute-force, hill-climbing, and inversion attacks
- **High accuracy**: low Equal Error Rate (EER) and high Area Under Curve (AUC)

In addition to user authentication, SHADOW supports a lightweight challenge–response handshake so that the server can verify the integrity of the client device itself.

Why SHADOW Is Useful
Biometric systems are ubiquitous, but once a template is compromised it cannot be safely revoked. SHADOW overcomes this fundamental weakness by never storing cleartext biometrics outside the device. The SAO construction leverages on-device math to ensure:

- **Security**: raw biometrics remain hidden and irrecoverable
- **Privacy**: unlinkable templates protect user identity
- **Usability**: on-device protection introduces minimal latency
- **Deployability**: compatible with FaceNet feature extractors

# Getting Started
Prerequisites

- MATLAB R2020a or later Signal Processing Toolbox

# Installation

- git clone https://github.com/DnlVisionSoft/SHADOW.git
- cd SHADOW
- addpath(genpath(pwd));

# Sample Files
All biometric feature files (*.txt) live in the samples/ folder. Each file contains 128 real‐valued FaceNet embeddings, and the first four characters of its filename are taken as the user’s ID. You can add new users by copying additional .txt files into samples/.

# App Workflows

**Enroll User**

- Select a sample file from the list box.
- The app loads its 128‐dimensional vector B.
- Computes PCA+rotation (PcaM, Q) → template T.
- Masks T → sends to server → server reconstructs T.
- Server generates key K and constructs SAO → displays SAO parameters.
- Client recovers K.
- Displays “Enrolled” status.

**Verify User**

- Select a sample file from the list box as the query.
- The client computes T from B via PCA+rotation.
- Masks T with HMAC‐based offset → sends <r, T̃> to server.
- Server recovers T, computes SAO‐distance d.
- If d ≤ 𝜏 returns Accept, else Reject.
- Client displays the result.


Getting Help
Documentation: in‐code comments & paper PDF

Maintainers & Contributors
Lead: Prof. D. Riccio (daniel.riccio@unina.it)

Citation
If you use SHADOW, please cite:

D. Riccio, “SHADOW: Secure Hidden Authenticating Digital Objects in the Wild”, 2025.
