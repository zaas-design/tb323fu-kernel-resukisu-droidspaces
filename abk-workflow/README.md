# Reproducing the ABK build

The successful kernel was built by the public `zaas-design/ABK` fork using its custom-source `kernel-source.yml` workflow. This folder records the exact inputs and includes snapshots of the two relevant workflow files at the successful commit.

- Successful run: https://github.com/zaas-design/ABK/actions/runs/37649518516
- ABK commit: `41a2109ce466dbd63977fc6fe5641a089fb16660`
- Build branch: `codex/tb323fu-kfinal-droidspaces-susfs-20261007`
- Entry workflow: [`.github/workflows/kernel-source.yml`](https://github.com/zaas-design/ABK/blob/41a2109ce466dbd63977fc6fe5641a089fb16660/.github/workflows/kernel-source.yml)
- Reusable build workflow: [`.github/workflows/build.yml`](https://github.com/zaas-design/ABK/blob/41a2109ce466dbd63977fc6fe5641a089fb16660/.github/workflows/build.yml)
- Original ABK project: https://github.com/xingguangcuican6666/ABK

The workflow snapshots and `config` file are archival references. They are not a complete ABK checkout and will not build by themselves: the workflows use other ABK scripts, actions, patches, and source files. To reproduce the build, use the full ABK fork at the pinned commit and provide the values in [`dispatch-inputs.json`](dispatch-inputs.json).

The build used public AOSP kernel sources; no GitHub source token or KPM password was configured.

