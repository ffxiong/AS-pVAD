# AS-pVAD

We create a test set with frame-wise ground truth labels for both pVAD and regular VAD.
The clean speech data is obtained from the test set of TIMIT corpus [1] while the noise data is from Noisex-92 [2];
14 RIRs from the ACE challenge [3] are adopted with the reverberation time ranging from 0.3 to 1.3 s. 

This test set contains 2 test tracks:
S_track: each speech file in this track contains only one same speaker. Segmental SNR varies among [-5, 0, 5, 10, 15, 20, 40]dB. Reverberation is added using the 14 RIRs mentioned above. The total length of this track is about 9 hours.
M_track: each speech file in this track contains two speakers where they take turns to talk in the first half and talk simultaneously in the second half. SNR and reverberation are simulated in the same way as for S_track except that the additional parameter, i.e., SIR of the target speech against the interference speech varies among [-10, -5, 0, 5, 10]dB. The total length of this track is about 10 hours.

For each test audio, we give its corresponding frame-wise pVAD label, VAD label, enrollment audio (15s) and clean audio. 
They are stored separately in folders /noisy/pvad_label/vad_label/enroll/clean.

It should be noted that the sampling rate is 16kHz, the frame-wise label is given with a frame length of 20ms with 50% overlap between successive frames. 

The naming rules are as follows：

#  S_track: 
noisy audio:      spk_xx(rir_names)_RIR_xx(noise_names)_snr?.wav

clean audio:      spk.wav

enrollment audio: spk_enroll.wav

pvad_label:       spk_pvad_label.npy

vad_label:        spk_vad_label.npy

For example, "FADG0_Single_403a_2_RIR_f16_snr40.wav" means: in this test audio, the target speaker's name is "FADG0", RIR type is "Single_403a_2", noise type is "f16", SNR is 40dB.
Its corresponding clean audio is "FADG0.wav", enrollment audio is "FADG0_enroll.wav", pvad_label is "FADG0_pvad_label.npy", vad_label is "FADG0_vad_label.npy".

#  M_track: (spk1 is the target speaker, spk2 is the interfering speaker)
noisy audio:      spk1_mixw_spk2_xx(rir_names)_RIR_xx(noise_names)_snr?_sir?.wav

clean audio:      spk1.wav

enrollment audio: spk1_enroll.wav

pvad_label:       spk1_pvad_label.npy

vad_label:        spk1_vad_label.npy

For example, "FADG0_mixw_MPAB0_Single_502_2_RIR_white_snr5_sir-5.wav" means: in this test audio, the target speaker's name is "FADG0", the interfering speaker's name is "MPAB0", spk1's RIR type is "Single_403a_2", spk2's RIR type is "Single_403a_1"(Same room but different location), noise type is "white", SNR is 5dB, SIR is -5dB. Its corresponding clean audio is "FADG0.wav", enrollment audio is "FADG0_enroll.wav", pvad_label is "FADG0_pvad_label.npy", vad_label is "FADG0_vad_label.npy".

We also provide the frame-wise prediction results (probability) of our model "AS-pVAD" [4] in the form of ".npy", which is the same as label. The results files are stored in /model_result/ 
For each track, in enrollment case, we give the pVAD results in "pVAD_result" folder; in enrollment-less case, we give regular VAD results in "VAD_result" folder.


#  References:

[1] V. Zue, S. Seneff, and J. Glass, “Speech database development: TIMIT and beyond,” in Speech Input/Output Assessment and Speech Databases, 1989, pp. Vol.2, 35–40.

[2] A. Varga and H. J.M. Steeneken, “Assessment for automatic speech recognition: II. NOISEX-92: A database and an experiment to study the effect of additive noise on speech recognition systems,” Speech Communication, vol. 12, no. 3, pp. 247–251, 1993.

[3] J. Eaton, N. D. Gaubitch, A. H. Moore, and P. A. Naylor, “Estimation of room acoustic parameters: The ACE challenge,” IEEE Trans Audio Speech Lang Process, vol. 24, no. 10, pp. 1681–1693, 2016.

[4] F. Liu, F. Xiong, Y. Hao, K. Zhou, C. Zhang, J. Feng, "AS-pVAD: A Frame-wise Personalized Voice Activity Detection Network with Attentive Score Loss" submitted to ICASSP2024
