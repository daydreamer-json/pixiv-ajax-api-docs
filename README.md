# Pixiv Ajax API

The details of the pixiv ajax API.

---

I am currently gradually transferring old documents to **Postman**.

## Postman workspace

<a href="https://postman.com/daydreamer-json/pixiv" target="_blank" rel="noopener noreferrer"><img src="https://voyager.postman.com/logo/postman-logo-orange.svg" height=100></a>

---

**This repository and documentation have been unmaintained and neglected for a long time. During the unmaintained period, the pixiv Ajax API has undergone numerous specification changes, which has reduced its reliability.**

**For this reason, I plan to rewrite this document. Please wait for a while.**

Issue: [#3](https://github.com/daydreamer-json/pixiv-ajax-api-docs/issues/3)

---

**Table of contents**

- [Pixiv Ajax API](#pixiv-ajax-api)
  * [Note](#note)
  * [Ajax API Base URL](#ajax-api-base-url)
  * [CORS](#cors)
  * [Authorization](#authorization)
    + [User-Agent](#user-agent)
    + [Authorization Method 1](#authorization-method-1)
    + [Authorization Method 2](#authorization-method-2)
  * [Top Page](#top-page)
    + [Get top page artworks](#get-top-page-artworks)
  * [User Information](#user-information)
    + [Get user information (short)](#get-user-information-short)
    + [Get user information (full)](#get-user-information-full)
    + [Get user information (focus on artwork)](#get-user-information-focus-on-artwork)
    + [Get following users](#get-following-users)
    + [Get user's followers](#get-users-followers)
    + [Get user latest artworks](#get-user-latest-artworks)
    + [Get user bookmarks](#get-user-bookmarks)
    + [Get users who are live steaming](#get-users-who-are-live-streaming)
    + [Get your own user extra data](#get-your-own-user-extra-data)
    + [Get new artwork from users you follow](#get-new-artwork-from-users-you-follow)
    + [Get manga on your watchlist](#get-manga-on-your-watchlist)
    + [Get your mypic artworks](#get-your-mypic-artworks)
  * [User Dashboard](#user-dashboard)
    + [Get your dashboard home information](#get-your-dashboard-home-information)
    + [Get your dashboard settings](#get-your-dashboard-settings)
    + [Get your illust request strategy](#get-your-illust-request-strategy)
  * [Artworks](#artworks)
    + [Get artwork information](#get-artwork-information)
    + [Get artwork comments](#get-artwork-comments)
    + [Get artwork image URL](#get-artwork-image-url)
    + [Get artwork recommendation](#get-artwork-recommendation)
    + [Add artwork to bookmarks](#add-artwork-to-bookmarks)
    + [Like an artwork](#like-an-artwork)
  * [Tags](#tags)
    + [Get tag information](#get-tag-information)
    + [Get tag storyId](#get-tag-storyid)
  * [Ranking](#ranking)
    + [Get ranking data](#get-ranking-data)
  * [Search](#search)
    + [Search top artworks](#search-top-artworks)
    + [Search artworks](#search-artworks)
    + [Search illustrations](#search-illustrations)
    + [Search manga](#search-manga)
  * [Requests](#requests)
    + [Get all request information](#get-all-request-information)
    + [Get the completed request illusts](#get-the-completed-request-illusts)
    + [Get the completed request manga](#get-the-completed-request-manga)
    + [Get the completed request ugoira](#get-the-completed-request-ugoira)
    + [Get users who have posted requested illusts](#get-users-who-have-posted-requested-illusts)
    + [Get users who have posted requested manga](#get-users-who-have-posted-requested-manga)
    + [Get users who have posted requested ugoira](#get-users-who-have-posted-requested-ugoira)
    + [Get request artworks in progress](#get-request-artworks-in-progress)
    + [Get request illusts in progress](#get-request-illusts-in-progress)
    + [Get request manga in progress](#get-request-manga-in-progress)
    + [Get request ugoira in progress](#get-request-ugoira-in-progress)
  * [Discovery](#discovery)
    + [Get artworks of Discovery page](#get-artworks-of-discovery-page)
    + [Get users of Discovery page](#get-users-of-discovery-page)
    + [Get page meta info of Discovery artworks page](#get-page-meta-info-of-discovery-artworks-page)
    + [Get page meta info of Discovery users page](#get-page-meta-info-of-discovery-users-page)
  * [New artworks](#new-artworks)
    + [Get new artworks](#get-new-artworks)
  * [Miscellaneous](#miscellaneous)
    + [Get webpush information](#get-webpush-information)
    + [Get notifications](#get-notifications)
    + [Get linked_service information](#get-linked_service-information)

---

## Note

This document was created and published for research purposes only. This document is unofficial and in no way affiliated with pixiv. Misuse of the API by this document is prohibited.

## Ajax API Base URL

```plaintext
https://www.pixiv.net/ajax
```

## CORS

The pixiv Ajax API **does probably not support CORS** and there is no `Access-Control-Allow-Origin` in the HTTP header of the response.  Therefore, to use the pixiv Ajax API **in a web browser**, **you must use a proxy that provides CORS headers.**

## Authorization

Authorization is required to use some parameters of the pixiv Ajax API. 

### User-Agent

I recommend specifying a User-Agent when sending requests to the API. (`User-Agent: {USER-AGENT}`)

Here is an example of User-Agent:

```plaintext
Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.0.0 Safari/537.36
```

(Windows 10 64-bit, Chrome v104)

### Authorization Method 1

First, log in to pixiv with a browser and get the Cookie data. Then, add the saved Cookie data to the request header to the API and send. (`Cookie: {RAW_COOKIE_DATA}`) 

Cookie data can be obtained using Chrome/Firefox developer tools. For iOS, you can use [Proxyman](https://apps.apple.com/jp/app/id1551292695) to get the Cookie data.

There are some endpoints that cannot be used by this method alone. For example, the endpoint that uses the `POST`.

### Authorization Method 2

First, log in to pixiv with a browser and get the `PHPSESSID` data. Then, add the saved `PHPSESSID` data to the request header to the API and send. (`Cookie: PHPSESSID={PHPSESSID}`)

`PHPSESSID` data can be obtained using Chrome/Firefox developer tools. For iOS, you can use [Proxyman](https://apps.apple.com/jp/app/id1551292695) to get the `PHPSESSID` data.

Thanks to [@X-Gorn](https://github.com/X-Gorn) ([#1](https://github.com/daydreamer-json/pixiv-ajax-api-docs/issues/1))

There are some endpoints that cannot be used by this method alone.

---

## Top page

Get the information in the top page.

### Get top page artworks

Get the artworks in the top page.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/top/illust
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|mode|`all`,`safe`,`r18`|`r18` cannot be used without login authorization.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/top/illust?mode=all
```

[JSON response](json/example_response/ajax/top/illust.json)

</details>

## User Information

Get user information in various formats.

### Get user information (short)

Get user information in a simplified format.

```plaintext
https://www.pixiv.net/ajax/user/{USER_ID}
```

Method: `GET`

Referer: `https://www.pixiv.net/member.php?id={USER_ID}`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/user/9153585
```

[JSON response](json/example_response/ajax/user/9153585.json)

</details>

### Get user information (full)

Get full user information.

```plaintext
https://www.pixiv.net/ajax/user/{USER_ID}?full=1
```

Method: `GET`

Referer: `https://www.pixiv.net/member.php?id={USER_ID}`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/user/9153585?full=1
```

[JSON response](json/example_response/ajax/user/9153585_full_1.json)

</details>

### Get user information (focus on artwork)

Get user information along with information about artwork posted by the user.

```plaintext
https://www.pixiv.net/ajax/user/{USER_ID}/profile/all
```

Method: `GET`

Referer: `https://www.pixiv.net/member.php?id={USER_ID}`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/user/9153585/profile/all
```

[JSON response](json/example_response/ajax/user/9153585/profile/all.json)

</details>

### Get following users

Get following users.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/user/{USER_ID}/following?offset={OFFSET_COUNT}&limit={LIMIT_COUNT}&rest=show
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/user/9153585/following?offset=0&limit=3&rest=show
```

[JSON response](json/example_response/ajax/user/9153585/following_offset_0_limit_3_rest_show.json)

</details>

### Get user's followers

Get user's followers.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/user/{USER_ID}/followers?offset={OFFSET_COUNT}&limit={LIMIT_COUNT}
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/user/43192924/followers?offset=0&limit=3
```

[JSON response](json/example_response/ajax/user/43192924/followers_offset_0_limit_3.json)

</details>

### Get user latest artworks

Get the latest artworks of users.

```plaintext
https://www.pixiv.net/ajax/user/{USER_ID}/works/latest
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/user/9153585/works/latest
```

[JSON response](json/example_response/ajax/user/9153585/works/latest.json)

</details>

### Get user bookmarks

Get bookmarks of users.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/user/{USER_ID}/illusts/bookmarks?tag={TAG}&offset={OFFSET_COUNT}&limit={LIMIT_COUNT}&rest=show
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|tag|string|Specify tags. Even if you do not specify a tag, you must include an empty tag in your query.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/user/43192924/illusts/bookmarks?tag=&offset=0&limit=3&rest=show
```

[JSON response](json/example_response/ajax/user/43192924/illusts/bookmarks_tag_offset_0_limit_3_rest_show.json)

</details>

### Get users who are live streaming

Get users you are following who are live streaming.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/sketch/live/following
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/sketch/live/following
```

[JSON response](json/example_response/ajax/sketch/live/following.json)

</details>

### Get your own user extra data

Get your own user extra data.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/user/extra
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/user/extra
```

[JSON response](json/example_response/ajax/user/extra.json)

</details>

### Get new artwork from users you follow

Get new artwork from users you follow.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/follow_latest/illust
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|mode|`all`,`safe`,`r18`||
|p|integer|Specifies the page number.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/follow_latest/illust?mode=all&p=1
```

[JSON response](json/example_response/ajax/follow_latest/illust_mode_all_p_1.json)

</details>

### Get manga on your watchlist

Get manga on your watchlist.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/watch_list/manga
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|p|integer|Specifies the page number.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/watch_list/manga?p=1
```

[JSON response](json/example_response/ajax/watch_list/manga_p_1.json)

</details>

### Get your mypic artworks

Get your mypic artworks.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/mypixiv_latest/illust
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|p|integer|Specifies the page number.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/mypixiv_latest/illust?p=1
```

[JSON response](json/example_response/ajax/mypixiv_latest/illust_p_1.json)

</details>

## User dashboard

Get user dashboard information.

### Get your dashboard home information

Get your dashboard home information.

```plaintext
https://www.pixiv.net/ajax/dashboard/home
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/dashboard/home
```

[JSON response](json/example_response/ajax/dashboard/home.json)

</details>

### Get your dashboard settings

Get your dashboard settings.

```plaintext
https://www.pixiv.net/ajax/dashboard/settings
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/dashboard/settings
```

[JSON response](json/example_response/ajax/dashboard/settings.json)

</details>

### Get your illust request strategy

Get your illust request strategy

```plaintext
https://www.pixiv.net/ajax/dashboard/works/illust/request_strategy
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/dashboard/works/illust/request_strategy
```

[JSON response](json/example_response/ajax/dashboard/works/illust/request_strategy.json)

</details>

## Artworks

Get various information about the artwork.

### Get artwork information

Get artwork information.

```plaintext
https://www.pixiv.net/ajax/illust/{ARTWORK_ID}
```

Method: `GET`

Referer: `https://www.pixiv.net/artworks/{ARTWORK_ID}`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/illust/100412238
```

[JSON response](json/example_response/ajax/illust/100412238.json)

</details>

### Get artwork comments

Get the comments posted to the artwork.

```plaintext
https://www.pixiv.net/ajax/illusts/comments/roots?illust_id={ARTWORK_ID}&offset={OFFSET_COUNT}&limit={LIMIT_COUNT}
```

Method: `GET`

Referer: `https://www.pixiv.net/artworks/{ARTWORK_ID}`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/illusts/comments/roots?illust_id=100412238&offset=0&limit=3
```

[JSON response](json/example_response/ajax/illusts/comments/roots_illust_id_100412238_offset_0_limit_3.json)

</details>

### Get artwork image URL

Get image URL of artwork.

```plaintext
https://www.pixiv.net/ajax/illust/{ARTWORK_ID}/pages
```

Method: `GET`

Referer: `https://www.pixiv.net/artworks/{ARTWORK_ID}`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/illust/100412238/pages
```

[JSON response](json/example_response/ajax/illust/100412238/pages.json)

</details>

### Get artwork recommendation

Get recommendations related to artwork.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/illust/{ARTWORK_ID}/recommend/init?limit=[LIMIT_COUNT]
```

Method: `GET`

Referer: `https://www.pixiv.net/artworks/{ARTWORK_ID}`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/illust/100412238/recommend/init?limit=2
```

[JSON response](json/example_response/ajax/illust/100412238/recommend/init_limit_2.json)

</details>

### Add artwork to bookmarks

Add an artwork to bookmarks.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/illusts/bookmarks/add
```

Method: `POST`

Request body type: `application/json`

Referer: `https://www.pixiv.net/`

**Request body parameters:**

|Key|Type|Info|
|---|---|---|
|comment|string|Specify the comment on the bookmark.|
|illust_id|integer|Specify the artwork ID.|
|restrict|`0`,`1`|If you specify `0`, the privacy settings of the bookmark will be "public". If you specify `1`, the privacy settings of the bookmark will be "private".|
|tags|list(string)|Specify the tag to be added to the bookmark.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/illusts/bookmarks/add
```

```json
{
  "comment": "",
  "illust_id": "101026657",
  "restrict": 0,
  "tags": []
}
```

[JSON response](json/example_response/ajax/illusts/bookmarks/add.json)

</details>

### Like an artwork

Like an artwork.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/illusts/like
```

Method: `POST`

Request body type: `application/json`

Referer: `https://www.pixiv.net/`

**Request body parameters:**

|Key|Type|Info|
|---|---|---|
|illust_id|integer|Specify the artwork ID.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/illusts/like
```

```json
{
  "illust_id": "101026657"
}
```

[JSON response](json/example_response/ajax/illusts/like.json)

</details>

## Tags

Get tags information.

### Get tag information

Get detailed information of a tag.

```plaintext
https://www.pixiv.net/ajax/search/tags/{TAG_NAME}
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/search/tags/%E5%8E%9F%E7%A5%9E
```

[JSON response](json/example_response/ajax/search/tags/原神.json)

</details>

### Get tag storyId

Get tag storyId.

```plaintext
https://www.pixiv.net/ajax/stories/tag_stories?tag={TAG_NAME}
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/stories/tag_stories?tag=%E5%8E%9F%E7%A5%9E
```

[JSON response](json/example_response/ajax/stories/tag_stories_tag_原神.json)

</details>

## Ranking

Get artwork ranking data.

### Get ranking data

Get artwork ranking data.

Ajax API base URL is not used.

```plaintext
https://www.pixiv.net/ranking.php
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|format|`json`|You can only use `json`.|
|mode|`daily`,`weekly`,`monthly`,<br>`male`,`female`,<br>`rookie`,`original`,<br>`daily_r18`,`weekly_r18`,<br>`male_r18`,`female_r18`|`r18` cannot be used without login authorization.|
|date|yyyymmdd|Used to get the ranking of the specified date. If not specified, get the latest ranking.|
|content|`complex`,`illust`,`ugoira`,`manga`|Filter the rankings by artwork type. If `complex` is specified, filtering will be canceled.|
|p|integer|Specifies the page number. Get 50 artwork per page.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ranking.php?format=json&mode=weekly&content=illust&p=1
```

[JSON response](json/example_response/ranking_format_json_mode_weekly_content_illust_p_1.json)

</details>

## Search

Search artworks.

### Search top artworks

Search various types of top artworks.

```plaintext
https://www.pixiv.net/ajax/search/top/{KEYWORD}
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/search/top/%E5%8E%9F%E7%A5%9E
```

[JSON response](json/example_response/ajax/search/top/原神.json)

</details>

### Search artworks

Search artworks.

```plaintext
https://www.pixiv.net/ajax/search/artworks/{KEYWORD}?word={KEYWORD}
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|type|`all`|You can only use `all`.|
|order|`date_d`,`date`,<br>`popular_d`,`popular`,<br>`popular_male_d`,`popular_male`,<br>`popular_female_d`,`popular_female`|Premium account authorization is required to use `popular*`.|
|mode|`all`,`safe`,`r18`|`r18` cannot be used without login authorization.|
|s_mode|`s_tag_full`,`s_tag`,`s_tc`|Specify `s_tag_full` to search by tag (exact match). Specify `s_tag` to search by tag (partial match). Specify `s_tc` to search by title or caption.|
|wlt|integer|Filter by minimum image width. If not specified, the filter will be disabled.|
|wgt|integer|Filter by maximum image width. If not specified, the filter will be disabled.|
|hlt|integer|Filter by minimum image height. If not specified, the filter will be disabled.|
|hgt|integer|Filter by maximum image height. If not specified, the filter will be disabled.|
|ratio|number|Filter by the image aspect ratio. `-0.5` is portrait, `0` is square, `0.5` is landscape. If not specified, the filter will be disabled.|
|tool|string|Filter by production tools. e.g. `Photoshop`|
|scd|yyyy-mm-dd|Get artwork posted after the specified date. If not specified, the filter will be disabled.|
|ecd|yyyy-mm-dd|Get artwork posted before the specified date. If not specified, the filter will be disabled.|
|blt|integer|Filter by minimum number of bookmarks. Premium account authorization is required. If not specified, the filter will be disabled.|
|bgt|integer|Filter by maximum number of bookmarks. Premium account authorization is required. If not specified, the filter will be disabled.|
|p|integer|Specifies the page number.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/search/artworks/%E5%8E%9F%E7%A5%9E?word=%E5%8E%9F%E7%A5%9E&type=all&order=date_d&mode=all&s_mode=s_tag_full
```

[JSON response](json/example_response/ajax/search/artworks/原神_word_原神_type_all_order_date_d_mode_all_s_mode_s_tag_full.json)

</details>

### Search illustrations

Search illustrations among artworks.

```plaintext
https://www.pixiv.net/ajax/search/illustrations/{KEYWORD}?word={KEYWORD}
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|type|`illust_and_ugoira`,`illust`,`ugoira`| Specify search target.|
|order|`date_d`,`date`,<br>`popular_d`,`popular`,<br>`popular_male_d`,`popular_male`,<br>`popular_female_d`,`popular_female`|Premium account authorization is required to use `popular*`.|
|mode|`all`,`safe`,`r18`|`r18` cannot be used without login authorization.|
|s_mode|`s_tag_full`,`s_tag`,`s_tc`|Specify `s_tag_full` to search by tag (exact match). Specify `s_tag` to search by tag (partial match). Specify `s_tc` to search by title or caption.|
|wlt|integer|Filter by minimum image width. If not specified, the filter will be disabled.|
|wgt|integer|Filter by maximum image width. If not specified, the filter will be disabled.|
|hlt|integer|Filter by minimum image height. If not specified, the filter will be disabled.|
|hgt|integer|Filter by maximum image height. If not specified, the filter will be disabled.|
|ratio|number|Filter by the image aspect ratio. `-0.5` is portrait, `0` is square, `0.5` is landscape. If not specified, the filter will be disabled.|
|tool|string|Filter by production tools. e.g. `Photoshop`|
|scd|yyyy-mm-dd|Get artwork posted after the specified date. If not specified, the filter will be disabled.|
|ecd|yyyy-mm-dd|Get artwork posted before the specified date. If not specified, the filter will be disabled.|
|blt|integer|Filter by minimum number of bookmarks. Premium account authorization is required. If not specified, the filter will be disabled.|
|bgt|integer|Filter by maximum number of bookmarks. Premium account authorization is required. If not specified, the filter will be disabled.|
|p|integer|Specifies the page number.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/search/illustrations/%E5%8E%9F%E7%A5%9E?word=%E5%8E%9F%E7%A5%9E&type=illust_and_ugoira&order=date_d&mode=all&s_mode=s_tag_full
```

[JSON response](json/example_response/ajax/search/illustrations/原神_word_原神_type_illust_and_ugoira_order_date_d_mode_all_s_mode_s_tag_full.json)

</details>

### Search manga

Search manga among artworks.

```plaintext
https://www.pixiv.net/ajax/search/manga/{KEYWORD}?word={KEYWORD}
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|type|`manga`|You can only use `manga`.|
|order|`date_d`,`date`,<br>`popular_d`,`popular`,<br>`popular_male_d`,`popular_male`,<br>`popular_female_d`,`popular_female`|Premium account authorization is required to use `popular*`.|
|mode|`all`,`safe`,`r18`|`r18` cannot be used without login authorization.|
|s_mode|`s_tag_full`,`s_tag`,`s_tc`|Specify `s_tag_full` to search by tag (exact match). Specify `s_tag` to search by tag (partial match). Specify `s_tc` to search by title or caption.|
|work_lang|string|Filter by the language of the text in artwork. Specify a two-letter language code. Japanese is `ja`.|
|wlt|integer|Filter by minimum image width. If not specified, the filter will be disabled.|
|wgt|integer|Filter by maximum image width. If not specified, the filter will be disabled.|
|hlt|integer|Filter by minimum image height. If not specified, the filter will be disabled.|
|hgt|integer|Filter by maximum image height. If not specified, the filter will be disabled.|
|ratio|number|Filter by the image aspect ratio. `-0.5` is portrait, `0` is square, `0.5` is landscape. If not specified, the filter will be disabled.|
|tool|string|Filter by production tools. e.g. `Photoshop`|
|scd|yyyy-mm-dd|Get artwork posted after the specified date. If not specified, the filter will be disabled.|
|ecd|yyyy-mm-dd|Get artwork posted before the specified date. If not specified, the filter will be disabled.|
|blt|integer|Filter by minimum number of bookmarks. Premium account authorization is required. If not specified, the filter will be disabled.|
|bgt|integer|Filter by maximum number of bookmarks. Premium account authorization is required. If not specified, the filter will be disabled.|
|p|integer|Specifies the page number.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/search/manga/%E5%8E%9F%E7%A5%9E?word=%E5%8E%9F%E7%A5%9E&type=manga&order=date_d&mode=all&s_mode=s_tag_full&p=1
```

[JSON response](json/example_response/ajax/search/manga/原神_word_原神_type_manga_order_date_d_mode_all_s_mode_s_tag_full.json)

</details>

## Requests

Get the request artworks.

### Get all request information

Get all request information

```plaintext
https://www.pixiv.net/ajax/commission/page/request
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/commission/page/request
```

[JSON response](json/example_response/ajax/commission/page/request.json)

</details>

### Get the completed request illusts

Get the completed request illusts.

```plaintext
https://www.pixiv.net/ajax/commission/page/request/complete/illust
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|mode|`all`,`safe`,`r18`|`r18` cannot be used without login authorization.|
|p|integer|Specifies the page number.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/commission/page/request/complete/illust?mode=all&p=1
```

[JSON response](json/example_response/ajax/commission/page/request/complete/illust_mode_all_p_1.json)

</details>

### Get the completed request manga

Get the completed request manga

```plaintext
https://www.pixiv.net/ajax/commission/page/request/complete/manga
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|mode|`all`,`safe`,`r18`|`r18` cannot be used without login authorization.|
|p|integer|Specifies the page number.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/commission/page/request/complete/manga?mode=all&p=1
```

[JSON response](json/example_response/ajax/commission/page/request/complete/manga_mode_all_p_1.json)

</details>

### Get the completed request ugoira

Get the completed request ugoira

```plaintext
https://www.pixiv.net/ajax/commission/page/request/complete/ugoira
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|mode|`all`,`safe`,`r18`|`r18` cannot be used without login authorization.|
|p|integer|Specifies the page number.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/commission/page/request/complete/ugoira?mode=all&p=1
```

[JSON response](json/example_response/ajax/commission/page/request/complete/ugoira_mode_all_p_1.json)

</details>

### Get users who have posted requested illusts

Get users who have posted requested illusts.

```plaintext
https://www.pixiv.net/ajax/commission/page/request/creators/illust
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|mode|`all`,`safe`,`r18`|`r18` cannot be used without login authorization.|
|p|integer|Specifies the page number.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/commission/page/request/creators/illust?mode=all&p=1
```

[JSON response](json/example_response/ajax/commission/page/request/creators/illust_mode_all_p_1.json)

</details>

### Get users who have posted requested manga

Get users who have posted requested manga.

```plaintext
https://www.pixiv.net/ajax/commission/page/request/creators/manga
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|mode|`all`,`safe`,`r18`|`r18` cannot be used without login authorization.|
|p|integer|Specifies the page number.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/commission/page/request/creators/manga?mode=all&p=1
```

[JSON response](json/example_response/ajax/commission/page/request/creators/manga_mode_all_p_1.json)

</details>

### Get users who have posted requested ugoira

Get users who have posted requested ugoira.

```plaintext
https://www.pixiv.net/ajax/commission/page/request/creators/ugoira
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|mode|`all`,`safe`,`r18`|`r18` cannot be used without login authorization.|
|p|integer|Specifies the page number.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/commission/page/request/creators/ugoira?mode=all&p=1
```

[JSON response](json/example_response/ajax/commission/page/request/creators/ugoira_mode_all_p_1.json)

</details>

### Get request artworks in progress

Get request artworks in progress.

```plaintext
https://www.pixiv.net/ajax/commission/page/request/in_progress/all
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|mode|`all`,`safe`,`r18`|`r18` cannot be used without login authorization.|
|p|integer|Specifies the page number.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/commission/page/request/in_progress/all?mode=all&p=1
```

[JSON response](json/example_response/ajax/commission/page/request/in_progress/all_mode_all_p_1.json)

</details>

### Get request illusts in progress

Get request illusts in progress.

```plaintext
https://www.pixiv.net/ajax/commission/page/request/in_progress/illust
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|mode|`all`,`safe`,`r18`|`r18` cannot be used without login authorization.|
|p|integer|Specifies the page number.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/commission/page/request/in_progress/illust?mode=all&p=1
```

[JSON response](json/example_response/ajax/commission/page/request/in_progress/illust_mode_all_p_1.json)

</details>

### Get request manga in progress

Get request manga in progress.

```plaintext
https://www.pixiv.net/ajax/commission/page/request/in_progress/manga
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|mode|`all`,`safe`,`r18`|`r18` cannot be used without login authorization.|
|p|integer|Specifies the page number.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/commission/page/request/in_progress/manga?mode=all&p=1
```

[JSON response](json/example_response/ajax/commission/page/request/in_progress/manga_mode_all_p_1.json)

</details>

### Get request ugoira in progress

Get request ugoira in progress.

```plaintext
https://www.pixiv.net/ajax/commission/page/request/in_progress/ugoira
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|mode|`all`,`safe`,`r18`|`r18` cannot be used without login authorization.|
|p|integer|Specifies the page number.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/commission/page/request/in_progress/ugoira?mode=all&p=1
```

[JSON response](json/example_response/ajax/commission/page/request/in_progress/ugoira_mode_all_p_1.json)

</details>

## Discovery

### Get artworks of Discovery page

Get artworks of Discovery page.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/discovery/artworks?limit={LIMIT_COUNT}
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|mode|`all`,`safe`,`r18`||

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/discovery/artworks?mode=all&limit=3
```

[JSON response](json/example_response/ajax/discovery/artworks_mode_all_limit_3.json)

</details>

### Get users of Discovery page

Get users of Discovery page.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/discovery/users?limit={LIMIT_COUNT}
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/discovery/users?limit=3
```

[JSON response](json/example_response/ajax/discovery/users_limit_3.json)

</details>

### Get page meta info of Discovery artworks page

Get page meta info of Discovery artworks page.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/discovery/artworks/meta
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|mode|`all`,`safe`,`r18`||

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/discovery/artworks/meta?mode=all
```

[JSON response](json/example_response/ajax/discovery/artworks/meta_mode_all.json)

</details>

### Get page meta info of Discovery users page

Get page meta info of Discovery users page.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/discovery/users/meta
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/discovery/users/meta
```

[JSON response](json/example_response/ajax/discovery/users/meta.json)

</details>

## New artworks

Get new artwork information.

### Get new artworks

Get new artworks.

```plaintext
https://www.pixiv.net/ajax/illust/new?lastId=0&limit={LIMIT_COUNT}
```

Method: `GET`

Referer: `https://www.pixiv.net/`

**Additional parameters:**

|Key|Type|Info|
|---|---|---|
|type|`illust`,`manga`|Specifies the type of artworks.|
|r18|boolean|Specify whether to include the R18 artworks.|

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/illust/new?lastId=0&limit=20&type=illust&r18=false
```

[JSON response](json/example_response/ajax/illust/new_lastId_0_limit_20_type_illust_r18_false.json)

</details>

## Miscellaneous

Get miscellaneous data.

### Get `webpush` information

Get `webpush` information.

```plaintext
https://www.pixiv.net/ajax/webpush
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/webpush
```

[JSON response](json/example_response/ajax/webpush.json)

</details>

### Get notifications

Get notifications.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/notification
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/notification
```

[JSON response](json/example_response/ajax/notification.json)

</details>

### Get `linked_service` information

Get `linked_service` information.

Login authorization is required.

```plaintext
https://www.pixiv.net/ajax/linked_service/tumeng?page={PAGE_COUNT}
```

Method: `GET`

Referer: `https://www.pixiv.net/`

<details>
<summary>Example response</summary>

```plaintext
https://www.pixiv.net/ajax/linked_service/tumeng
```

[JSON response](json/example_response/ajax/linked_service/tumeng.json)

</details>
