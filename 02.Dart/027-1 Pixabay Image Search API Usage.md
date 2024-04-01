# API 문서

> <https://pixabay.com/>

> <https://pixabay.com/api/docs/#api_support>

PIxabay 가입 후 api 문서 링크를 통해 이동하면 api이용방법에 대해 나와있음

# Image Search

이미지 검색의 기본 URL 은 아래와 같음

> (GET) <https://pixabay.com/api/>

## Parameters

이미지 검색에 필요한 필수 + 선택 파라미터는 다음과 같이 나와있다.

| name           | type   | description                                                                                                                                                                                                                                                                  |
| -------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| key (required) | str    | Your API key: ****                                                                                                                                                                                                                                                           |
| q              | str    | A URL encoded search term. If omitted, _all images_ are returned. This value may not exceed 100 characters.  <br>Example: "yellow+flower"                                                                                                                                    |
| lang           | str    | [Language code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) of the language to be searched in.  <br>Accepted values: cs, da, de, en, es, fr, id, it, hu, nl, no, pl, pt, ro, sk, fi, sv, tr, vi, th, bg, ru, el, ja, ko, zh  <br>Default: "en"                    |
| id             | str    | Retrieve individual images by ID.                                                                                                                                                                                                                                            |
| image_type     | str    | Filter results by image type.  <br>Accepted values: "all", "photo", "illustration", "vector"  <br>Default: "all"                                                                                                                                                             |
| orientation    | str    | Whether an image is wider than it is tall, or taller than it is wide.  <br>Accepted values: "all", "horizontal", "vertical"  <br>Default: "all"                                                                                                                              |
| category       | str    | Filter results by category.  <br>Accepted values: backgrounds, fashion, nature, science, education, feelings, health, people, religion, places, animals, industry, computer, food, sports, transportation, travel, buildings, business, music                                |
| min_width      | int    | Minimum image width.  <br>Default: "0"                                                                                                                                                                                                                                       |
| min_height     | int    | Minimum image height.  <br>Default: "0"                                                                                                                                                                                                                                      |
| colors         | str    | Filter images by color properties. A comma separated list of values may be used to select multiple properties.  <br>Accepted values: "grayscale", "transparent", "red", "orange", "yellow", "green", "turquoise", "blue", "lilac", "pink", "white", "gray", "black", "brown" |
| editors_choice | bool   | Select images that have received an [Editor's Choice](https://pixabay.com/editors_choice/) award.  <br>Accepted values: "true", "false"  <br>Default: "false"                                                                                                                |
| safesearch     | bool   | A flag indicating that only images suitable for all ages should be returned.  <br>Accepted values: "true", "false"  <br>Default: "false"                                                                                                                                     |
| order          | str    | How the results should be ordered.  <br>Accepted values: "popular", "latest"  <br>Default: "popular"                                                                                                                                                                         |
| page           | int    | Returned search results are paginated. Use this parameter to select the page number.  <br>Default: 1                                                                                                                                                                         |
| per_page       | int    | Determine the number of results per page.  <br>Accepted values: 3 - 200  <br>Default: 20                                                                                                                                                                                     |
| callback       | string | JSONP callback function name                                                                                                                                                                                                                                                 |
| pretty         | bool   | Indent JSON output. This option should not be used in production.  <br>Accepted values: "true", "false"  <br>Default: "false"                                                                                                                                                |

가장 자주 쓰이는 파라미터는 아래와 같다

- `key` — (필수) api 요청에 필요한 api 키 스트링
- `image_type` — 검색 결과를 필터링 할 이미지 타입 ("all", "photo", "illustration", "vector") (기본값 : "all" )
- `q` — URL로 인코딩 된 검색어, 만약에 생략되었다면 모든 이미지가 검색결과로 반환됨, 최대 100글자로 제한
- `id` — ID로 개별 이미지를 검색
- `pretty` —

몇개의 단어로 간단한 이미지 검색 api 요청을 하면 다음과 같다.

`https://pixabay.com/api/?key=43170873-f37e577d19b4e9b1bd2ecc27b&q=yellow+flowers&image_type=photo`

그리고 다음과 같은 Response 가 오게 된다.

```json
{
"total": 4692,
"totalHits": 500,
"hits": [
    {
        "id": 195893,
        "pageURL": "https://pixabay.com/en/blossom-bloom-flower-195893/",
        "type": "photo",
        "tags": "blossom, bloom, flower",
        "previewURL": "https://cdn.pixabay.com/photo/2013/10/15/09/12/flower-195893_150.jpg"
        "previewWidth": 150,
        "previewHeight": 84,
        "webformatURL": "https://pixabay.com/get/35bbf209e13e39d2_640.jpg",
        "webformatWidth": 640,
        "webformatHeight": 360,
        "largeImageURL": "https://pixabay.com/get/ed6a99fd0a76647_1280.jpg",
        "fullHDURL": "https://pixabay.com/get/ed6a9369fd0a76647_1920.jpg",
        "imageURL": "https://pixabay.com/get/ed6a9364a9fd0a76647.jpg",
        "imageWidth": 4000,
        "imageHeight": 2250,
        "imageSize": 4731420,
        "views": 7671,
        "downloads": 6439,
        "likes": 5,
        "comments": 2,
        "user_id": 48777,
        "user": "Josch13",
        "userImageURL": "https://cdn.pixabay.com/user/2013/11/05/02-10-23-764_250x250.jpg",
    },
    {
        "id": 73424,
        ...
    },
    ...
]
}
```
