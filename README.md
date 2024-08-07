# IDForge: Identity-Driven Multimedia Forgery Detection via Reference Assistance

<a href='https://arxiv.org/abs/2401.11764'><img src='https://img.shields.io/badge/Paper-Arxiv-red'></a> <a href='https://request.idforge.cfd/ '><img src='https://img.shields.io/badge/Request-IDForge-blue '></a>

## Dataset Overview

Recent advancements in "deepfake" techniques have paved the way for generating various media forgeries.
In response to the potential hazards of these media forgeries, many researchers engage in exploring detection methods, increasing the demand for high-quality media forgery datasets. Despite this, existing datasets have certain limitations. Firstly, most datasets focus on manipulating visual modality and usually lack diversity, as only a few forgery approaches are considered. Secondly, the quality of media is often inadequate in clarity and naturalness. Meanwhile, the size of the dataset is also limited. Thirdly, it is commonly observed that real-world forgeries are motivated by identity, yet the identity information of the individuals portrayed in these forgeries within existing datasets remains under-explored. For detection, identity information could be an essential clue to boost performance. Moreover, official media concerning relevant identities on the Internet can serve as prior knowledge, aiding both the audience and forgery detectors in determining the true identity. Therefore, we propose an identity-driven multimedia forgery dataset, **IDForge**, which contains 249,138 video shots sourced from 324 wild videos of 54 celebrities collected from the Internet. The fake video shots involve 9 types of manipulation across visual, audio, and textual modalities. Additionally, IDForge provides extra 214,438 real video shots as a reference set for the 54 celebrities. Correspondingly, we propose the Reference-assisted Multimodal Forgery Detection Network (R-MFDN), aiming at the detection of deepfake videos. Through extensive experiments on the proposed dataset, we demonstrate the effectiveness of R-MFDN on the multimedia detection task.

![image](https://github.com/xyyandxyy/IDForge/blob/main/assets/sample_2.gif)

## 🫱 Access IDForge

You can request our dataset in this link:  👉 https://request.idforge.cfd/ 👈

> Request will be processed in 1-3 days. 
> 
> If you encounter any issues or do not receive a response within the expected timeframe, please contact idforge_access@outlook.com 🙋‍♂️.

## Types of forgery

The following table categorizes different types of forgery based on various manipulation techniques, with $1$ indicating the presence of a technique and $0$ indicating its absence.

| Forgery Type in Provided Data   | Fake | Lip synchronization | Stand-in Use | Face-swapping | Voice cloning (TorToiSe) | Voice conversion (RVC) | Audio shuffling | LLM generation | Text shuffling |
| ------------------------------- | ---- | ------------------- | ------------ | ------------- | ------------------------ | ---------------------- | --------------- | -------------- | -------------- |
| face_audiomismatch_textmismatch | 1    | 1                   | 1            | 1             | 0                        | 0                      | 1               | 0              | 1              |
| face_rvc_textmismatch           | 1    | 1                   | 1            | 1             | 0                        | 1                      | 0               | 0              | 1              |
| face_tts                        | 1    | 1                   | 1            | 1             | 1                        | 0                      | 0               | 0              | 0              |
| face_tts_textgen                | 1    | 1                   | 1            | 1             | 1                        | 0                      | 0               | 1              | 0              |
| lip_audiomismatch_textmismatch  | 1    | 1                   | 0            | 0             | 0                        | 0                      | 1               | 0              | 1              |
| lip_rvc_textmismatch            | 1    | 1                   | 0            | 0             | 0                        | 1                      | 0               | 0              | 1              |
| lip_tts_textgen                 | 1    | 1                   | 0            | 0             | 1                        | 0                      | 0               | 1              | 0              |
| pristine                        | 0    | 0                   | 0            | 0             | 0                        | 0                      | 0               | 0              | 0              |
| rvc_textmismatch                | 1    | 0                   | 0            | 0             | 0                        | 1                      | 0               | 0              | 1              |

- **Lip synchronization** (*lip*): This method aligns lip movements in a video to correspond with a new audio track. We employ Wav2Lip for precise lip synchronization.

- **Face-swapping** (*face*): This technique replaces an individual's face in a video with another person's. We implement face-swapping using advanced methods like InsightFace, SimSwap, and InfoSwap. 

- **Stand-in Use**: If the stand-in value is 1, it indicates that the body in the video is not the body of the source face's owner. If the stand-in value is 0, it indicates that the body in the video corresponds to the source face's owner.

  > This is consistent with the `Face-swapping`. As described in our paper, we selected stand-ins with body types similar to the source face's owner.

- **Voice cloning** (*tts*): Voice cloning generates new audio sequences from text, closely mimicking a person's unique voice. In this process, we utilize TorToiSe for effective voice cloning.

- **Voice conversion** (*rvc*): This technique alters the voice of one individual to resemble another's while keeping the original speech content intact. We achieve this through RVC.

- **Audio shuffling** (*audioshuffle*): In audio shuffling, we exchange the audio tracks between individuals of the same gender. This technique creates an effect similar to dubbed video content found online.

- **LLM generation** (*textgen*): This approach generates new text stylistically consistent with the original but conveys opposite or altered content. We leverage GPT-3.5 for this sophisticated text generation.

- **Text shuffling** (*textshuffle*): Text shuffling entails exchanging one individual's transcript with another, producing fabricated yet human-originated texts.

## Dataset Structure

We provide two versions of the IDForge dataset. 

* IDForge v1 is the original files, consisting of the mp4 files for each video.

* IDForge v2  is the dataset used in our paper, where each video retains 16 frames (sampled in 4 groups with equal intervals, 4 frames per group), audio files, and extracted text. 

  >  The IDForge v2 builds on the IDForge v1 by adding compression and super-resolution operations to simulate real-world conditions.

### IDForge v1

There are two parts in IDForge v1:

* `main`: main part of the dataset, containing 11 types of data. 

  All data are in `.mp4` format. Each type of data are in a independent zip file, you can only download and extra the data you need.

  ```
  .
  |-- face_audiomismatch_textmismatch.zip
  |-- face_rvc_textmismatch.zip
  |-- face_tts.zip
  |-- face_tts_textgen.zip
  |-- lip_audiomismatch_textmismatch.zip
  |-- lip_rvc_textmismatch.zip
  |-- lip_tts_textgen.zip
  |-- pristine.zip
  |-- rvc_textmismatch.zip
  |-- tts_textgen.zip
  `-- tts_textmismatch.zip
  ```

* `ref`: reference set, in which all video are pristine. 

  ```
  .
  |-- unprocessed_ref.z01
  |-- unprocessed_ref.z02
  |-- unprocessed_ref.z03
  |-- unprocessed_ref.z04
  |-- unprocessed_ref.z05
  |-- unprocessed_ref.z06
  |-- unprocessed_ref.z07
  |-- unprocessed_ref.z08
  `-- unprocessed_ref.zip
  ```

  You need the run the following code to extract data from **Split Zip Files**.

  ```
  (if needed) apt-get update && apt-get install p7zip-full
  
  7z x unprocessed_ref.zip
  ```

Main Folder Structure (reference set is similar): 

```
./main
|-- face_audiomismatch_textmismatch
|-- face_rvc_textmismatch
|-- face_tts
|-- face_tts_textgen
|-- lip_audiomismatch_textmismatch
|-- lip_rvc_textmismatch
|-- lip_tts_textgen
|-- pristine
|-- rvc_textmismatch
|-- tts_textgen
`-- tts_textmismatch ##### Forgery Type
    |-- id01
    |-- id02
    |-- ...
    `-- id53 ##### Person
        |-- id53_00
        |-- id53_04
        |-- id53_05
        `-- id53_08 ##### Different Source Video
            |-- id53_scene_0083_0_simswap.mp4
            |-- id53_scene_0090_0_infoswap.mp4
            |-- id53_scene_0090_0_roop.mp4
            |-- id53_scene_0090_1_simswap.mp4
            `-- id53_scene_0092_0_roop.mp4 ##### Video File
```

### IDForge v2

There are 4 parts in IDForge v2:

* ref
* train
* val
* test

Each part is compressed into a series of split zip files.

You need the run the following code to extract data from **Split Zip Files**:

```
(if needed) apt-get update && apt-get install p7zip-full

7z x FILENAME.zip
```

Train Folder Structure (others are similar): 

```
.
|-- face_audiomismatch_textmismatch
|-- face_rvc_textmismatch
|-- face_tts
|-- face_tts_textgen
|-- lip_audiomismatch_textmismatch
|-- lip_rvc_textmismatch
|-- lip_tts_textgen
|-- pristine
|-- rvc_textmismatch
|-- tts_textgen
`-- tts_textmismatch ##### Forgery Type
    |-- id01
    |-- id02
    |-- ...
    `-- id53 ##### Person
        |-- id53_00
        |-- id53_04
        |-- id53_05
        `-- id53_08 ##### Different Source Video
            |-- id53_scene_0083_0_simswap.mp4
            |-- id53_scene_0090_0_infoswap.mp4
            |-- id53_scene_0090_0_roop.mp4
            |-- id53_scene_0090_1_simswap.mp4
            `-- id53_scene_0092_0_roop.mp4 ##### Video File
                |-- frames_ndarray.npy ##### Extracted Frame (ndarray format)
                |-- id53_scene_0092_0_roop.mp3  ##### Extracted Audio by FFmpeg
                `-- id53_scene_0092_0_roop.txt ##### Extracted Transcript by Whisper
```



## TODO

- [x] Open access requests for IDForge.
- [x] Provide mp4 version.
- [x] Provide samples.
- [ ] Provide more samples.



