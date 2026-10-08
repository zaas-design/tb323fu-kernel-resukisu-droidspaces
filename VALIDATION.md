# Validation snapshot

Test device: Lenovo Legion Y700 Gen 5 (TB323FU), ZUXOS 2.0.11.043, unlocked bootloader, active slot A.

On 2026-10-07, the matched `boot_a`, `system_dlkm_a`, and `vbmeta_a` test candidates were written through fastbootd. Android completed boot on kernel release `6.12.30-android16-5-g0baa65ffa8964-ab10018892-4k`. Root was available; `rust_binder` was live in `/proc/modules`; Gunyah modules `gh_rm_drv`, `gh_arm_drv`, `gh_dbl`, and `gh_msgq` were present. `/system_dlkm` mounted read-only through the dm-verity mapper.

Post-write readback for all three targets matched the respective candidate bytes exactly. The exact SHA-256 values are listed in `kernel/final/SHA256SUMS.txt`.

This records a first successful boot only. The captured runtime scan did not find AVB/verity/Binder CRC/unknown-symbol matches in the available dmesg buffer, but that is not a complete boot log analysis. Repeated reboot, cold boot, audio, Wi-Fi, DroidSpaces userspace operation, SUSFS behavior, and KPM runtime behavior remain unverified.

