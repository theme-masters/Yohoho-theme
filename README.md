# Тема «Yohoho-theme»

![Тема «Yohoho-theme» nodejs](https://raw.githubusercontent.com/theme-masters/Yohoho-theme/master/screenshot.png)

:art: Тема «Yohoho-theme»

## Как установить?
1. Скачать архив с [GitHub](https://github.com/theme-masters/Yohoho-theme/archive/refs/heads/main.zip)
2. Распаковать архив на сервер в папку **themes**
3. Изменить название темы в админ-панели

![агрегатор плееров Yohoho-theme](https://raw.githubusercontent.com/theme-masters/Yohoho-theme/master/6.png)

## как добавить фильмы со всех балансеров (инфо скопировано [от сюда](https://enota.club/threads/kak-otvjazat-nastroit-parsing-i-video-pleer-ot-kp.3040/#post-24118))?

1. Очищаете базу сайта (будут удалены все фильмы):

![Очищаете базу сайта (будут удалены все фильмы)](https://raw.githubusercontent.com/theme-masters/Yohoho-theme/master/1.png)

2. Делаете основным ID КиноПоиска:

![Делаете основным ID КиноПоиска](https://raw.githubusercontent.com/theme-masters/Yohoho-theme/master/2.png)

3. Заполняете строки автозаполнения с того источника, который Вам нужен:

![Заполняете строки автозаполнения с того источника, который Вам нужен](https://raw.githubusercontent.com/theme-masters/Yohoho-theme/master/3.png)

```
    # Заполнение с API Kodik
    0 ~ http://kodikapi.com/list?limit=100&with_material_data=true&token=45c53578f11ecfb74e31267b634cc6a8&page=[page][next_page] ~ results ~ ~ kinopoisk_id <> kp_id ~ material_data.title <> title_ru ~ material_data.title_en <> title_en ~ material_data.year <> year ~ material_data.description <> description ~ material_data.poster_url <> poster ~ material_data.screenshots <> pictures ~ material_data.countries <> country ~ material_data.genres <> genre ~ material_data.premiere_world <> premiere ~ material_data.actors <> actor ~ material_data.directors <> director ~ type <> type


    # Заполнение с API Collaps
    0 ~ https://apicollaps.cc/list?token=eedefb541aeba871dcfc756e6b31c02e&limit=99&page=[page] ~ results.0.id ~ https://apicollaps.cc/franchise/details?token=eedefb541aeba871dcfc756e6b31c02e&id=[id] ~ kinopoisk_id <> kp_id ~ imdb_id <> custom.imdb_id ~ name <> title_ru ~ name_eng <> title_en ~ year <> year ~ type <> type ~ quality <> quality ~ premier <> premiere ~ description <> description ~ country <> country <> <> <> Object.values(_OBJECT_) ~ genre <> genre <> <> <> Object.values(_OBJECT_) ~ director.0 <> director ~ actors.0 <> actor <> 5 ~ voiceActing <> translate <> 1 ~ id <> custom.movie_id ~ world_art_id <> custom.wa_id ~ poster <> poster <> 1


    # Заполнение с API Alloha фильмы
    0 ~ https://api.alloha.tv/?token=04941a9a3ca3ac16e2b4327347bbc1&order=date&list=movie&page=[page] ~ data.0.id_kp ~ https://api.alloha.tv/?token=04941a9a3ca3ac16e2b4327347bbc1&kp=[id] ~ data.id_kp <> kp_id ~ data.id_imdb <> custom.imdb_id ~ data.id_tmdb <> custom.tmdb_id ~ data.id_world_art <> custom.wa_id ~ data.name <> title_ru ~ data.original_name <> title_en ~ data.year <> year ~ "movie" <> type ~ data.quality <> quality <> 1 <> <> "_VALUE_".split(",") ~ data.translation <> translate <> 1 <> <> "_VALUE_".split(",") ~ data.premiere <> premiere ~ data.description <> description ~ data.country <> country ~ data.genre <> genre <> <> <> "_VALUE_".split(",") ~ data.directors <> director <> <> <> "_VALUE_".split(",") ~ data.actors <> actor <> 5 <> <> "_VALUE_".split(",") ~ data.poster <> poster


    # Заполнение с API Alloha сериалы
    0 ~ https://api.alloha.tv/?token=04941a9a3ca3ac16e2b4327347bbc1&order=date&list=serial&page=[page] ~ data.0.id_kp ~ https://api.alloha.tv/?token=04941a9a3ca3ac16e2b4327347bbc1&kp=[id] ~ data.id_kp <> kp_id ~ data.id_imdb <> custom.imdb_id ~ data.id_tmdb <> custom.tmdb_id ~ data.id_world_art <> custom.wa_id ~ data.name <> title_ru ~ data.original_name <> title_en ~ data.year <> year ~ "serial" <> type ~ data.quality <> quality <> 1 <> <> "_VALUE_".split(",") ~ data.translation <> translate <> 1 <> <> "_VALUE_".split(",") ~ data.premiere <> premiere ~ data.description <> description ~ data.country <> country ~ data.genre <> genre <> <> <> "_VALUE_".split(",") ~ data.directors <> director <> <> <> "_VALUE_".split(",") ~ data.actors <> actor <> 5 <> <> "_VALUE_".split(",") ~ data.poster <> poster


    # Заполнение с API Bazon
    0 ~ https://bazon.cc/api/json/?token=2848f79ca09d4bbbf419bcdb464b4d11&type=all&limit=50&page=[page] ~ results.0.kinopoisk_id ~ https://bazon.cc/api/search?token=2848f79ca09d4bbbf419bcdb464b4d11&kp=[id] ~ results.0.kinopoisk_id <> kp_id <> 1 ~ results.0.info.rus <> title_ru <> 1 ~ results.0.info.orig <> title_en <> 1 ~ results.0.info.year <> year <> 1 ~ results.0.serial <> type <> 1 ~ results.0.quality <> quality <> 1 ~ results.0.translation <> translate <> 1 ~ results.0.info.premiere <> premiere <> 1 ~ results.0.info.description <> description <> 1 ~ results.0.info.country <> country <> 1 ~ results.0.info.genre <> genre <> 1 ~ results.0.info.director <> director <> 1 ~ results.0.info.actors <> actor <> 1 ~ results.0.info.poster <> poster <> 1


    # Заполнение ID TMDb + постер + красивое фото для фильмов, у которых уже есть ID IMDb
    0 ~ db ~ custom.imdb_id ~ https://api.themoviedb.org/3/find/tt[imdb_id]?api_key=269890f657dddf4635473cf4cf456576&external_source=imdb_id ~ movie_results.0.id <> custom.tmdb_id <> 1 ~ movie_results.0.poster_path <> poster <> 1 ~ movie_results.0.backdrop_path <> picture <> 1


    # Заполнение ID TMDb + постер + красивое фото для сериалов, у которых уже есть ID IMDb
    0 ~ db ~ custom.imdb_id ~ https://api.themoviedb.org/3/find/tt[imdb_id]?api_key=269890f657dddf4635473cf4cf456576&external_source=imdb_id ~ tv_results.0.id <> custom.tmdb_id <> 1 ~ tv_results.0.poster_path <> poster <> 1 ~ tv_results.0.backdrop_path <> pictures <> 1


    # Заполнение рейтинга КиноПоиск и IMDb, напрямую с КиноПоиска.
    0 ~ db ~ kp_id ~ https://rating.kinopoisk.ru/[id].xml ~ rating.kp_rating._attributes.num_vote <> kp_vote ~ rating.kp_rating._text <> kp_rating ~ rating.imdb_rating._attributes.num_vote <> imdb_vote ~ rating.imdb_rating._text <> imdb_rating


    # Заполнение постера с Bazon (постер с КиноПоиск, Яндекс, Shikimori, TMDb, IMDb)
    0 ~ db ~ ~ https://bazon.cc/api/search?token=2848f79ca09d4bbbf419bcdb464b4d11&kp=[id] ~ results.0.kinopoisk_id <> kp_id <> 1 ~ results.0.info.poster <> poster <> 1


    # Заполнение постера с Kodik (постер с Shikimori)
    0 ~ db ~ ~ https://kodikapi.com/search?token=b7cc4293ed475c4ad1fd599d114f4435&with_material_data=true&kinopoisk_id=[id] ~ results.0.kinopoisk_id <> kp_id <> 1 ~ results.0.material_data.poster_url <> poster <> 1
```

4. Запускаете получение:

![Запускаете получение](https://raw.githubusercontent.com/theme-masters/Yohoho-theme/master/4.png)

5. Смотрите как наполняется сайт:

![Смотрите как наполняется сайт](https://raw.githubusercontent.com/theme-masters/Yohoho-theme/master/5.png)

## когда на сайт добавится 60 000 - 70 000 фильмов и сериалов, как добавлять все остальные новые и новые фильмы и сериалы автоматически ([от сюда](https://enota.club/threads/sozdanie-onlajn-kinoteatra-s-doramami-anime-avtodobavlenie-novyx-20-000-filmov.2999/))?

1. изменить `[page]` на `1` чтобы не обходить все страницы api балансеров а заходить только на первую где новые фильмы

2. изменить `0` на `2` чтобы за новыми фильмами сайт ходил смотреть каждые 2 часа

3. изменить `db` на `lastmod` чтобы не обходить всю базу данных а только последние измененные фильмы

```
    # Заполнение с API Kodik
    2 ~ http://kodikapi.com/list?limit=100&with_material_data=true&token=45c53578f11ecfb74e31267b634cc6a8&page=1 ~ results ~ ~ kinopoisk_id <> kp_id ~ material_data.title <> title_ru ~ material_data.title_en <> title_en ~ material_data.year <> year ~ material_data.description <> description ~ material_data.poster_url <> poster ~ material_data.screenshots <> pictures ~ material_data.countries <> country ~ material_data.genres <> genre ~ material_data.premiere_world <> premiere ~ material_data.actors <> actor ~ material_data.directors <> director ~ type <> type


    # Заполнение с API Collaps
    2 ~ https://apicollaps.cc/list?token=eedefb541aeba871dcfc756e6b31c02e&limit=99&page=1 ~ results.0.id ~ https://apicollaps.cc/franchise/details?token=eedefb541aeba871dcfc756e6b31c02e&id=[id] ~ kinopoisk_id <> kp_id ~ imdb_id <> custom.imdb_id ~ name <> title_ru ~ name_eng <> title_en ~ year <> year ~ type <> type ~ quality <> quality ~ premier <> premiere ~ description <> description ~ country <> country <> <> <> Object.values(_OBJECT_) ~ genre <> genre <> <> <> Object.values(_OBJECT_) ~ director.0 <> director ~ actors.0 <> actor <> 5 ~ voiceActing <> translate <> 1 ~ id <> custom.movie_id ~ world_art_id <> custom.wa_id ~ poster <> poster <> 1


    # Заполнение с API Alloha фильмы
    2 ~ https://api.alloha.tv/?token=04941a9a3ca3ac16e2b4327347bbc1&order=date&list=movie&page=1 ~ data.0.id_kp ~ https://api.alloha.tv/?token=04941a9a3ca3ac16e2b4327347bbc1&kp=[id] ~ data.id_kp <> kp_id ~ data.id_imdb <> custom.imdb_id ~ data.id_tmdb <> custom.tmdb_id ~ data.id_world_art <> custom.wa_id ~ data.name <> title_ru ~ data.original_name <> title_en ~ data.year <> year ~ "movie" <> type ~ data.quality <> quality <> 1 <> <> "_VALUE_".split(",") ~ data.translation <> translate <> 1 <> <> "_VALUE_".split(",") ~ data.premiere <> premiere ~ data.description <> description ~ data.country <> country ~ data.genre <> genre <> <> <> "_VALUE_".split(",") ~ data.directors <> director <> <> <> "_VALUE_".split(",") ~ data.actors <> actor <> 5 <> <> "_VALUE_".split(",") ~ data.poster <> poster


    # Заполнение с API Alloha сериалы
    2 ~ https://api.alloha.tv/?token=04941a9a3ca3ac16e2b4327347bbc1&order=date&list=serial&page=1 ~ data.0.id_kp ~ https://api.alloha.tv/?token=04941a9a3ca3ac16e2b4327347bbc1&kp=[id] ~ data.id_kp <> kp_id ~ data.id_imdb <> custom.imdb_id ~ data.id_tmdb <> custom.tmdb_id ~ data.id_world_art <> custom.wa_id ~ data.name <> title_ru ~ data.original_name <> title_en ~ data.year <> year ~ "serial" <> type ~ data.quality <> quality <> 1 <> <> "_VALUE_".split(",") ~ data.translation <> translate <> 1 <> <> "_VALUE_".split(",") ~ data.premiere <> premiere ~ data.description <> description ~ data.country <> country ~ data.genre <> genre <> <> <> "_VALUE_".split(",") ~ data.directors <> director <> <> <> "_VALUE_".split(",") ~ data.actors <> actor <> 5 <> <> "_VALUE_".split(",") ~ data.poster <> poster


    # Заполнение с API Bazon
    2 ~ https://bazon.cc/api/json/?token=2848f79ca09d4bbbf419bcdb464b4d11&type=all&limit=50&page=1 ~ results.0.kinopoisk_id ~ https://bazon.cc/api/search?token=2848f79ca09d4bbbf419bcdb464b4d11&kp=[id] ~ results.0.kinopoisk_id <> kp_id <> 1 ~ results.0.info.rus <> title_ru <> 1 ~ results.0.info.orig <> title_en <> 1 ~ results.0.info.year <> year <> 1 ~ results.0.serial <> type <> 1 ~ results.0.quality <> quality <> 1 ~ results.0.translation <> translate <> 1 ~ results.0.info.premiere <> premiere <> 1 ~ results.0.info.description <> description <> 1 ~ results.0.info.country <> country <> 1 ~ results.0.info.genre <> genre <> 1 ~ results.0.info.director <> director <> 1 ~ results.0.info.actors <> actor <> 1 ~ results.0.info.poster <> poster <> 1


    # Заполнение ID TMDb + постер + красивое фото для фильмов, у которых уже есть ID IMDb
    2 ~ lastmod ~ custom.imdb_id ~ https://api.themoviedb.org/3/find/tt[imdb_id]?api_key=269890f657dddf4635473cf4cf456576&external_source=imdb_id ~ movie_results.0.id <> custom.tmdb_id <> 1 ~ movie_results.0.poster_path <> poster <> 1 ~ movie_results.0.backdrop_path <> picture <> 1


    # Заполнение ID TMDb + постер + красивое фото для сериалов, у которых уже есть ID IMDb
    2 ~ lastmod ~ custom.imdb_id ~ https://api.themoviedb.org/3/find/tt[imdb_id]?api_key=269890f657dddf4635473cf4cf456576&external_source=imdb_id ~ tv_results.0.id <> custom.tmdb_id <> 1 ~ tv_results.0.poster_path <> poster <> 1 ~ tv_results.0.backdrop_path <> pictures <> 1


    # Заполнение рейтинга КиноПоиск и IMDb, напрямую с КиноПоиска.
    2 ~ lastmod ~ kp_id ~ https://rating.kinopoisk.ru/[id].xml ~ rating.kp_rating._attributes.num_vote <> kp_vote ~ rating.kp_rating._text <> kp_rating ~ rating.imdb_rating._attributes.num_vote <> imdb_vote ~ rating.imdb_rating._text <> imdb_rating


    # Заполнение постера с Bazon (постер с КиноПоиск, Яндекс, Shikimori, TMDb, IMDb)
    2 ~ lastmod ~ ~ https://bazon.cc/api/search?token=2848f79ca09d4bbbf419bcdb464b4d11&kp=[id] ~ results.0.kinopoisk_id <> kp_id <> 1 ~ results.0.info.poster <> poster <> 1


    # Заполнение постера с Kodik (постер с Shikimori)
    2 ~ lastmod ~ ~ https://kodikapi.com/search?token=b7cc4293ed475c4ad1fd599d114f4435&with_material_data=true&kinopoisk_id=[id] ~ results.0.kinopoisk_id <> kp_id <> 1 ~ results.0.material_data.poster_url <> poster <> 1
```

# как поставить все балансеры в рунете в плеер ([от сюда](https://enota.club/threads/kak-podkljuchit-videobalanser-hdvb.1781/page-2#post-24906))?

![агрегатор плееров](https://raw.githubusercontent.com/theme-masters/Yohoho-theme/master/7.png)

1. дашборд -> модуль плеер -> api

```
https://bazon.cc/api/search?token=2848f79ca09d4bbbf419bcdb464b4d11&kp=[kp_id] ~ "Базон" ~ results.0.link
https://apicollaps.cc/list?token=eedefb541aeba871dcfc756e6b31c02e&kinopoisk_id=[kp_id] ~ "Колапс" ~ results.0.iframe_url
https://videocdn.tv/api/short?api_token=pfp3D870PGEY3Afjti0gMtSfmn2aZqih&kinopoisk_id=[kp_id] ~ "Видеосдн" ~ data.0.iframe_src
https://api.alloha.tv/?token=d317441359e505c343c2063edc97e7&kp=[kp_id] ~ "Алоха" ~ data.iframe
https://api.bhcesh.me/list?token=eedefb541aeba871dcfc756e6b31c02e&kinopoisk_id=[kp_id] ~ "Бхцеш" ~ results.0.iframe_url
https://kodikapi.com/search?token=b7cc4293ed475c4ad1fd599d114f4435&kinopoisk_id=[kp_id] ~ "Кодик" ~ results.0.link
https://apivb.info/api/videos.json?token=5e2fe4c70bafd9a7414c4f170ee1b192&id_kp=[kp_id] ~ "Хдвб" ~ iframe_url
https://iframe.video/api/v2/search?kp=[kp_id] ~ "Ифрейм" ~ results.path
https://pleer.video/[kp_id].json ~ "Иви" ~ embeds.0.iframe
https://api.themoviedb.org/3/[type]/[tmdb_id]?language=ru&append_to_response=videos&api_key=4f06fae67ddcf28e2e5b3f91193cb555 ~ "Трейлер (TMDb)" ~ videos.results.0.key <> https://www.youtube.com/embed/_VALUE_ ~ videos.results.0.key <> https://img.youtube.com/vi/_VALUE_/maxresdefault.jpg
https://www.googleapis.com/youtube/v3/search?part=id,snippet&maxResults=1&key=AIzaSyDcr11tMC1PDGyLAyWP7K2XYD9FeWARPnA&q=[title] [year] трейлер ~ "Трейлер (YouTube)" ~ items.0.id.videoId <> https://www.youtube.com/embed/_VALUE_ ~ items.0.id.videoId <> https://img.youtube.com/vi/_VALUE_/maxresdefault.jpg
```

2. замени все токены своими собственными

## как раздавать свои плееры всем желающим html сайтам?

```
<iframe src="https://get-video-player.com/iframe/id-кинопоиск" frameborder="0" width="640" height="360">
```

## как раздавать свои плееры всем желающим nodejs сайтам?

1. дашборд -> модуль плеер -> api

```
https://get-video-player.com/iframe/[id] ~ [iframe]
```

2. дашборд -> модуль плеер -> Настройка встраиваемого плеера /embed/[id]

```
"data-cinemaplayer-tabs-left": "160px"
```

## как раздавать свои плееры всем желающим php/java/python сайтам?

1. сделаешь токен для вебмастера которому хочешь дать плеер

2. плееры вебмастер получает по api

```
https://get-video-player.com/api?token=TEST&id=id-кинопоиск
```

#### инстркуция не является призывом к твоим незаконным действиям ;)

<a href="https://www.buymeacoffee.com/congar" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="41" width="174"></a>

<a href="https://patreon.com/congar"><img src="https://img.shields.io/endpoint.svg?url=https%3A%2F%2Fshieldsio-patreon.vercel.app%2Fapi%3Fusername%3Dendel%26type%3Dpledges&style=for-the-badge" /> </a>