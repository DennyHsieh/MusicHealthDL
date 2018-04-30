# Overview of the MusicHealthDL Data
The MusicHealthDL is the database containing tables of data relating to songs which are annotated by deep learning. The songs are used in physiological measurement.  

## List of tables
* song_info: 子項三與子項四的各歌曲清單
	
| Name                       | Postgres data type | Description                                                                                                   |
|----------------------------|--------------------|---------------------------------------------------------------------------------------------------------------|
| ***song_id***              | int                | 歌曲ID，由1開始編號，若同首歌不同檔案來源，則ID不同                                                           |
| ***song_name***            | varchar(50)        | 歌曲名稱，可於歌名後新增副歌名 <br>格式: 歌名+space+(副歌名) <br>Example: Gonna Make You Sweat (Everybody Dance Now)  |
| ***song_lyric***           | varchar(200)       | 歌詞，為一歌詞檔案路徑                                                                                        |
| ***song_link***            | varchar(200)       | 歌曲下載連結，為一超連結                                                                                      |
| ***song_file***            | varchar(200)       | 歌曲檔案，為一歌曲檔案路徑                                                                                    |
| ***song_class***           | varchar(50)        | 歌曲分類，Example: 歌曲, 演奏, 鋼琴, ...                                                                      |
| ***song_artist***          | varchar(50)        | 歌曲創作者，Example: 周杰倫                                                                                   |
| ***song_year***            | char(4)            | 歌曲年代，Example: 2018                                                                                       |
| ***link_date***            | stamp(0)           | 歌曲連結日期，格式: YYYY-MM-DD <br>Example: 2018-01-01                                                            |
| ***song_version***         | varchar(200)       | 專輯歌曲版本，Example: 國語懷舊金曲3                                                                          |
| ***song_version_company*** | varchar(200)       | 專輯歌曲發行公司，Example: 威森影視事業有限公司                                                               |
| ***song_type***            | varchar(50)        | 歌曲類型，Example: 搖滾                                                                                       |

    
* person_info
* person_musicbg
* rank
* health_info
