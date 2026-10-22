[![DOI](https://img.shields.io/badge/DOI-10.82901%2Fnemar.on005398-blue)](https://doi.org/10.82901/nemar.on005398)

This dataset was utilized for the publication of the manuscript by Zhang et al. [1]. A subset of the data has been employed in [2], [3], [4], and [5].

Summary:
This data set comprises the de-identified subjects with interictal iEEG recordings with sleep from University of California Los Angels Mattel Children’s Hospital, and Children’s Hospital of Michigan, Detroit. 
Subject-wise information is contained in each folder, including iEEGs collected from 185 subjects during sleep. The channel name and valuables, such as the anatomical label and the resection status, are attached to each folder. The outcome and background information of all the subjects are summarized in ‘paticipant.tsv’ located in the parental directory.

Derivatives
The processed data for HFO detection and classification are shown in the derivatives/folder. The HFO analysis contains detection from two methods: RMS and MNI detectors. The bipolar iEEG data used for [5] is also uploaded, and the credit for creating such dataset is given to the authors of the manuscript. 

References: 

[1] Zhang Y, Daida A, Liu L, Kuroda N, Ding Y, Oana S, Kanai S, Monsoor T, Duan C, Hussain SA, Qiao JX, Salamon N, Fallah A, Sim MS, Sankar R, Staba RJ, Engel J Jr, Asano E, Roychowdhury V, Nariai H. Self-supervised data-driven approach defines pathological high-frequency oscillations in epilepsy. Epilepsia. 2025 Nov;66(11):4434-4450. doi: 10.1111/epi.18545.

[2] Monsoor T, Kanai S, Daida A, Kuroda N, Sinha P, Oana S, Zhang Y, Liu L, Singh G, Duan C, Sim MS, Fallah A, Speier W, Asano E, Roychowdhury V, Nariai H. Mini-Seizures: Novel Interictal iEEG Biomarker Capturing Synchronization Network Dynamics at the Epileptogenic Zone. medRxiv. 2025 Feb 2:2025.01.31.25321482. doi: 10.1101/2025.01.31.25321482.

[3] Zhang Y, Lu Q, Monsoor T, Hussain SA, Qiao JX, Salamon N, Fallah A, Sim MS, Asano E, Sankar R, Staba RJ, Engel J Jr, Speier W, Roychowdhury V, Nariai H. Refining epileptogenic high-frequency oscillations using deep learning: a reverse engineering approach. Brain Commun. 2021 Nov 3;4(1):fcab267. doi: 10.1093/braincomms/fcab267. 

[4] Kuroda N, Sonoda M, Miyakoshi M, Nariai H, Jeong JW, Motoi H, Luat AF, Sood S, Asano E. Objective interictal electrophysiology biomarkers optimize prediction of epilepsy surgery outcome. Brain Commun. 2021 Mar 14;3(2):fcab042. doi: 10.1093/braincomms/fcab042.

[5]  Blanca Romero Milà, Nathan Phi Hoang, Marco Pinto-Orellana, Atsuro Daida, Sotaro Kanai, Naoto Kuroda, Shaun A. Hussain, Daniel W. Shrey, Eishi Asano, Hiroki Nariai, Beth A. Lopour. Discovering Novel intracranial EEG Biomarkers of Seizure Generating Tissue through Time-Frequency Analysis. medRxiv. doi: https://doi.org/10.64898/2026.06.12.26355482. Posted June 22, 2026.

## Sampling frequency of sub-UCLA42 (19 Oct 2026)

For sub-UCLA42, `sub-UCLA42_ses-01_task-sleep_ieeg.json` said SamplingFrequency 200 Hz and RecordingDuration 3899.995 s, and its channels.tsv said sampling_frequency 200 Hz and high_cutoff 100 Hz. The EDF file says 2000 Hz: 5809 data records of 1 s with 2000 samples per channel (32 channels), and the file size matches that layout exactly. Readers take the rate from the EDF header, so the data were always read at 2000 Hz; only the sidecars were wrong. Since 19 Oct 2026 the sidecars say SamplingFrequency 2000 Hz, RecordingDuration 5808.9995 s (= (number of samples - 1) / 2000, as for the other UCLA subjects), sampling_frequency 2000 Hz and high_cutoff 600 Hz. 600 Hz is the documented acquisition low-pass: Zhang et al., Brain Commun 2022 (doi:10.1093/braincomms/fcab267, Methods) state that the UCLA recordings were acquired at 2000 Hz with the Nihon Kohden default high frequency filter of 600 Hz. (A version of 19 Oct set 1000 Hz, half the sampling rate; Nyquist does not establish the applied filter, so it was corrected on 20 Oct. The other 49 UCLA subjects still carry 1000 Hz from the original deposit and were not changed.). The EDF file is unchanged.

The EDF rate is the true one. Evidence:
- participants.tsv lists sampling_frequency 2000 for sub-UCLA42.
- Read at 2000 Hz, the recording shows the 60 Hz mains line (16.5 dB above the neighbouring frequencies) with its odd harmonics at 180, 300 and 420 Hz. Seven other UCLA subjects, read the same way at their 2000 Hz rate, show the same pattern. At 200 Hz the line would sit at 6 Hz, and at 1000 Hz at 30 Hz.
- The sleep-spindle (sigma) peak is at 13.4 Hz, as in the seven other UCLA subjects (13 to 17 Hz).
- `derivatives/hfo_detection/sub-UCLA42/` lists 17,313 high-frequency oscillations detected from 1.0 s to 5759.9 s. That fits a 5809 s recording, but not the 3900 s of the former sidecar. Detecting such oscillations needs a sampling rate of 1000 Hz or more.
- The group's description of the UCLA recordings (Zhang et al., Brain Commun 2022, doi:10.1093/braincomms/fcab267) gives a 2000 Hz sampling frequency.
