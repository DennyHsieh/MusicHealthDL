# Overview of the Music-Health-Dataset
The dataset is the database containing tables of data relating to songs which are annotated by deep learning. The songs are used in physiological measurement. We will transfer the file format from .xlsx to .csv after we complete the content. 

## List of tables
* song_basicinfo: 子項三與子項四的各歌曲清單與歌曲基本資訊
	
| Name                            | Data type | Description                                                                                                           |
|---------------------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------|
| ***song_id***                   | int                | 歌曲ID，由1開始編號，若同首歌不同檔案來源，則ID不同                                                                   |
| ***song_id_kkbox***             | int                | KKBOX歌曲ID                                                                              |
| ***song_name***                 | varchar(50)        | 歌曲名稱，可於歌名後新增副歌名 <br>格式: 歌名+space+(副歌名) <br>Example: Gonna Make You Sweat (Everybody Dance Now)  |
| ***song_artist***               | varchar(50)        | 歌曲創作者，若無人聲則空著，若超過一人則以","隔開。Example: 周杰倫                                                         |
| ***song_original_artist***      | varchar(50)        | 歌曲原唱，若無人聲則空著，若超過一人則以","隔開。Example: 周杰倫                                                         |
| ***song_year***                 | char(4)            | 歌曲發行年份，Example: 2018                                                                                           |
    
* song_path: 歌曲路徑

| Name                            | Data type | Description                                                                                                           |
|---------------------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------|
| ***song_id***                   | int                | 歌曲ID，由1開始編號，若同首歌不同檔案來源，則ID不同                                                                   |
| ***song_lyric***                | varchar(200)       | 歌詞，為一歌詞檔案路徑。格式: song_id + "-" + song_name，其中song_id為7位數。 <br>Example: 0000001-明日天涯.lyrc      |
| ***song_file***                 | varchar(200)       | 歌曲檔案，為一歌曲檔案路徑。格式: song_id + "-" + song_name，其中song_id為7位數。由於歌曲有版權問題，此路徑僅作為研究使用 <br>Example: 0000001-明日天涯.mp3 |
| ***youtube_link***              | varchar(200)       | 歌曲於YouTube下載連結，為一超連結                                                                                     |
| ***youtube_date***              | stamp(0)           | 歌曲於YouTube上傳日期，格式: YYYY-MM-DD <br>Example: 2018-01-01                                                       |
| ***youtube_lastretrieve_date*** | stamp(0)           | 歌曲於YouTube最後擷取日期，格式: YYYY-MM-DD                                                                           |
| ***kkbox_lastretrieve_date***   | stamp(0)           | 歌曲於KKBOX最後擷取日期，格式: YYYY-MM-DD                                                                             |
| ***song_album***                | varchar(200)       | 歌曲專輯，Example: 國語懷舊金曲3                                                                                  |
| ***song_version_company***      | varchar(200)       | 專輯歌曲發行公司，Example: 威森影視事業有限公司                                                                       |

* song_feature: 歌曲特徵

| Name                            | Data type | Description                                                                                                           |
|---------------------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------|
| ***song_id***                   | int                | 歌曲ID，由1開始編號，若同首歌不同檔案來源，則ID不同                                                                   |
| ***song_scenario***            | varchar(50)        | 歌曲應用情境。與子項四討論確定後，將會有額外reference說明                                                             |
| ***song_ifvocal***              | smallint           | 歌曲是否具人聲。若具演唱則為1；純演奏則為0                                                                            |
| ***vocal_gender***              | smallint           | 歌手性別。男生為0；女生為1；合唱為2                                                                                   |
| ***vocal_language***            | varchar(50)        | 歌曲語言。以中文表示，若超過一種則以","隔開。目前語言有"中文"、台語"、"英文"                                           |
| ***song_type***                 | varchar(50)        | 歌曲類型。與子項四討論確定後，將會有額外reference說明。Example: 搖滾                                                   |


- song_annotation_compute: 歌曲音樂特徵加註，使用Python內librosa, madmom之library與MATLAB之MIRtoolbox分析。
  - 為了資料科學之方便使用，原則能從librosa與madmom提取之特徵優先使用，但部分音樂特徵於電腦計算分析有盲點，因此這些特徵將使用過去的工具MIRtoolbox。
  - 以下檔案除song_id外，其他音樂特徵皆為檔名，檔名為: “song_id” + “-” + “annotation_feature” + “.副檔名”

  - LIBROSA

| **Name**        | **Data type** | **Description**              |
| --------------- | ------------- | ---------------------------- |
| ***song_id***   | int           | 歌曲ID，由1開始編號，若同首歌不同檔案來源，則ID不同 |
| ***sr***        | varchar(50)   | 取樣速率                         |
| ***beat_time*** | varchar(50)   | 拍子時間點                        |
| ***duration***  | varchar(50)   | 歌曲長度                         |
| ***mfcc***      | varchar(50)   | 歌曲梅爾頻率倒譜係數                   |
| ***tempo***     | varchar(50)   | 歌曲拍速                         |


  - madmom

| **Name**                         | **Data type** | **Description**              |
| -------------------------------- | ------------- | ---------------------------- |
| ***song_id***                    | int           | 歌曲ID，由1開始編號，若同首歌不同檔案來源，則ID不同 |
| ***key***                        | varchar(50)   | 歌曲音調                         |
| ***segments_time***              | varchar(50)   | 音樂事件(onset)的開始時間點            |
| ***segments_loudness_max***      | varchar(50)   | 歌曲段落音量最大值                    |
| ***segments_loudness_max_time*** | varchar(50)   | 歌曲段落音量最大值之時間                 |
| ***segments_loudness_start***    | varchar(50)   | 歌曲段落音量最大值之開始時間               |
| ***mfcc***                       | varchar(50)   | 歌曲梅爾頻率倒譜係數                   |
| ***tempo***                      | varchar(50)   | 歌曲拍速                         |


  - MIRtoolbox

| **Name**         | **Data type** | **Description**              |
| ---------------- | ------------- | ---------------------------- |
| ***song_id***    | int           | 歌曲ID，由1開始編號，若同首歌不同檔案來源，則ID不同 |
| ***mirmode***    | varchar(50)   | 歌曲調式                         |
| ***mirpitch***   | varchar(50)   | 歌曲音高(multiple)               |
| ***miremotion*** | varchar(50)   | 歌曲情緒                         |


  - Reference: Annotation between **Million song dataset** ([reference](https://labrosa.ee.columbia.edu/millionsong/pages/example-track-description), [paper](http://ismir2011.ismir.net/papers/OS6-1.pdf)) and **LIBROSA**
    - Common metadata for annotation(12) 

| **Million song dataset**       | **LIBROSA**                      |                                              |  |
| ------------------------------ | -------------------------------- | -------------------------------------------- |
| **analysis_sample_rate**       | ***sr***                         | 取樣速率                                         |
| **beats_start**                | ***beat_time***                  | 拍子開始時間點                                      |
| **duration**                   | ***duration***                   | 歌曲長度                                         |
| **key**                        | ***key***                        | 歌曲音調                                         |
| **mode**                       | ***mode***                       | 歌曲調式                                         |
| **segments_start**             | ***segment_time***               | 音樂事件(onset)的開始時間點                       |
| **segments_loudness_max**      | ***segments_loudness_max***      | max loudness during each segment             |
| **segments_loudness_max_time** | ***segments_loudness_max_time*** | time of the max loudness during each segment |
| **segments_loudness_start**    | ***segments_loudness_start***    |                                              |
| **segments_pitches**           | ***pitch***                      | 歌曲音高                                         |
| **segments_timbre**            | ***mfcc***                       | 歌曲梅爾頻率倒譜係數                              |
| **tempo**                      | ***tempo***                      | 歌曲拍速                                         |

    - Common metadata but already appear in other tables(8):
        artist_name(song_name), release(album_version), artist_playmeid, release_7digitalid, track_id(kkbox_id), song_id(song_id), title(song_name), year(song_year)

    - Not useful for annotation(35): 
      artist_7digitalid, artist_familiarity, artist_hotttnesss, artist_id, artist_latitude, artist_location, artist_longitude, artist_mbid, artist_mbtags, artist_mbtags_count, artist_terms, artist_terms_freq, artist_terms_weight, audio_md5, bars_confidence, bars_start, beats_confidence, ****danceability, end_of_fade_in, energy, key_confidence, loudness, mode_confidence, num_songs, sections_confidence, sections_start, segments_confidence, similar_artists, song_hotttnesss**,** start_of_fade_out, ****tatums_confidence, ****tatums_start, time_signature, time_signature_confidence, track_7digitalid


- song_annotation_compute: 歌曲音樂特徵之音樂專家加註，使用Sonic Visualiser加註。
  - 加註細節與Demo寫於[SOP](https://github.com/DennyHsieh/annotation-expert)
  - Reference: [SALAMI annotation guide](http://www.music.mcgill.ca/~jordan/salami/SALAMI-Annotator-Guide.pdf)

| **Name**             | **Data type** | **Description**                  |
| -------------------- | ------------- | -------------------------------- |
| ***song_id***        | int           | 歌曲ID，由1開始編號，若同首歌不同檔案來源，則ID不同     |
| ***special***        | varchar(50)   | 歌曲特別標記，判斷歌曲起始與結束(參考SALAMI)       |
| ***structure***      | varchar(50)   | 歌曲之結構(intro, verse, etc…)        |
| ***melody_phrase***  | varchar(50)   | 歌曲之樂句                            |
| ***cadence***        | varchar(50)   | 歌曲之終止式                           |
| ***lyric_phrase***   | varchar(50)   | 歌詞之歌詞句                           |
| ***structure_plus*** | varchar(50)   | 歌曲之結構，相同結構標註相同大寫英文字母(A, B, C, …) |
| ***serial_number***  | varchar(50)   | 歌曲流水號，判斷第幾人次加註                   |
| ***sv***             | varchar(50)   | Sonic Visualiser工作檔              |



* person_info: 受試者基本背景資訊

| Name              | Data type | Description                                                                  |
|-------------------|--------------------|------------------------------------------------------------------------------|
| ***id***          | int                | 受試者ID，由1開始編號                        |
| ***gender***      | varchar(6)         | 受試者性別，male(M)/female(F)                                                |
| ***age***         | smallint           | 受試者年紀                                                                   |
| ***education***   | varchar(20)        | 受試者最高學歷                                                               |
| ***ethnic***      | varchar(50)        | 受試者族群，格式: 出生地, 民族 <br>Example: 台灣新竹, 原住民、中國福建, 漢人 |
| ***language***    | varchar(20)        | 受試者母語，若超過一個以" , "隔開，Example: 國語、國語, 台語                 |
| ***institution*** | varchar(50)        | 受試機構                                                                     |

* person_musicbg: 受試者音樂背景，受試者音樂背景可超過2項。

| Name             | Data type | Description                                           |
|------------------|--------------------|-------------------------------------------------------|
| ***id***         | int                | 受試者ID，由1開始編號                                  |
| ***instrument*** | varchar(50)        | 受試者熟悉樂器                                        |
| ***years***      | smallint           | 受試者熟悉樂器之學習時間, unit: years                 |

* person_artistprefer: 受試者歌手喜好。

| Name         | Data type | Description                          |
|--------------|--------------------|--------------------------------------|
| ***id***     | int                | 受試者ID，由1開始編號                 |
| ***artist*** | varchar(50)        | 受試者喜歡之歌手                      |

* nursing_record_dynamic: 生理量測動態資訊。

| Name                | Data type | Description                                                                                                                          |
|---------------------|--------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| ***date***          | stamp(0)           | 資料紀錄時間點，格式: YYYYMMDDHHMMSS。Example: 20180101120000                                                                        |
| ***id***            | int                | 受試者ID                                                                                                                             |
| ***song_id***       | int                | 受試者受測歌曲ID                                                                                                                     |
| ***song_start***    | stamp(0)           | 生理資料開始量測時之歌曲時間，格式: MM:SS。Example: 00:20                                                                            |
| ***song_end***      | stamp(0)           | 生理資料結束量測時之歌曲時間，格式: MM:SS。Example: 03:50                                                                            |
| ***heart_rate***    | varchar(200)       | 心率紀錄，為一檔案路徑，格式: heartrate + "-" + id + "-" + song_id + "-" + date <br>Example: heartrate-0001-0000001-20180101120000   |
| ***activity***      | varchar(200)       | 活動紀錄，為一檔案路徑，格式: activity + "-" + id + "-" + song_id + "-" + date <br>Example: activity-0001-0000001-20180101120000     |
| ***sleep_quality*** | varchar(200)       | 受試者睡眠品質，為一檔案路徑，格式: sleepqua "-" + id + "-" + song_id + "-" + date <br>Example: sleepqua-0001-0000001-20180101120000 |

* nursing_record_static: 生理量測靜態資訊。

| Name             | Data type | Description                                                                                                                                          |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| ***date***       | stamp(0)           | 資料紀錄時間點，格式: YYYYMMDDHHMMSS。Example: 20180101120000                                                                                        |
| ***id***         | int                | 受試者ID                                                                                                                                             |
| ***song_id***    | int                | 受試者受測歌曲ID                                                                                                                                     |
| ***song_start*** | stamp(0)           | 生理資料開始量測時之歌曲時間，格式: MM:SS。Example: 00:20                                                                                            |
| ***song_end***   | stamp(0)           | 生理資料結束量測時之歌曲時間，格式: MM:SS。Example: 03:50                                                                                            |
| ***scr***        | varchar(200)       | 膚電值(skin conductance responce)，為一檔案路徑，格式: scr + "-" + id + "-" + song_id + "-" + date <br>Example: scr-0001-0000001-20180101120000      |
| ***hrv***        | varchar(200)       | 心跳變異率(heart rate variability)，為一檔案路徑，格式: hrv + "-" + id + "-" + song_id + "-" + date <br>Example: hrv-0001-0000001-20180101120000     |
| ***fer***        | varchar(200)       | 臉部情緒辨識(face emotion recognition)，為一檔案路徑，格式: fer + "-" + id + "-" + song_id + "-" + date <br>Example: fer-0001-0000001-20180101120000 |
| ***sp***         | varchar(200)       | 站姿壓力(standing pressure)資料，為一檔案路徑，格式: sp + "-" + id + "-" + song_id + "-" + date <br>Example: sp-0001-0000001-20180101120000          |

* questionnaire: 問卷結果與睡眠品質

| Name                | Data type | Description                               |
|---------------------|--------------------|-------------------------------------------|
| ***id***            | int                | 受試者ID，由1開始編號                     |
| ***ques_bsrs5***    | smallint           | 心情溫度計(BSRS-5)量表，score range: 0-15 |
| ***ques_mmse***     | smallint           | 簡易智能狀態測驗(MMSE)，score range: 0-30 |
| ***ques_moca***     | smallint           | 蒙特利爾智能測驗(MoCA)，score range: 0~30 |

* 檔案路徑之命名，有使用song_id則增加為7位數(0000001)，id為4位數(0001)
