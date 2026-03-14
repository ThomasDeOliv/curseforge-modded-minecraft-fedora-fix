# CurseForge crash on Fedora when launching clients for specific modded servers

## Problem

Launching modded Minecraft clients with [CurseForge](https://www.curseforge.com/) on [Fedora](https://fedoraproject.org) may cause a crash.

## Investigation

After debugging, the crash appeared to originate from a conflict between [PipeWire](https://pipewire.org/) and [OpenAL Soft](https://openal-soft.org/).
The error was thrown directly at the audio driver level.

## A solution that worked for me

Create the file .alsoftrc in your home directory (~/.alsoftrc) with the following content:
```ini
[general]
drivers=pulse
hrtf=true
```

This forces OpenAL to use the PulseAudio backend (provided by pipewire-pulse), resolving the conflict.

## References
- [Minecraft crashing from OpenAL - r/linux_gaming](https://www.reddit.com/r/linux_gaming/comments/18qjnwk/minecraft_crashing_from_openal/)
