### Pixabay Search Images API

### 개요

Pixabay 서비스의 Search Images API를 정리했습니다.
분당 최대 100개의 요청이 가능합니다.

**URL**
```
https://pixabay.com/api/
```

### Parameters
- key (required) - `str`: 유저 고유의 API Key
  
<br>

- q - `str`: 검색 키워드 (최대 100자)<br>
  `ex) "yellow-flowers"`
<br>
  
- lang - `str` : 이미지를 검색할 때 쓸 언어의 언어 코드<br>
  `Accepted values : cs, da, de, en, es, fr, id, it, hu, nl, no, pl, pt, ro, sk, fi, sv, tr, vi, th, bg, ru, el, ja, ko, zh`<br>
  `Default : "en"`
<br>

- id - `str`: 검색할 이미지의 id
<br>

- image-type - `str`: 검색할 이미지의 유형<br>
  `Accepted values :  "all", "photo", "illustration", "vector"`<br>
  `Default : "all"`
<br>

- orientation - `str`: 검색할 이미지의 너비와 높이 제한<br>
  `Accepted values : "all", "horizontal"(너비가 큼), "vertical"(높이가 큼)`<br>
<br>

- category - `str`: 검색할 이미지의 카테고리<br>
  `Accepted values : backgrounds, fashion, nature, science, education, feelings, health, people, religion, places, animals, industry, computer, food, sports, transportation, travel, buildings, business, music`
<br>

- min-width - `int`: 최소 너비<br>
  `Default : 0`
<br>

- min-height - `int`: 최소 높이<br>
  `Default : 0`
<br>

- colors - `str`: 검색할 이미지의 색<br>
  `Accepted values : "grayscale", "transparent", "red", "orange", "yellow", "green", "turquoise", "blue", "lilac", "pink", "white", "gray", "black", "brown"`
<br>

- editors_choice - `bool`: 검색할 이미지가 [Editor's Choice](https://pixabay.com/editors_choice/)에 해당하는지에 대한 여부<br>
  `Accepted values : true, false`<br>
  `Default : false`
<br>

- safesearch - `bool`: 검색할 이미지가 모든 연령에 적합한지에 대한 여부<br>
  `Accepted values : true, false`<br>
  `Default : false`
<br>

- order - `str`: 결과 정렬 기준<br>
  `Accepted values : "popular", "latest"`<br>
  `Default : "popular"`
<br>

- page - `int`: 검색된 이미지들의 페이지 번호<br>
  `Default : 1`
<br>

- per_page - `int`: 한 페이지 당 이미지 개수<br>
  `Accepted values :  3 ~ 200`<br>
  `Default : 20`
<br>

- callback - `str`: JSONP 콜백 함수 이름
<br>

- pretty - `bool`: JSON에 들여쓰기 여부<br>
  `Accepted values : true, false`<br>
  `Default : false`
  
  
### Example

**Request**

빨간색 문 이미지를 3개만 검색, 검색한 결과의 첫 번째 페이지만 받기
```
https://pixabay.com/api/?key={key}
&q=red+door&page=1&per_page=3
```
![](https://velog.velcdn.com/images/chojja7188/post/6701d79f-ac51-474d-8e4e-ff1ca9db85eb/image.jpeg)

**Response**

```json
{
    "total": 306,
    "totalHits": 306,
    "hits": [
        {
            "id": 4955342,
            "pageURL": "https://pixabay.com/photos/dublin-home-house-ireland-europe-4955342/",
            "type": "photo",
            "tags": "dublin, home, house",
            "previewURL": "https://cdn.pixabay.com/photo/2020/03/21/22/18/dublin-4955342_150.jpg",
            "previewWidth": 150,
            "previewHeight": 100,
            "webformatURL": "https://pixabay.com/get/gbc0624d47d308a61ed073191285aa75071d644d53e335e2a54f2df90e12618f70851a0930aa0becc16d1e775d7a3f3c4a16f71ff2dbda640fb3074e43114555b_640.jpg",
            "webformatWidth": 640,
            "webformatHeight": 427,
            "largeImageURL": "https://pixabay.com/get/g733c6f5c78e2f58ef83629a6fb95eeb6a3a83e730560f109a9eac88fb8de29b98d68e3f0ffd0df4e81c194c8d893c7da6c82afee2bb7ebe8b225ae40e74bc273_1280.jpg",
            "imageWidth": 3053,
            "imageHeight": 2035,
            "imageSize": 2027349,
            "views": 26569,
            "downloads": 18268,
            "collections": 110,
            "likes": 81,
            "comments": 12,
            "user_id": 88716,
            "user": "ptrabattoni",
            "userImageURL": "https://cdn.pixabay.com/user/2013/12/06/14-07-36-644_250x250.jpg"
        },
        {
            "id": 5060234,
            "pageURL": "https://pixabay.com/photos/dark-fear-terror-factory-red-5060234/",
            "type": "photo",
            "tags": "dark, fear, terror",
            "previewURL": "https://cdn.pixabay.com/photo/2020/04/18/17/37/dark-5060234_150.jpg",
            "previewWidth": 150,
            "previewHeight": 100,
            "webformatURL": "https://pixabay.com/get/ge5147e80cde6a260972b4af22ecd1c5e84f9fa19674a29dd961866431ced913702b1c69a2e74ecf964e5112461e0c60b18da76f6800151567781dab9340622b4_640.jpg",
            "webformatWidth": 640,
            "webformatHeight": 428,
            "largeImageURL": "https://pixabay.com/get/g5a9ffd484970547bd3bc14518c3f985c20f963af8c11dc065c65b523c61fa292c80b8b4aff4a1cc0ed280bcdd9438ed1dcbd910a9ae001088db0c05e72cca7db_1280.jpg",
            "imageWidth": 6032,
            "imageHeight": 4032,
            "imageSize": 4086357,
            "views": 28548,
            "downloads": 24106,
            "collections": 61,
            "likes": 55,
            "comments": 7,
            "user_id": 16108050,
            "user": "phmaxiestevez",
            "userImageURL": "https://cdn.pixabay.com/user/2020/04/18/21-01-05-600_250x250.jpg"
        },
        {
            "id": 962755,
            "pageURL": "https://pixabay.com/photos/fall-leaves-multicoloured-door-962755/",
            "type": "photo",
            "tags": "fall, leaves, multicoloured",
            "previewURL": "https://cdn.pixabay.com/photo/2015/09/28/21/01/autumn-962755_150.jpg",
            "previewWidth": 150,
            "previewHeight": 126,
            "webformatURL": "https://pixabay.com/get/g9ddcee9889f881a09fe6af7672b2b7a0f247fdc9f9221739c5c0bcb7e31b8568575aafaf1fd803354c710d06706ff328_640.jpg",
            "webformatWidth": 640,
            "webformatHeight": 538,
            "largeImageURL": "https://pixabay.com/get/gf587da775ea5355f7a4d531a1de8f226cb3d01abdb83530a1ff1f402250f1abb4bc17d7eb9f0631ec07f5ab13d2925bf30caa9e6c042af6d90e4e06b6de82837_1280.jpg",
            "imageWidth": 3856,
            "imageHeight": 3246,
            "imageSize": 4095750,
            "views": 25342,
            "downloads": 13258,
            "collections": 296,
            "likes": 187,
            "comments": 22,
            "user_id": 901263,
            "user": "901263",
            "userImageURL": ""
        }
    ]
}
```
![](https://velog.velcdn.com/images/chojja7188/post/f89d86b7-688c-4797-a6d1-f936059c355f/image.png)



**Request**

id가 4955342인 이미지 검색
```
https://pixabay.com/api/?key={key}&id=4955342
```
![](https://velog.velcdn.com/images/chojja7188/post/6a161d5e-10de-461b-b611-a6f96c061725/image.jpeg)

**Response**

```json
{
    "total": 1,
    "totalHits": 1,
    "hits": [
        {
            "id": 4955342,
            "pageURL": "https://pixabay.com/photos/dublin-home-house-ireland-europe-4955342/",
            "type": "photo",
            "tags": "dublin, home, house",
            "previewURL": "https://cdn.pixabay.com/photo/2020/03/21/22/18/dublin-4955342_150.jpg",
            "previewWidth": 150,
            "previewHeight": 100,
            "webformatURL": "https://pixabay.com/get/g751516acf419230d2cbaa77f47f4053067208fb4920cccbbdbb0aeb9aa5472ab9db9ac62e9a2f22e4bc8b04b6594c55bf5d618430c07c840b1296adf75fe519f_640.jpg",
            "webformatWidth": 640,
            "webformatHeight": 427,
            "largeImageURL": "https://pixabay.com/get/g4a5c63d92ba957ffc9a55e957c4d5517f2f78e805511187bfec5769b11ccc68b7e104d77b94d48e3cbd3278fe26aaa70b623c13cc0c3634a9b0ad7ac8883fa45_1280.jpg",
            "imageWidth": 3053,
            "imageHeight": 2035,
            "imageSize": 2027349,
            "views": 27041,
            "downloads": 18670,
            "collections": 110,
            "likes": 81,
            "comments": 12,
            "user_id": 88716,
            "user": "ptrabattoni",
            "userImageURL": "https://cdn.pixabay.com/user/2013/12/06/14-07-36-644_250x250.jpg"
        }
    ]
}
```
![](https://velog.velcdn.com/images/chojja7188/post/b7267986-45f2-4cc1-b083-b1146127912b/image.png)
