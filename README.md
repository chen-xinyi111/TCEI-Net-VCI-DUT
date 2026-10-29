# TCEI-Net VCI-DUT processed data

Processed trajectory data supporting **Temporal Conflict Evolution Interaction Network: Pedestrian Trajectory Prediction for Heterogeneous Traffic Scenes**.

The upstream VCI-DUT dataset was released by its original authors at https://github.com/dongfang-steven-yang/vci-dataset-dut . The data in this release were preprocessed by the manuscript authors. This repository contains processed data and documentation. The model source code is planned to be released after manuscript acceptance.

## Download

Download `TCEI-Net-VCI-DUT-processed-v1.0.zip` from the repository's Releases page. Extract the archive to obtain `data/train_data.npz`, `data/val_data.npz`, `data/test_data.npz`, `data/norm_params.pkl`, and `data/processing_stats.pkl`.

## Split protocol

The supplied files are partitioned at the **scene-frame group** level, approximately 70/20/10. Every sample with the same scene identifier and frame identifier belongs to the same split. Pedestrian identities can appear in different splits at different frames. This is not an identity-disjoint or held-out-scene split.

| Split | Pedestrian trajectory windows | Scene-frame groups |
|---|---:|---:|
| Training | 121489 | 3864 |
| Validation | 35033 | 1104 |
| Test | 18864 | 553 |

The stored arrays contain 7 observed time steps and 10 future time steps. `veh_hist` has 10 vehicle slots. The temporal sampling interval used by the study is 0.5 seconds; coordinates are in metres. The archive preserves the input data files byte for byte. No repartitioning, resampling, retraining, or numerical alteration was performed while preparing this release.

## Array fields

- `ped_hist_pos`, `ped_hist_vel`: pedestrian historical position and velocity arrays.
- `ped_future`: future pedestrian positions.
- `veh_hist`, `veh_mask`: vehicle history and validity masks.
- `ped_mask`: stored pedestrian validity mask.
- `scene_ids`, `frame_ids`, `ped_ids`: stored scene, frame, and pedestrian identifiers.
- `reference_points`: stored reference coordinates.

The identifier arrays use NumPy object dtype. Loading those fields requires pickle support; only load files from a trusted source. `norm_params.pkl` and `processing_stats.pkl` are the original supporting files. The array names describe the stored fields and do not constitute a complete independent validation of the original preprocessing pipeline.

## Attribution and reuse

Please cite the original dataset paper, *Top-view Trajectories: A Pedestrian Dataset of Vehicle-Crowd Interaction from Controlled Experiments and Crowded Campus*, https://arxiv.org/abs/1902.00487 , and retain the upstream attribution. See `SOURCE_NOTICE.md` for upstream rights information. No model code or model checkpoints are included.

## Integrity

`manifest.json` and `SHA256SUMS.txt` record sizes and SHA-256 digests of the five original data files. Verify the checksums after extraction.
