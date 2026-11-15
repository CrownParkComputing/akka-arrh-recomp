# Development

Akka Arrh uses Llamasoft's native Neon/global framework, SCREAM audio and NGS2.
Linux maps the x86-64 executable directly; Android executes it through FEXCore.
The C runtime replaces PS4 services, and shadPS4 translates GNM/GCN to Vulkan.

`run.py prepare` reconstructs the executable, links libc/Fios2 and registers
other modules for deferred loading. `run.py check` reports unresolved main-image
imports; only a real boot verifies the dependencies' startup paths too.
An unsupported import traps and prints its caller instead of returning success.

Read [building.md](building.md) and [akka-port-status.md](akka-port-status.md).
Shared runtime configuration names are `TEMPEST_*`. Isolate runtime experiments
with `--user out/check/user` and `TEMPEST_GPU_USER_DIR=out/check/gpu`.
Frame/audio diagnostics are enabled with `TEMPEST_FRAME_STATS=1` and
`TEMPEST_AUDIO_STATS=1`. PCM sound is not counted by ATRAC9-only music counters.

The original package has 190 stereo 44.1 kHz PCM16 waves. Its resource XML says
there are no standalone soundtracks. Do not reuse Tempest's track-number table.
Game-specific address hooks are intentionally inert until independently verified.

Upstream historical docs under legacy describe earlier games and are not Akka's
runtime contract or verification record.
