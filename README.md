# pixelpipe
# ChromaSync ⚡ (24-Bit Optical Streamer)

A zero-trust, client-side, high-speed optical file transfer protocol. Transfers heavy files locally and remotely by bypassing slow monochrome QR codes in favor of **24-bit raw RGB raster streaming**, native **Gzip stream compression**, and **AES-256-GCM authenticated encryption**.

---

## 🚀 Key Features

* **High-Density 24-Bit Optical Streaming:** Packs binary payload directly into raw RGB pixel values ($1920 \times 1080$ frame yields ~6.22 MB per frame at 3 bytes/pixel).
* **Native In-Browser Pre-Compression:** Uses the browser `CompressionStream` (Gzip) API to shrink text, source code, and databases by 60%–80% before transmission.
* **Hardened Zero-Trust Cryptography:**
  * **AES-256-GCM** authenticated cipher.
  * **600,000-iteration PBKDF2** key derivation.
  * Ephemeral session binding via cryptographic salt and random seed.
  * **3-Attempt Brute-Force Self-Destruct:** Destroys active in-memory payload buffers upon 3 invalid code attempts.
* **Single-Tab Unified Interface:** Sender and Receiver mode switch toggle with real-time frame rasterization and automated de-shrink downloads.
* **100% Client-Side:** Zero external server dependencies or cloud storage.

---

## 📊 Protocol Specifications

| Parameter | Specification |
| :--- | :--- |
| **Raster Resolution** | $1920 \times 1080$ (1080p Full HD) |
| **Color Depth** | 24-bit Truecolor (8 bits Red, 8 bits Green, 8 bits Blue) |
| **Payload per Frame** | ~6.22 MB (6,220,752 bytes raw payload + 48-byte header) |
| **Ingestion Throughput** | Up to 120 FPS via memory/screen pipe (~740 MB/s) |
| **Integrity Verification** | 32-bit hardware-accelerated CRC-32 per slice |
| **Transfer Duration (1 GB)** | ~5 to 15 seconds (shrunk payload depending on entropy) |

---

## 🛠️ How It Works

```text
[SENDER]
Original File ──> Gzip Compression ──> AES-256-GCM Encrypt ──> 24-Bit RGB Raster Frames
                                                                        │
                                                               [Optical / Memory Pipe]
                                                                        │
[RECEIVER]
Download File <── Gzip Decompress <── AES-256-GCM Decrypt <── 6-Digit Code Verified
