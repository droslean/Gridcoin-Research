# Change Log
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/)
and this project adheres to [Semantic Versioning](http://semver.org/).

## Unreleased
### Added
### Changed
 - Staking cleanup, #301 (@tomasbrod). This also solves several other issues:
 - UI:
    - Wallet window can now be made smaller, #384 (@skcin). 
    - Interest and Research subsidy visible in getmininginfo (@tomasbrod).
    - External links now use HTTPS where possible, and the code has been cleaned
      up, #339 (@skcin).
    - Rearrange menu items to reduce the number of entries. Remove references
      to broken function, #362 (@skcin).
 - Replace translations which were just question marks with new files from
   the Bitcoin source tree: Arabic, Belarusian, Bulgarian, Greek, Persian,
   Hebrew, Hindi, Japanese, Georgian, Kirghiz, Serbian, Thai, Ukranian,
   Urdu and Chinese.
 - Don't print the "Bootup" and "Signing block" messages unless fDebug (@tomasbrod). 
 - Print beacons as they are loaded and debug3=true (@tomasbrod).
 - Show superblock information in getblock (@tomasbrod).
 - Code cleanup (@skcin).

### Fixed
 - High CPU usage, #349 (@tomasbrod)
 - Repetetive block signing, #295 (@tomasbrod)
 - Staking creates 1 cent output, #311 (@tomasbrod)
 - Client no longer has be restarted for a beacon to activate, #253
   (@Foggyx420).

### Removed
 - Removed newbie boost, #332
 - Removed obsolete functionality.

## [3.5.9.2] - 2017-07-04
### Fixed
 - Fix neural network project gather bug related to timezones.

## [3.5.9.1] - 2017-07-03
### Changed
 - Neural Network improvements:
    - Don't download stats data that hasn't changed.
    - Use gridcoin.us as a stat mirror to reduce BOINC server loads.
    - Use UTC instead of local time when filtering idle CPIDs.
    - Only include beacons younger than 6 months when calculating mags.

### Security
 - Prevent untauthorized poll and vote deletions.

## [3.5.9.0] - 2017-06-05
### Added
 - Added execute unspentreport (shows proof of unspent coins in wallet).
 - Add RPC commands for changing debug flags: debug, debugnet, debug2, debug3,
   debug4, debug5, debug10. #309 (@Foggyx420).
 - Add support for themes via stylesheets, #233 (@skcin).
 - Add support for OpenSSL 1.1.x, #164.
 - BOINC data dir auto detection, #242 (@3ullShark)
 - Add install (make install) target for UNIX systems.
 - Add aarch64 support, #151 (@datenklause).
 - Add diagnostic message for if web lookup fails for cpid valid test,
   #175 (@fooforever).

### Changed
 - Wallet overview cleanup, #233 (@skcin)
    - The main overview page is now cleaner, more structured and holds more of
     the recent transactions.
    - Displayed DPOR weight should now be accurate, #233 (@skcin).
 - Show as many of the recent transactions as we can fit on the overview page.
 - Translation updates
    - Portuguese (Miguel Veiga)
    - Slovak (@tomasbrod)
    - Swedish (@denravonska)
    - Afrikaan and Spanish (@philipswift)
    - French (@PsiPhiTheta)
    - Russian (@rambinho)
 - Gridcoinstats is now used as block explorer, #308.
 - Slight RAM usage reduction.
 - Improve beacon advertise error message, #133 (@comprehendreality).
 - Code cleanup (@Foggyx420, @TheCharlatan).

### Fixed
 - Fix numerous beacon issues, #344, #321 and #334 (@Foggyx420).
 - Fix incorrect WCG URL, #323 (@3ullShark).
 - Fix alt key shortcut order, #326 (@TheCharlatan).
 - Fix a bug where beacons were stored even though none were generated due
   to the wallet being locked, #264 (@denravonska).

### Removed
 - Remove empty "wcgtest" RPC command.

### Security
 - Security enhancement (@tomasbrod)
 - Upgraded security on voting system - voting proof of balance and proof of
   magnitude.

## [3.5.8.9] - 2017-05-15
### Added
- Implement voting functionality for Linux and OSX (@skcin).
- Add man pages to doc folder, #135 (@caraka).

### Changed
 - Windows are now resizable 
 - Replace Windows voting dialog with the new dialog.
 - Update Gridcoin icon on Windows.
 - Enable C++11.
 - Update Hungarian translations (@matthew11).
 - Update Portuguese translations (Miguel Veiga).
 - Update icon set by @Peppernrino.
 - Update icon on OSX, #193 (@coagmano).
 - Lossless compression of resources, #227 (@Peppernrino).
 - Reduced memory usage by around 100MB+.
 - Improve UI when used with dark themes on Linux, #222 (@skcin).

### Fixed
 - Fix OSX build issues, #174 (@coagmano).
 - Fix occasional crashes when starting on Linux, #139.
 - Fix freeze when clicking on the "Amount" field under Send Coins when using
   KDE, #210.
 - Possible fix for invalid time check in diagnostic.

### Removed
 - Remove lots of dead, obsolete code.
 - Removed unused link dependencies: librt, boost_chrono, boost_date_time, libz
   and libdl.