﻿# Overview of the MusicHealthDL
The MusicDatabase.xlsx is the database containing tables of data relating to songs which are annotated by deep learning. The songs are used in physiological measurement. We will transfer the file format from .xlsx to .csv after we complete the content. 

## List of tables
* song_basicinfo: 子項三與子項四的各歌曲清單與歌曲基本資訊
	
| Name                            | Postgres data type | Description                                                                                                           |
|---------------------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------|
| ***song_id***                   | int                | 歌曲ID，由1開始編號，若同首歌不同檔案來源，則ID不同                                                                   |
| ***song_id_kkbox***             |                    | KKBOX歌曲ID，(等6月初洽談後確定資料型式)                                                                              |
| ***song_name***                 | varchar(50)        | 歌曲名稱，可於歌名後新增副歌名 <br>格式: 歌名+space+(副歌名) <br>Example: Gonna Make You Sweat (Everybody Dance Now)  |
| ***song_artist***               | varchar(50)        | 歌曲創作者，若超過一人則以","隔開。Example: 周杰倫                                                                    |
| ***song_year***                 | char(4)            | 歌曲年代，Example: 2018                                                                                               |
    
* song_path: 歌曲路徑

| Name                            | Postgres data type | Description                                                                                                           |
|---------------------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------|
| ***song_id***                   | int                | 歌曲ID，由1開始編號，若同首歌不同檔案來源，則ID不同                                                                   |
| ***song_lyric***                | varchar(200)       | 歌詞，為一歌詞檔案路徑。格式: song_id + "-" + song_name，其中song_id為7位數。 <br>Example: 0000001-明日天涯.lyrc      |
| ***song_file***                 | varchar(200)       | 歌曲檔案，為一歌曲檔案路徑。格式: song_id + "-" + song_name。由於歌曲有版權問題，此路徑僅作為研究使用 <br>Example: 0000001-明日天涯.mp3 |
| ***youtube_link***              | varchar(200)       | 歌曲於YouTube下載連結，為一超連結                                                                                     |
| ***kkbox_link***                | varchar(200)       | 歌曲於KKBOX下載連結，為一超連結                                                                                       |
| ***youtube_date***              | stamp(0)           | 歌曲於YouTube連結日期，格式: YYYY-MM-DD <br>Example: 2018-01-01                                                       |
| ***youtube_lastretrieve_date*** | stamp(0)           | 歌曲於YouTube最後擷取日期，格式: YYYY-MM-DD                                                                           |
| ***kkbox_lastretrieve_date***   | stamp(0)           | 歌曲於KKBOX最後擷取日期，格式: YYYY-MM-DD                                                                             |
| ***song_version***              | varchar(200)       | 專輯歌曲版本，Example: 國語懷舊金曲3                                                                                  |
| ***song_version_company***      | varchar(200)       | 專輯歌曲發行公司，Example: 威森影視事業有限公司                                                                       |

* song_feature: 歌曲特徵

| Name                            | Postgres data type | Description                                                                                                           |
|---------------------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------|
| ***song_id***                   | int                | 歌曲ID，由1開始編號，若同首歌不同檔案來源，則ID不同                                                                   |
| ***song_scenario***            | varchar(50)        | 歌曲應用情境。與子項四討論確定後，將會有額外reference說明                                                             |
| ***song_ifvocal***              | smallint           | 歌曲是否具人聲。若具演唱則為1；純演奏則為0                                                                            |
| ***vocal_gender***              | smallint           | 歌手性別。男生為0；女生為1；合唱為2                                                                                   |
| ***vocal_language***            | varchar(50)        | 歌曲語言。以中文表示，若超過一種則以","隔開                                                                           |
| ***song_type***                 | varchar(50)        | 歌曲類型。與子項四討論確定後，將會有額外reference說明。Example: 搖滾                                                   |

* song_annotation: 歌曲加註內容，此表格等子項一加註方法確定後將補完

| Name                            | Postgres data type | Description                                                                                                           |
|---------------------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------|
| ***song_id***                   | int                | 歌曲ID，由1開始編號，若同首歌不同檔案來源，則ID不同                                                                   |
| ***待補***                   |     ...          | ... |

* person_info: 受試者基本背景資訊

| Name              | Postgres data type | Description                                                                  |
|-------------------|--------------------|------------------------------------------------------------------------------|
| ***id***          | int                | 受試者ID，由1開始編號                        |
| ***gender***      | varchar(6)         | 受試者性別，male(M)/female(F)                                                |
| ***age***         | smallint           | 受試者年紀                                                                   |
| ***education***   | varchar(20)        | 受試者最高學歷                                                               |
| ***ethnic***      | varchar(50)        | 受試者族群，格式: 出生地, 民族 <br>Example: 台灣新竹, 原住民、中國福建, 漢人 |
| ***language***    | varchar(20)        | 受試者母語，若超過一個以" , "隔開，Example: 國語、國語, 台語                 |
| ***institution*** | varchar(50)        | 受試機構                                                                     |

* person_musicbg: 受試者音樂背景，受試者音樂背景可超過2項。

| Name             | Postgres data type | Description                                           |
|------------------|--------------------|-------------------------------------------------------|
| ***id***         | int                | 受試者ID，由1開始編號                                  |
| ***instrument*** | varchar(50)        | 受試者熟悉樂器                                        |
| ***years***      | smallint           | 受試者熟悉樂器之學習時間, unit: years                 |

* person_artistprefer: 受試者歌手喜好。

| Name         | Postgres data type | Description                          |
|--------------|--------------------|--------------------------------------|
| ***id***     | int                | 受試者ID，由1開始編號                 |
| ***artist*** | varchar(50)        | 受試者喜歡之歌手                      |

* health_info_static: dynamic, static資料，此項與子項三討論確定後，將會有額外reference說明
* nursing_record: 此項與子項三討論確定後，將會有額外reference說明
* questionnaire: 問卷結果與睡眠品質

| Name                | Postgres data type | Description                               |
|---------------------|--------------------|-------------------------------------------|
| ***id***            | int                | 受試者ID，由1開始編號                     |
| ***ques_bsrs5***    | smallint           | 心情溫度計(BSRS-5)量表，score range: 0-15 |
| ***ques_mmse***     | smallint           | 簡易智能狀態測驗(MMSE)，score range: 0-30 |
| ***ques_moca***     | smallint           | 蒙特利爾智能測驗(MoCA)，score range: 0~30 |
| ***sleep_quality*** | smallint           | 受試者睡眠品質 (量化標準請子項四提供意見)  |
