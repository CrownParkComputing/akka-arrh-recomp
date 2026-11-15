# Akka Arrh port status

Input: CUSA36609 v1.00, executable SHA-256
`d6a1c0a179b4d9a4a9884c3f2e172db9d262bc8f33107335b9d03bb799075cfb`.
The original game remains a private local input. This is a native PS4 runtime
port, using direct x86 execution on Linux and FEXCore on Android ARM64.

## Verified on Linux

- libc and Fios2 initialize; the original main entry runs.
- Title, score table and introductory gameplay render. Measured stable intervals
  run at 60.0 FPS on the host RTX3060, with median frame time 16.67 ms.
- Both audio ports submit approximately 469 buffers per 5 seconds, with zero
  starvation in the measured runs. Actual output contains nonzero PCM; this
  does not independently verify every music cue or effect.
- The SaveData thread creates SAVEDATA00 and writes TEST_SAVEDATA.bin.
- Original fonts, logo, starfield and gameplay geometry are visible in captures.
- User reported title text flashing over other text with the inherited draw
  pipeline enabled. A controlled `TEMPEST_DRAW_PIPE=0` run clears the issue,
  confirmed by the user, while retaining60FPS. Serial draw recording is now the
  default. `TEMPEST_DRAW_PIPE=1` remains a diagnostic override; the exact race
  in the parallel recording path is not proven.

## Boot contracts corrected

The package stores lower-case `assets`, while the executable requests
`/app0/Assets/Localisation/Akka_Strings_PS4_Eng.csv`. A mount alias resolves
this without changing the dump. The missing UI resources caused the initial
null dereference at guest0x3e717; it was not an audio-handle fault.

SDK libc uses POSIX pthread condition-variable broadcasts while releasing C++
guards. The shared runtime's real condition-variable implementation handles
its NID, including zero-initialized static conditions. SFO ATTRIBUTE0x810002
selects SDK CPU mode5. No fixed addresses from Tempest or CE2 are patched.

Audio bank inspection identifies190 stereo 44,100 Hz PCM16 waves. The resource
XML explicitly says Akka has no standalone soundtracks. The game controls
sequencing; Tempest's fixed track mapping is not used.

## Android structure

Separate package `com.crownparkcomputing.akkaarrh`, label Akka Arrh. ARM64 main,
headless boot and FEX checks compile. The bundled driver is Standard Turnip 27,
November11 build r2, containing the KGSL zero-timeout fix verified for CE2.

L3+R3 toggles Settings. Graphics driver opens the Android selector with Bundled,
System and Import driver ZIP. The importer validates metadata, ARM64 ELF and
Android API, stores immutable hash-named libraries and applies changes at the
next launch. The launcher shortcut provides recovery independently of rendering.

Android device rendering, sustained gameplay/audio and physical menu checks
remain pending. The user's current Retroid game is left running until a test
is authorized. Linux 60FPS does not establish Retroid performance.

## Checks

The native C/C++ runtime/renderer suite passes, including pad menu shortcut tests.
Python:90 checks, 18 skipped for unavailable optional inputs. Driver ZIP fixtures
and the actual bundled Turnip library hash pass. Android packaging checks its
signature. Game files, driver ZIPs and signing keys are excluded from Git.

Private retained evidence lives under `out/`: package/artifact inventories,
audio-audit, kernel-contract, linux-boot-4, linux-play-check and linux-title-serial.
Historical docs in legacy describe other games and do not establish Akka status.
