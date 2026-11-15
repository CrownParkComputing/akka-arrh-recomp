# Akka Arrh native port

Linux x86-64 and Android ARM64 port workspace for the PS4 game Akka Arrh
(CUSA36609 v1.00), based on the Tempest 4000 runtime and shadPS4 renderer.

The original executable, modules and game assets remain under ignored `game/`;
prepared images and build products are under ignored `out/`. Game executables, audio and level data are
excluded from the source repository and APK. Launcher artwork is read from the
local dump during APK packaging.

Build Linux with `bash build.sh`, then `./play-akka-arrh.sh`. Preparation reads
`game/` by default or `--game /path/to/dump`. The tested executable SHA-256 is
`d6a1c0a179b4d9a4a9884c3f2e172db9d262bc8f33107335b9d03bb799075cfb`.

Android uses `com.crownparkcomputing.akkaarrh`, separately from Tempest and
PAC-MAN. Bundled Turnip is the default. L3 + R3 toggles the internal settings
menu; its Graphics driver row offers system-driver selection and importing an
ARM64 driver ZIP, applied on the next launch.

Linux title and introductory gameplay run at 60 FPS. Android device validation
is in progress. Shared configuration
names remain `TEMPEST_*`. Akka Arrh's native frame/aspect hooks do not patch any
addresses copied from another game.

See [build instructions](docs/building.md), [Android](android/README.md) and
[current status](docs/akka-port-status.md).
