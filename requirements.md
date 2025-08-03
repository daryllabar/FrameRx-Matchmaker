
# 📱 Mobile App Requirements

## 1. **Project Overview**
This mobile application is designed to assist health volunteers working in under-resourced areas. The app enables users to match a client’s eyeglass prescription with available frames using an internal database. It functions offline through peer-to-peer Wi-Fi sharing, allowing multiple users to stay synchronized without internet access.

## 2. **Target Users**
- Health volunteers distributing eyeglasses
- Operating in locations with no internet access
- Users with minimal technical background

## 3. **Supported Platforms**
- Android (Android 10 and above)
- iOS (iOS 15 and above)

## 4. **Key Features**

### 4.1 **Offline Peer-to-Peer Sync**
- One user designates their device as the **server**
- Other users connect via local Wi-Fi to the server device
- Data is synced between devices on a local network
- Local device shows **last sync timestamp** (down to the second)

### 4.2 **Server Failover**
- If server fails, users choose the device with the most recent sync
- That user re-establishes server mode
- All other devices reconnect and re-sync

### 4.3 **Database Management**
- Import/export eyeglass frame data via Excel (.xlsx/.csv)
- Frame records include:
  - Left & right lens prescription (Sphere, Cylinder, Axis)
  - Additive power (for bifocals)
  - Frame type (Men’s, Women’s, Children’s)
  - Bag number and frame number (frame number is unique within each bag)

### 4.4 **Search & Match Function**
- Users enter full prescription:
  - Sphere, Cylinder, Axis (for each eye)
  - Additive Power
- App ranks matches and returns:
  - Bag number and frame number
  - Match % overall, plus per eye
  - Frame type
- Filter by frame type and sort by match quality

### 4.5 **Frame Status Management**
- Mark frames as:
  - **Bestowed**: Frame given to a client
  - **Missing**: Frame unaccounted for
- Mark **entire bags** as missing (cascades to all frames in the bag)
- Bestowed and Missing frames are excluded from searches but retained in local database and exports

### 4.6 **Prescription Input UI**
- Streamlined numeric input with:
  - Buttons for 0–15
  - Buttons for decimal values (.00, .25, .50, .75)

## 5. **Data Structure (Simplified)**
```
Frame:
- FrameID (bag + number)
- BagNumber
- FrameNumber
- Type (Men, Women, Children)
- LeftLens: { Sphere, Cylinder, Axis }
- RightLens: { Sphere, Cylinder, Axis }
- AdditivePower
- Status (Available, Bestowed, Missing)

Metadata:
- LastSync: Timestamp
- ServerID
```

## 6. **Technical Requirements**
- **Frontend**: React Native (cross-platform support)
- **Local DB**: SQLite or Realm for offline access
- **Networking**: Peer-to-peer communication via Wi-Fi Direct / local networking (Bonjour, Multipeer Connectivity for iOS)
- **Data Import/Export**: Excel file parser (e.g., SheetJS)

## 7. **Security & Reliability**
- Data integrity checks during sync
- Local backups
- Manual server reassignment with guided steps

## 8. **Performance Goals**
- App opens in <2s
- Sync time <5s for ≤1000 frames
- Efficient battery usage during Wi-Fi sync

## 9. **Future Enhancements (Optional)**
- Barcode scanning for bag/frame lookup
- Language localization
- Prescription tolerance customization for match scoring
