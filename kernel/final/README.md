# Kfinal artifacts

The ABK bundles are available in the [successful workflow artifact `ReSukiSU_kernel-android16-6.12-30`](https://github.com/zaas-design/ABK/actions/runs/37649518516/artifacts/11497722783). The workflow and configuration are pinned to [ABK commit `41a2109`](https://github.com/zaas-design/ABK/tree/41a2109ce466dbd63977fc6fe5641a089fb16660). I compared SHA-256 for all three downloaded bundles against the local copies; all match. The artifact is subject to the fork’s Actions artifact retention policy.

See [`KERNEL-METADATA.json`](KERNEL-METADATA.json) for build provenance and the test status summary.

| File | Use / status |
| --- | --- |
| `Image` | Raw kernel Image inside the ABK `Images` bundle and also inside the AnyKernel3 bundle linked above. |
| `boot-TB323FU-Kfinal.img` | GBL-preserving boot image used in the successful one-boot test. This device-specific image was not produced by the ABK workflow and is not in its artifact. |
| `system_dlkm-a-test.img` | Matching logical `system_dlkm_a` test image, including the newly built Binder module and dm-verity tree. This was assembled for the device test; only the source module bundle is in the ABK artifact. |
| `vbmeta-a-test.img` | Matching test vbmeta for that `system_dlkm` tree. Signed with a temporary key, not a Lenovo key; this test image is not an ABK workflow output. |
| `ABK-AnyKernel3.bundle.zip` | ABK AnyKernel3 artifact bundle; available in the linked workflow artifact. |
| `ABK-Images.bundle.zip` | ABK image artifact bundle; contains `Image`, `Image.lz4`, and `Image.gz`; available in the linked workflow artifact. |
| `ABK-SystemDlkmModules.bundle.zip` | ABK system_dlkm module bundle; contains `rust_binder.ko` and build metadata and is not itself a complete `system_dlkm.img`. Available in the linked workflow artifact. |
| `test-only-vbmeta-key.pub.pem` | Public test key only; the private test key is intentionally not included. |

The test image omits FEC. Keep the bootloader unlocked and do not treat this test pair as a production AVB package. Do not flash only one member of the `boot + system_dlkm + vbmeta` set. No universal flash script is provided.

`SHA256SUMS.txt` identifies files currently present in this repository. I separately verified that all three linked ABK bundles match their locally verified copies byte-for-byte. `ABK-LICENSE.txt` and `THIRD_PARTY_NOTICES.md` accompany the upstream ABK bundles.
