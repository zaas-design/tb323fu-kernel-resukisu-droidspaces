# TB323FU chainload-only delta for gbl_root_canoe

This folder is a device-specific source delta for [SuperTurtleDev/gbl_root_canoe](https://github.com/SuperTurtleDev/gbl_root_canoe), not a full fork or a replacement for the upstream project.

## Pinned upstream base

The patch applies to upstream commit `8cc6fa5ad467af6d34a00f401290035ee87a14c7` (the patch's original blob IDs for `submodules/patcher/Makefile` and `core.c` match this revision).

## What changed

- Added a `build_chainload` Makefile target that defines `CHAINLOAD_ONLY`.
- In that build mode, `PatchBuffer` applies only the GBL recursion guard: the UTF-16 string `efisp` becomes `nulls`.
- This mode intentionally skips fake-lock, boot-state, KeyMaster, and OPlus-specific patches.
- The resulting TB323FU ZUXOS .043 ABL derivative changed five bytes. Its recorded SHA-256 is `b9f1572962aca864255b3e1a95c0aba143f08f750372df312cb56e38f6da6b6d`.

The delta is in [`patches/tb323fu-043-chainload-only.patch`](patches/tb323fu-043-chainload-only.patch). The derived EFI and vendor BDS binaries are not included; use firmware files legally obtained for your own device. This keeps the public repository focused on source changes instead of redistributing OEM firmware blobs.

The upstream license text for the source delta is preserved in [`LICENSE-UPSTREAM.txt`](LICENSE-UPSTREAM.txt).

The chainload-only path was exercised on a TB323FU running ZUXOS .043. It is separate from the Kfinal kernel build settings. Read the upstream project documentation and the device-specific notes before adapting it; do not assume compatibility with other ABL or firmware versions.

## Reboot to EDL

The tested Canoe boot-root setup also exposed **Android Tools → Reboot to EDL** in the BDS menu. It launches the platform-specific `RebootTools-EDL.efi` utility (SHA-256: `59b6b9bdf3ddd097bb21eb68e59fdd7fbfd35e9efeb13f884d202deea5452faa`) to request an EDL reset; it is not a generic reboot fallback. The utility was verified in a standalone device test, while selecting this menu entry was not separately re-tested in that session.

The EDL utility binary and OEM-derived BDS payload are not included in this source-delta archive. The hash is provided to identify the previously tested utility. EDL only changes the tablet's boot mode; it does not itself read or flash partitions. On this model, confirm the device enumerates as Qualcomm `9008` before using QDL.
