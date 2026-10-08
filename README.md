# Lenovo TB323FU custom kernel and GBL notes

This repository records one custom kernel result for the Lenovo Legion Y700 Gen 5 (TB323FU). It is an engineering notebook and artifact archive, not a universal installer or a “flash this and everything works” package.

## Device and firmware

- **Device:** Lenovo Legion Y700 Gen 5, model TB323FU
- **Firmware:** ZUXOS 2.0.11.043 (Android 16 base)
- **Bootloader:** must be unlocked. The tested vbmeta uses a temporary test key. **Do not relock the bootloader** with these artifacts.
- **Kernel release:** `6.12.30-android16-5-g0baa65ffa8964-ab10018892-4k`
- **Successful CI build:** [zaas-design/ABK run 37649518516](https://github.com/zaas-design/ABK/actions/runs/37649518516)

The exact raw kernel image SHA-256 is `06321cbfca22c2de883d5e02bd8b43a20cd110974684bcab8c4dc7c4a2b43f3f`. File hashes for all published artifacts are in [kernel/final/SHA256SUMS.txt](kernel/final/SHA256SUMS.txt).

## What is here

- [`kernel/final/`](kernel/final/README.md) contains the Kfinal raw Image, the boot image used in the successful test, the matching test `system_dlkm` and `vbmeta` images, and the ABK output bundles.
- [`gbl_root_canoe/`](gbl_root_canoe/README.md) contains the small TB323FU-specific chainload-only source patch and documents exactly what it changes. It is a delta against upstream, not a repackaged copy of the full upstream repository.
- [`abk-workflow/`](abk-workflow/README.md) contains the ABK dispatch inputs and snapshots of the relevant workflow files from the exact successful ABK commit.

## Kernel configuration summary

The successful build used AOSP `kernel/common` at commit `1750f757fabea014ecc59d327c0c9d3c15ab1e6d`, GKI `gki_defconfig`, Android 16 / Linux 6.12.30, and the 2025-06 toolchain patch level.

Enabled for this build:

- ReSukiSU, Stable branch
- DroidSpaces kernel integration, pinned to commit `2ac9f5af650ae20149d9d46606526d5b003ca626`
- SUSFS
- ReSukiSU KPM
- DroidSpaces virtualization support
- `USER_NS=y`
- trust for the stock TB323FU GKI module certificate

ABK options such as ZRAM enhancements, extra ZRAM algorithms, BBG, DDK, NTsync, networking enhancements, and Re-Kernel were disabled. The complete recorded dispatch values are in [`abk-workflow/dispatch-inputs.json`](abk-workflow/dispatch-inputs.json).

## Test result and limits

The tablet booted once with the matched `boot_a + system_dlkm_a + vbmeta_a` set through fastbootd. The active slot remained A. Post-write readbacks matched all three candidate files byte-for-byte. Root was available, `rust_binder` was loaded, and the Gunyah/DroidSpaces kernel modules were present.

The test `vbmeta` was signed with a temporary non-Lenovo key, and the `system_dlkm` image has no FEC data. The bootloader was unlocked; the observed boot state was orange with verity mode `eio`. These artifacts do not demonstrate acceptance by a locked Lenovo bootloader or a production-secure AVB setup. Keep the bootloader unlocked and treat the pair as experimental.

Note: Upstream DroidSpaces documentation does not list SUSFS as a supported combination. 

## Reproduction references

The exact ABK source revision, kernel source revision, DroidSpaces revision, workflow inputs, and CI link are captured in [`abk-workflow/`](abk-workflow/README.md). Build workflow snapshots are included for reference only: they depend on scripts, actions, configuration, and patch files elsewhere in the ABK checkout. Use the pinned ABK commit; these files are not standalone workflows in this archive.

## Upstream projects

- [gbl_root_canoe](https://github.com/SuperTurtleDev/gbl_root_canoe)
- [ABK upstream](https://github.com/xingguangcuican6666/ABK)
- [ABK fork used for the successful build](https://github.com/zaas-design/ABK)
- [DroidSpaces OSS](https://github.com/ravindu644/droidspaces-oss)
- [ReSukiSU](https://github.com/ReSukiSU)

The ABK bundle includes its license and third-party notices. Kernel and component licensing remains governed by the respective upstream projects.

