# EWISH: Energy-aware User-centric Bitrate Adaptation for HTTP Adaptive Streaming #
We implemented our recent proposed ABR algorithm based on a **E**nergy-aware **W**e**I**ghted **S**um model for **H**AS, namely EWISH, in the [Bitmovin][] player. EWISH takes into account four cost factors of each video representation: (a) *throughput cost*, (b) *buffer cost*, and (c) *quality cost*, and (d) *energy cost*. An overall cost, which is a weighted sum of these penalties, represents each video representation. Our proposed method provides the optimal segment bitrate by choosing the representation with the lowest overall cost for a certain time. A solution determining the weights of the cost factors based on end users’ preferences will be introduced in this work.

[Bitmovin]: https://bitmovin.com/video-player/

## Dependencies ##

In order to shape the traffic it is required to install [wondershaper].

[wondershaper]: https://github.com/magnific0/wondershaper

## Usage ##

* Download this repository on your device.
* Run the experiments.

### Manual experiment ###

To run the experiment manually or test that everything has been set correctly, open the *index_ewish_bitmovin.html* file on your browser.
Three different options can be set through the interface:

1. ABR strategy: 'throughputBased', 'BBA' (Buffer-Based Adaptation), 'SARA' (Segment-Aware Rate Adaptation), 'WISH', and 'EWISH'. This is the ABR technique adopted for requesting the video segments.
2. Mode (only available for WISH and EWISH): 'save_data' (reduce data consumption), 'high_quality' (maximize the video quality), 'save_energy' (reduce the energy consumption - only available for EWISH), and 'balance' (a balanced configuration). This defines the weights configuration to advantage/prioritize specific goals.
3. Quality: 'linear' or 'logarithmic'. This selectes the function used to estimate the quality of a video representation.

If you are satisifed with the settings, click on the *Submit* button to start the streaming session.
When the playback terminates, the JSON file containing the streaming information (formatted as the JSON input file to the [ITU-T P.1203][], mode 0) will be downloaded automatically. Feed this file to the model to obtain the Quality-of-Experience (QoE) estimation.

P.S.: when using codecs different than 'avc', please refer to the [extended model][].

[ITU-T P.1203]: https://github.com/itu-p1203/itu-p1203
[extended model]: https://github.com/Telecommunication-Telemedia-Assessment/itu-p1203-codecextension

### Experiment automation ###

To automate the experiment simply run the *run_bitmovin_player.py* file. The browser will be automatically opened and the experiment will start right-away.
To customize the scenario, simply use the following parameters when running the python script:

```
run_bitmovin_player.py -a [--abr] <abr_strategy> -q [--quality] <quality_mode> -m [--mode] <weights_configuration>
-a [--abr]: "throughputBased", "BBA", "SARA", "wish", "ewish"
-q [--quality]: "linear", "logarithm"
-m [--mode]: "save_data", "high_quality", "save_energy", "balance"
```

Further information can be found using the parameter '-h' when running the script.

## Authors ##
* Daniele Lorenzi - Christian Doppler Laboratory ATHENA, Alpen-Adria-Universitaet Klagenfurt - daniele.lorenzi@aau.at
* Minh Nguyen - Christian Doppler Laboratory ATHENA, Alpen-Adria-Universitaet Klagenfurt - minh.nguyen@aau.at
* Farzad Tashtarian - Christian Doppler Laboratory ATHENA, Alpen-Adria-Universitaet Klagenfurt - farzad.tashtarian@aau.at
* Christian Timmerer - Christian Doppler Laboratory ATHENA, Alpen-Adria-Universitaet Klagenfurt - christian.timmerer@aau.at

## Acknowledgments
If you use this source code in your research, please cite 
1. Include the link to this repository
2. Cite the following publication

*Lorenzi, D., Nguyen, M., Tashtarian, F., Hellwagner, H. and Timmerer, C., "E-WISH: An Energy-aware ABR Algorithm For Green HTTP Adaptive Video Streaming", In 2024 ACM 3rd Mile-High Video (MHV'24), ACM, 2024.*

```
@inproceedings{lorenzi2024ewish,
author = {Lorenzi, Daniele and Nguyen, Minh and Tashtarian, Farzad and Timmerer, Christian},
title = {E-WISH: An Energy-aware ABR Algorithm For Green HTTP Adaptive Video Streaming},
year = {2024},
isbn = {9798400704932},
publisher = {Association for Computing Machinery},
address = {New York, NY, USA},
url = {https://doi.org/10.1145/3638036.3640802},
doi = {10.1145/3638036.3640802},
abstract = {HTTP Adaptive Streaming (HAS) is the de-facto solution for delivering video content over the Internet. The climate crisis has highlighted the environmental impact of information and communication technologies (ICT) solutions and the need for green solutions to reduce ICT's carbon footprint. As video streaming dominates Internet traffic, research in this direction is vital now more than ever. HAS relies on Adaptive BitRate (ABR) algorithms, which dynamically choose suitable video representations to accommodate device characteristics and network conditions. ABR algorithms typically prioritize video quality, ignoring the energy impact of their decisions. Consequently, they often select the video representation with the highest bitrate under good network conditions, thereby increasing energy consumption. This is problematic, especially for energy-limited devices, because it affects the device's battery life and the user experience. To address the aforementioned issues, we propose E-WISH, a novel energy-aware ABR algorithm, which extends the already-existing WISH algorithm to consider energy consumption while selecting the quality for the next video segment. According to the experimental findings, E-WISH shows the ability to improve Quality of Experience (QoE) by up to 52\% according to the ITU-T P.1203 model (mode 0) while simultaneously reducing energy consumption by up to 12\% with respect to state-of-the-art approaches.},
booktitle = {Proceedings of the 3rd Mile-High Video Conference},
pages = {28–33},
numpages = {6},
keywords = {ABR algorithm, Energy, HTTP Adaptive Streaming, MPEG-DASH, QoE},
location = {Denver, CO, USA},
series = {MHV '24}
}
```
