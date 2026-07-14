# Hiking Trail Navigator

**Integrated Trail Discovery and Safety Platform** - React Native/Expo + Express

![Platform](https://img.shields.io/badge/platform-React%20Native-blue)
![Framework](https://img.shields.io/badge/framework-Expo%2054-green)
![License](https://img.shields.io/badge/license-MIT-orange)

## Overview

Hiking Trail Navigator is a comprehensive mobile application designed for outdoor enthusiasts, providing real-time trail navigation, safety monitoring, and emergency response capabilities. Built with React Native and Expo, it delivers a seamless cross-platform experience for hikers exploring trails in the Western Ghats region of Karnataka, India.

## Features

### Trail Discovery & Navigation
- **Interactive Map View** with trail polylines, markers, and layer controls
- **8 Pre-loaded Trails** in Karnataka (Kudremukh, Mullayyanagiri, Coorg Brahmagiri, etc.)
- **Trail Search & Filtering** by difficulty, region, and popularity
- **Real-time Navigation** with distance, elevation, and ETA tracking
- **Route Deviation Alerts** with distance from trail

### Safety & Emergency
- **Emergency SOS Button** with pulse animation and haptic feedback
- **Fall Detection** using device accelerometer sensors
- **Periodic Safety Check-ins** with configurable intervals
- **Silent SOS Mode** for discreet emergency alerts
- **Live Location Sharing** with emergency contacts
- **Danger Zone Warnings** and hazard reporting

### Offline Capabilities
- **Offline Mode** for areas without network coverage
- **Offline Storage Service** using AsyncStorage
- **No Coverage Zone Mapping** on the map

### Activity Tracking
- **Real-time Hike Stats** (duration, distance, elevation gain)
- **Activity History** with completed hike summaries
- **Route Recording** with GPS waypoints

### Weather & Risk Assessment
- **Weather Integration** with alerts for dangerous conditions
- **Dynamic Risk Level Assessment** (low/medium/high/critical)
- **Network Status Monitoring** (connected/offline, signal strength)

## Tech Stack

| Layer | Technology |
|-------|------------|
| **Frontend** | React Native 0.81, Expo 54 |
| **Navigation** | React Navigation 6 (Bottom Tabs + Native Stack) |
| **State Management** | React Context + useReducer |
| **Maps** | react-native-maps |
| **Location** | expo-location (GPS tracking) |
| **Sensors** | expo-sensors (accelerometer for fall detection) |
| **Storage** | @react-native-async-storage/async-storage |
| **Haptics** | expo-haptics |
| **Notifications** | expo-notifications |
| **UI Components** | Custom components with Ionicons |

## Project Structure

```
hiking-trail-navigator/
├── App.js                    # Root component with providers
├── src/
│   ├── components/           # Reusable UI components
│   │   ├── EmergencyButton.js
│   │   ├── SafetyCheckInModal.js
│   │   ├── WeatherAlert.js
│   │   └── NoNetworkWarning.js
│   ├── constants/            # Theme, trail data, danger zones
│   │   ├── theme.js          # Colors, typography, spacing
│   │   ├── trailData.js      # 8 trail definitions
│   │   └── dangerZones.js    # Danger/coverage/unexplored zones
│   ├── navigation/           # React Navigation setup
│   │   └── AppNavigator.js   # Tab + Stack navigators
│   ├── screens/              # Screen components
│   │   ├── HomeScreen.js
│   │   ├── TrailDiscoveryScreen.js
│   │   ├── TrailDetailScreen.js
│   │   ├── NavigationScreen.js
│   │   ├── SafetyDashboardScreen.js
│   │   ├── SOSScreen.js
│   │   ├── HazardReportScreen.js
│   │   ├── LiveTrackingScreen.js
│   │   ├── EmergencyContactsScreen.js
│   │   ├── ActivityScreen.js
│   │   ├── ActivityHistoryScreen.js
│   │   ├── ProfileScreen.js
│   │   └── SettingsScreen.js
│   ├── services/             # Business logic services
│   │   ├── LocationService.js
│   │   ├── ConnectivityService.js
│   │   ├── EmergencyService.js
│   │   ├── FallDetectionService.js
│   │   ├── GeofencingService.js
│   │   ├── OfflineStorageService.js
│   │   ├── RiskAssessmentService.js
│   │   ├── SafetyCheckInService.js
│   │   ├── TrailService.js
│   │   └── WeatherService.js
│   └── store/                # State management
│       └── AppContext.js     # Global state with useReducer
├── backend/                  # Express backend (optional)
├── android/                  # Android native code
├── assets/                   # Images, icons
└── screenshots/              # App screenshots
```

## Architecture

### State Management Flow

```
┌─────────────────────────────────────────────────────────────┐
│                        AppContext                            │
│  ┌─────────────────────────────────────────────────────┐   │
│  │                    State                             │   │
│  │  • user (profile, preferences, emergency contacts)  │   │
│  │  • currentHike (active hike data, route, stats)     │   │
│  │  • safetyStatus (SOS, fall detection, check-ins)    │   │
│  │  • hazards (reported hazards)                       │   │
│  │  • activities (hike history)                        │   │
│  │  • networkStatus (connectivity state)               │   │
│  │  • weather (current conditions, alerts)             │   │
│  └─────────────────────────────────────────────────────┘   │
│                           │                                 │
│                           ▼                                 │
│  ┌─────────────────────────────────────────────────────┐   │
│  │                  Dispatch Actions                    │   │
│  │  START_HIKE, END_HIKE, UPDATE_LOCATION, CHECK_IN    │   │
│  │  TRIGGER_SOS, CANCEL_SOS, FALL_DETECTED, etc.       │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

### Navigation Architecture

```
Bottom Tab Navigator
├── Home (Stack)
│   └── HomeScreen
├── Trails (Stack)
│   ├── TrailDiscoveryScreen
│   └── TrailDetailScreen
├── Navigate (Stack)
│   ├── NavigationScreen
│   ├── ActivityScreen
│   └── ActivityHistoryScreen
├── Safety (Stack)
│   ├── SafetyDashboardScreen
│   ├── SOSScreen
│   ├── HazardReportScreen
│   ├── LiveTrackingScreen
│   └── EmergencyContactsScreen
└── Profile (Stack)
    ├── ProfileScreen
    └── SettingsScreen
```

### Service Layer

| Service | Responsibility |
|---------|----------------|
| **LocationService** | GPS permissions, location tracking, distance calculation |
| **GeofencingService** | Route deviation detection, danger zone monitoring |
| **FallDetectionService** | Accelerometer monitoring, fall event detection |
| **EmergencyService** | SOS alerts, emergency contact notification |
| **SafetyCheckInService** | Periodic check-in scheduling and management |
| **ConnectivityService** | Network status monitoring, offline mode |
| **OfflineStorageService** | AsyncStorage operations for offline data |
| **RiskAssessmentService** | Dynamic risk level calculation |
| **WeatherService** | Weather data and alerts |
| **TrailService** | Trail data management and filtering |

## Key Components

### EmergencyButton
- Pulse animation when SOS is active
- Haptic feedback on press
- Configurable sizes (small/medium/large)
- Accessibility support

### SafetyCheckInModal
- Periodic check-in prompts
- Countdown timer
- Auto-triggers SOS if not acknowledged

### Map Layers
- **Danger Zones** (red circles) - areas with hazards
- **No Coverage Zones** (gray circles) - areas without network
- **Unexplored Areas** (purple circles) - unmapped regions
- **Hazard Markers** - user-reported hazards

## Getting Started

### Prerequisites
- Node.js 18+
- Expo CLI
- Android Studio / Xcode

### Installation

```bash
# Clone the repository
git clone https://github.com/poornesh0604/hiking-trail-navigator.git
cd hiking-trail-navigator

# Install dependencies
npm install

# Start Expo development server
npx expo start

# Run on Android
npx expo run:android

# Run on iOS
npx expo run:ios
```

### Environment Setup

1. Install Expo CLI globally:
```bash
npm install -g expo-cli
```

2. Configure app.json with your Expo project ID

3. For Android, configure signing in `android/app/build.gradle`

## App Screens

### Home Screen
- Interactive map with all trails
- Search bar for trail discovery
- Layer toggle buttons (danger zones, coverage, unexplored)
- Real-time risk level badge
- Quick SOS access

### Trail Discovery
- List/grid view of all trails
- Filter by difficulty, region, popularity
- Trail cards with distance, duration, rating

### Navigation Screen
- Real-time map with user location
- Route polyline and deviation alerts
- Elapsed time, distance, elevation stats
- Pause/Resume/End hike controls
- Periodic safety check-in modals

### Safety Dashboard
- Current safety status indicator
- Quick action buttons (SOS, Share Location, Report Hazard, Contacts)
- Safety feature toggles
- Risk level display
- Network status

### SOS Screen
- Large emergency button
- Emergency contact list
- Silent SOS option
- Cancel SOS functionality

## Safety Features

1. **Automatic Fall Detection**: Uses accelerometer to detect falls and prompt user response
2. **Periodic Check-ins**: Configurable intervals (default 60 min) with auto-SOS
3. **Route Deviation Alerts**: Warns when hiker strays from trail
4. **Live Location Sharing**: Share real-time location with emergency contacts
5. **Danger Zone Warnings**: Visual alerts for hazardous areas
6. **Offline Safety**: Core features work without network connectivity

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- React Native and Expo teams for the amazing framework
- Western Ghats hiking community for trail data inspiration
- All contributors and testers

---

**Built with love for the hiking community**
