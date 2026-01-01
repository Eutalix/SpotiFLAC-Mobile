# Changelog

## [1.2.0] - 2026-01-02

### Added
- **Track Metadata Screen**: New detailed metadata view when tapping on downloaded tracks
  - Material Expressive 3 design with cover art header and gradient
  - Hero animation from list to detail view
  - Displays: track name, artist, album artist, album, track number, disc number, duration, release date, ISRC, Spotify ID, quality, service, download date
  - File info: format (FLAC/M4A), file size, quality badge, service badge with colors
  - Tap to copy ISRC and Spotify ID
  - "Open in Spotify" button to open track in Spotify app/browser
  - File path display with copy functionality
  - Play and Delete action buttons
- **Hi-Res Lossless MAX**: New highest quality option for maximum audio fidelity

### Fixed
- **Hi-Res Quality Bug**: Fixed issue where Hi-Res downloads were stuck at Lossless quality
  - Users on previous versions are recommended to upgrade to get proper Hi-Res downloads
- **Settings Navigation Bug**: Fixed issue where changing settings (like audio quality) would navigate back to Home tab
- **Tidal Badge Color**: Fixed unreadable Tidal service badge (was too bright cyan, now darker blue)

### Changed
- **Recent Downloads**: Tapping on a track now opens metadata screen instead of playing directly
  - Play button still available for quick playback
- **Download History Model**: Extended with additional metadata fields (albumArtist, isrc, spotifyId, trackNumber, discNumber, duration, releaseDate, quality)
- Removed unused `history_screen.dart` and `history_tab.dart` files

## [1.1.2] - 2026-01-01

### Added
- **Update Checker**: Automatic check for new versions from GitHub releases
  - Shows changelog in update dialog
  - Option to disable update notifications
- **Release Changelog**: GitHub releases now include full changelog

### Changed
- Updated version to 1.1.2

## [1.1.1] - 2026-01-01

### Fixed
- **About Dialog**: Custom About dialog with cleaner layout
- **Setup Screen**: Fixed step indicator line alignment
- **Warning Text**: Fixed parallel downloads warning to use Material theme colors
- **Copyright Year**: Updated to 2026

### Changed
- Removed Theme Preview from Settings
- Added MIT License


## [1.1.0] - 2026-01-01

### Added
- **Parallel Downloads**: Download up to 3 tracks simultaneously (configurable in Settings)
  - Default: Sequential (1 at a time) for stability
  - Options: 1, 2, or 3 concurrent downloads
  - Warning about potential rate limiting from streaming services
- **Download Progress Tracking**: Real-time progress for BTS manifest downloads from Tidal
- **History Persistence**: Download history now persists across app restarts using SharedPreferences
- **Connection Pooling**: Shared HTTP transport to prevent TCP connection exhaustion during large batch downloads
- **Connection Cleanup**: Automatic cleanup of idle connections every 50 downloads and at queue end

### Fixed
- **Download Progress Bug**: Fixed 0% → 100% jump by adding proper progress tracking for BTS format downloads
- **TCP Connection Exhaustion**: Fixed slow downloads after ~300 tracks by implementing connection pooling and periodic cleanup
- **Trailing Space in Names**: Fixed download failures when playlist/album/track names have trailing spaces
- **History Loss on Debug**: History no longer disappears when sideloading via `flutter run --debug`

### Changed
- Updated version to 1.1.0

### Technical Details
- Added `concurrentDownloads` field to `AppSettings` model (default: 1, max: 3)
- Implemented worker pool pattern in `DownloadQueueNotifier` for parallel processing
- Added `SetCurrentFile()`, `SetBytesTotal()`, and `ProgressWriter` for BTS downloads in Go backend
- Added `strings.TrimSpace()` to all string fields in `DownloadTrack()` and `DownloadWithFallback()`
- Added shared `http.Transport` with connection pooling in `httputil.go`
- Added `CleanupConnections()` export for Flutter to call via method channel

## [1.0.5] - Previous Release
- Material Expressive 3 UI
- Dynamic color support
- Swipe navigation with PageView
- Settings as bottom navigation tab
- APK size optimization
