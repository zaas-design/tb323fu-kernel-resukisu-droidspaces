# Kfinal artifacts

The files present here are outputs from ABK run [37649518516](https://github.com/zaas-design/ABK/actions/runs/37649518516), plus metadata for the boot/system_dlkm/vbmeta pair written to the tablet and read back successfully. The repository currently contains only a subset: `ABK-SystemDlkmModules.bundle.zip` and `vbmeta-a-test.img` are present; the other files listed below were validated locally but could not be uploaded. This is not a complete flashable set.

See [`KERNEL-METADATA.json`](KERNEL-METADATA.json) for build provenance and the test status summary.

| File | Use / status |
| --- | --- |
| `Image` | Raw kernel Image from the Kfinal build. |
| `boot-TB323FU-Kfinal.img` | GBL-preserving boot image used in the successful one-boot test. |
| `system_dlkm-a-test.img` | Matching logical `system_dlkm_a` test image, including the newly built Binder module and dm-verity tree. |
| `vbmeta-a-test.img` | Matching test vbmeta for that `system_dlkm` tree. Signed with a temporary key, not a Lenovo key. |
| `ABK-AnyKernel3.bundle.zip` | ABK AnyKernel3 artifact bundle. |
| `ABK-Images.bundle.zip` | ABK image artifact bundle. |
| `ABK-SystemDlkmModules.bundle.zip` | ABK system_dlkm module bundle; this is not itself a complete `system_dlkm.img`. |
| `test-only-vbmeta-key.pub.pem` | Public test key only; the private test key is intentionally not included. |

The test image omits FEC. Keep the bootloader unlocked and do not treat this test pair as a production AVB package. Do not flash only one member of the `boot + system_dlkm + vbmeta` set. No universal flash script is provided.

`SHA256SUMS.txt` identifies files currently present in this repository. `ABK-LICENSE.txt` and `THIRD_PARTY_NOTICES.md` accompany the upstream ABK bundles.
