# pixabay open Api 한글번역
## **Pixabay API**
API를 사용하는 경우 검색 결과가 표시될 때마다 이미지와 비디오의 출처를 사용자에게 보여주세요. 이는 무료 API 사용에 대한 대가로 우리가 친절하게 요청하는 것 중 하나입니다.
PI는 JSON으로 인코딩된 객체를 반환합니다. 해시 키와 값은 대소문자를 구분하며 문자 인코딩은 UTF-8 입니다 . 해시 키는 임의의 순서로 반환될 수 있으며 언제든지 새 키가 추가될 수 있습니다. 결과에서 해시 키를 제거하거나 필수 매개변수를 추가하기 전에 사용자에게 알릴 수 있도록 최선을 다하겠습니다.

<br/>

## 요청한도
기본적으로 분당 최대 100개의 요청을 할 수 있습니다. 요청은 API 키와 연결되어 있으며 IP 주소와는 관련이 없습니다. 응답 헤더에는 현재 요청 한도 상태에 대한 모든 정보가 포함되어 있습니다.

<br/>

## 헤더 이름 설명
`X-RateLimit-Limit` :  소비자가 30분 동안 허용된 최대 요청 수입니다.
`X-RateLimit-Remaining` : 현재 요청 한도 창에 남아있는 요청 수입니다.
`X-RateLimit-Reset` : 현재 요청 한도 창이 재설정되는 남은 시간(초)입니다.

<br/>

## Hotlinking 핫링크
이미지의 영구적인 핫링크(앱에서 Pixabay URL 사용)는 허용되지 않습니다. 이미지를 사용할 경우 먼저 서버로 다운로드해야 합니다. 비디오는 애플리케이션에 직접 임베드될 수 있습니다. 그러나 서버에 저장하는 것이 좋습니다.

<br/>

## 오류처리
오류가 발생하면 적절한 HTTP 오류 상태 코드가 포함된 응답이 반환됩니다. 이 응답의 본문에는 문제에 대한 설명이 평문으로 포함됩니다. 예를 들어, 요청 한도를 초과하면 HTTP 오류 429("너무 많은 요청")가 반환되고 "API 요청 한도 초과"라는 메시지가 표시됩니다.

<br/>

# image Search
```
(get)
	https://pixabay.com/api/
```

| key (required) | str | Your API key:  | 귀하의 API  |
| --- | --- | --- | --- |
| q | str | A URL encoded search term. If omitted, all images are returned. This value may not exceed 100 characters.Example: "yellow+flower" | URL로 인코딩된 검색어입니다. 생략하면 모든 이미지가 반환됩니다. 이 값은 100자를 초과할 수 없습니다.예: "노란색+꽃" |
| lang | str | Language code of the language to be searched in.Accepted values: cs, da, de, en, es, fr, id, it, hu, nl, no, pl, pt, ro, sk, fi, sv, tr, vi, th, bg, ru, el, ja, ko, zhDefault: "en" | 검색할 언어의 언어 코드입니다. 허용되는 값: cs, da, de, en, es, fr, id, it, hu, nl, no, pl, pt, ro, sk, fi, sv, tr, vi , th, bg, ru, el, ja, ko, zh기본값: "en" |
| id | str | Retrieve individual images by ID. | ID별로 개별 이미지를 검색합니다. |
| image_type | str | Filter results by image type.Accepted values: "all", "photo", "illustration", "vector"Default: "all" | 이미지 유형별로 결과를 필터링합니다.허용되는 값: "모두", "사진", "그림", "벡터"기본값: "모두" |
| orientation | str | Whether an image is wider than it is tall, or taller than it is wide.Accepted values: "all", "horizontal", "vertical"Default: "all" | 이미지의 높이가 높이보다 넓은지, 아니면 너비보다 큰지 여부입니다.허용되는 값: "all", "horizontal", "vertical"기본값: "all" |
| category | str | Filter results by category.Accepted values: backgrounds, fashion, nature, science, education, feelings, health, people, religion, places, animals, industry, computer, food, sports, transportation, travel, buildings, business, music | 카테고리별로 결과를 필터링합니다.허용되는 값: 배경, 패션, 자연, 과학, 교육, 감정, 건강, 사람, 종교, 장소, 동물, 산업, 컴퓨터, 음식, 스포츠, 교통, 여행, 건물, 비즈니스, 음악 |
| min_width | int | Minimum image width.Default: "0" | 최소 이미지 너비.기본값: "0" |
| min_height | int | Minimum image height.Default: "0" | 최소 이미지 높이.기본값: "0" |
| colors | str | Filter images by color properties. A comma separated list of values may be used to select multiple properties.Accepted values: "grayscale", "transparent", "red", "orange", "yellow", "green", "turquoise", "blue", "lilac", "pink", "white", "gray", "black", "brown" | 색상 속성을 기준으로 이미지를 필터링합니다. 쉼표로 구분된 값 목록을 사용하여 여러 속성을 선택할 수 있습니다.허용되는 값: "회색조", "투명", "빨간색", "주황색", "노란색", "녹색", "청록색", "파란색", "라일락색", "분홍색", "흰색", "회색" , "검은색", "갈색" |
| editors_choice | bool | Select images that have received an Editor's Choice award.Accepted values: "true", "false"Default: "false" | Editor's Choice 상을 받은 이미지를 선택하세요 .허용되는 값: "true", "false"기본값: "false" |
| safesearch | bool | A flag indicating that only images suitable for all ages should be returned.Accepted values: "true", "false"Default: "false" | 모든 연령에 적합한 이미지만 반환해야 함을 나타내는 플래그입니다.허용되는 값: "true", "false"기본값: "false" |
| order | str | How the results should be ordered.Accepted values: "popular", "latest"Default: "popular" | 결과를 정렬하는 방법.허용되는 값: "인기", "최신"기본값: "인기" |
| page | int | Returned search results are paginated. Use this parameter to select the page number.Default: 1 | 반환된 검색 결과는 페이지가 매겨져 있습니다. 이 매개변수를 사용하여 페이지 번호를 선택합니다.기본값: 1 |
| per_page | int | Determine the number of results per page.Accepted values: 3 - 200Default: 20 | 페이지당 결과 수를 결정합니다.허용되는 값: 3 - 200기본값: 20 |
| callback | string | JSONP callback function name | JSONP 콜백 함수 이름 |
| pretty | bool | Indent JSON output. This option should not be used in production.Accepted values: "true", "false"Default: "false" | JSON 출력을 들여쓰기합니다. 이 옵션은 프로덕션에서 사용하면 안 됩니다.허용되는 값: "true", "false"기본값: "false" |

<br/>

## parameter
| Response key | Description |  |
| --- | --- | --- |
| total | The total number of hits. | 총 히트 수 |
| totalHits | The number of images accessible through the API. By default, the API is limited to return a maximum of 500 images per query. | API를 통해 액세스할 수 있는 이미지 수입니다. 기본적으로 API는 쿼리당 최대 500개의 이미지를 반환하도록 제한됩니다. |
| id | A unique identifier for this image. | 이 이미지의 고유 식별자입니다. |
| pageURL | Source page on Pixabay, which provides a download link for the original image of the dimension imageWidth x imageHeight and the file size imageSize. | Pixabay의 소스 페이지는 imageWidth x imageHeight 크기와 파일 크기 imageSize의 원본 이미지에 대한 다운로드 링크를 제공합니다. |
| previewURL | Low resolution images with a maximum width or height of 150 px (previewWidth x previewHeight). | 최대 너비 또는 높이가 150픽셀(previewWidth x PreviewHeight)인 저해상도 이미지. |
| webformatURL | Medium sized image with a maximum width or height of 640 px (webformatWidth x webformatHeight). URL valid for 24 hours.Replace '_640' in any webformatURL value to access other image sizes:Replace with '_180' or '_340' to get a 180 or 340 px tall version of the image, respectively. Replace with '_960' to get the image in a maximum dimension of 960 x 720 px. | 최대 너비 또는 높이가 640px(webformatWidth x webformatHeight)인 중간 크기 이미지입니다. 24시간 동안 유효한 URL입니다. 다른 이미지 크기에 액세스하려면 webformatURL 값에서 '_640'을 바꾸세요.이미지의 높이가 각각 180px 또는 340px인 버전을 얻으려면 '_180' 또는 '_340'으로 바꾸세요. 최대 크기 960 x 720픽셀의 이미지를 얻으려면 '_960'으로 바꾸세요. |
| largeImageURL | Scaled image with a maximum width/height of 1280px. | 최대 너비/높이가 1280px인 크기가 조정된 이미지입니다. |
| views | Total number of views. | 총 조회수입니다. |
| downloads | Total number of downloads. | 총 다운로드 수입니다. |
| likes | Total number of likes. | 총 좋아요 수입니다. |
| comments | Total number of comments. | 총 댓글 수입니다. |
| user_id, user | User ID and name of the contributor. Profile URL: https://pixabay.com/users/{ USERNAME }-{ ID }/ | 사용자 ID 및 기여자의 이름입니다. 프로필 URL: https://pixabay.com/users/{ 사용자 이름 }-{ ID }/ |
| userImageURL | Profile picture URL (250 x 250 px). | 프로필 사진 URL(250x250픽셀). |

<br/>

```
💡 The following response key/value pairs are only available if your account has been [approved for full API access](https://pixabay.com/api/docs/#).
These URLs give you access to the original images in full resolution and - if available - in vector format:
다음 응답 키/값 쌍은 귀하의 계정이 [전체 API 액세스에 대해 승인](https://pixabay.com/api/docs/#) 된 경우에만 사용할 수 있습니다  이 URL을 사용하면 전체 해상도 및 가능한 경우 벡터 형식의 원본 이미지에 액세스할 수 있습니다.
```

| response key | Description | 설명 |
| --- | --- | --- |
| fullHDURL | Full HD scaled image with a maximum width/height of 1920px. | 최대 너비/높이가 1920px인 풀 HD 크기의 이미지입니다. |
| imageURL | URL to the original image (imageWidth x imageHeight). | 원본 이미지의 URL(imageWidth x imageHeight) |
| vectorURL | URL to a vector resource if available, else omitted. | 사용 가능한 경우 벡터 리소스에 대한 URL이고, 그렇지 않으면 생략됩니다. |

<br/>

# Search Video
```
(get)
		https://pixabay.com/api/videos/
```

| key (required) | str | Your API key:  | 귀하의 API 키: |
| --- | --- | --- | --- |
| q | str | A URL encoded search term. If omitted, all images are returned. This value may not exceed 100 characters.Example: "yellow+flower" | URL로 인코딩된 검색어입니다. 생략하면 모든 동영상이 반환됩니다. 이 값은 100자를 초과할 수 없습니다.예: "노란색+꽃" |
| lang | str | Language code of the language to be searched in.Accepted values: cs, da, de, en, es, fr, id, it, hu, nl, no, pl, pt, ro, sk, fi, sv, tr, vi, th, bg, ru, el, ja, ko, zhDefault: "en" | 검색할 언어의 언어 코드입니다. 허용되는 값: cs, da, de, en, es, fr, id, it, hu, nl, no, pl, pt, ro, sk, fi, sv, tr, vi , th, bg, ru, el, ja, ko, zh기본값: "en" |
| id | str | Retrieve individual images by ID. | ID별로 개별 동영상을 검색합니다. |
| image_type | str | Filter results by image type.Accepted values: "all", "photo", "illustration", "vector"Default: "all" | 비디오 유형별로 결과를 필터링합니다.허용되는 값: "all", "film", "animation"기본값: "all" |
| orientation | str | Whether an image is wider than it is tall, or taller than it is wide.Accepted values: "all", "horizontal", "vertical"Default: "all" | 카테고리별로 결과를 필터링합니다.허용되는 값: 배경, 패션, 자연, 과학, 교육, 감정, 건강, 사람, 종교, 장소, 동물, 산업, 컴퓨터, 음식, 스포츠, 교통, 여행, 건물, 비즈니스, 음악 |
| category | str | Filter results by category.Accepted values: backgrounds, fashion, nature, science, education, feelings, health, people, religion, places, animals, industry, computer, food, sports, transportation, travel, buildings, business, music | 최소 비디오 너비.기본값: "0" |
| min_width | int | Minimum image width.Default: "0" | 최소 비디오 높이.기본값: "0" |
| min_height | int | Minimum image height.Default: "0" | Editor's Choice 상을 받은 동영상을 선택하세요 .허용되는 값: "true", "false"기본값: "false" |
| colors | str | Filter images by color properties. A comma separated list of values may be used to select multiple properties.Accepted values: "grayscale", "transparent", "red", "orange", "yellow", "green", "turquoise", "blue", "lilac", "pink", "white", "gray", "black", "brown" | 모든 연령에 적합한 동영상만 반환해야 함을 나타내는 플래그입니다.허용되는 값: "true", "false"기본값: "false" |
| editors_choice | bool | Select images that have received an Editor's Choice award.Accepted values: "true", "false"Default: "false" | 결과를 정렬하는 방법.허용되는 값: "인기", "최신"기본값: "인기" |
| safesearch | bool | A flag indicating that only images suitable for all ages should be returned.Accepted values: "true", "false"Default: "false" | 반환된 검색 결과는 페이지가 매겨져 있습니다. 이 매개변수를 사용하여 페이지 번호를 선택합니다.기본값: 1 |
| order | str | How the results should be ordered.Accepted values: "popular", "latest"Default: "popular" | 페이지당 결과 수를 결정합니다.허용되는 값: 3 - 200기본값: 20 |
| page | int | Returned search results are paginated. Use this parameter to select the page number.Default: 1 | JSONP 콜백 함수 이름 |
| per_page | int | Determine the number of results per page.Accepted values: 3 - 200Default: 20 | JSON 출력을 들여쓰기합니다. 이 옵션은 프로덕션에서 사용하면 안 됩니다.허용되는 값: "true", "false"기본값: "false" |
| callback | string | JSONP callback function name |  |
| pretty | bool | Indent JSON output. This option should not be used in production.Accepted values: "true", "false"Default: "false" |  |

<br/>

## parameter
| Response key | Description |  |
| --- | --- | --- |
| total | The total number of hits. | 총 히트 수입니다. |
| totalHits | The number of videos accessible through the API. By default, the API is limited to return a maximum of 500 videos per query. | API를 통해 액세스할 수 있는 동영상 수입니다. 기본적으로 API는 쿼리당 최대 500개의 비디오를 반환하도록 제한됩니다. |
| id | A unique identifier for this video. | 이 동영상의 고유 식별자입니다. |
| pageURL | Source page on Pixabay. | Pixabay의 소스 페이지. |
| videos | A set of differently sizes video streams:large usually has a dimension of 3840x2160. If a large video version is not available, an empty URL value and a size of zero is returned.medium usually has a dimension of 1920x1080, older videos have a dimension of 1280x720. This size is available for all Pixabay videos.small typically has a dimension of 1280x720, older videos have a dimension of 960x540. This size is available for all videos.tiny typically has a dimension of 960x540, older videos have a dimension of 640x360. This size is available for all videos.Object keyDescriptionurlThe video URL. Append the GET parameter download=1 to the value to have the browser download it.widthThe width of the video and thumbnail.heightThe height of the video and thumbnail.sizeThe approximate size of the video in bytes.thumbnailThe URL of the poster image for this rendition. | 다양한 크기의 비디오 스트림 세트:large일반적으로 크기는 3840x2160입니다. 큰 비디오 버전을 사용할 수 없는 경우 빈 URL 값과 0 크기가 반환됩니다. medium일반적으로 크기는 1920x1080이고 이전 비디오의 크기는 1280x720입니다. 이 크기는 모든 Pixabay 비디오에 사용할 수 있습니다. small일반적으로 크기는 1280x720이고 이전 비디오의 크기는 960x540입니다. 이 크기는 모든 비디오에 사용할 수 있습니다. tiny일반적으로 크기는 960x540이고 이전 비디오의 크기는 640x360입니다. 이 크기는 모든 비디오에 사용할 수 있습니다. 객체 키설명URL동영상 URL입니다. 브라우저가 해당 값을 다운로드하도록 하려면 GET 매개변수를 download=1값에 추가하세요. 너비비디오 및 썸네일의 너비입니다.키동영상 및 미리보기 이미지의 높이입니다.크기비디오의 대략적인 크기(바이트)입니다.미리보기 이미지 변환의 포스터 이미지 URL입니다. |
| url | The video URL. Append the GET parameter download=1 to the value to have the browser download it. | 동영상 URL입니다. 브라우저가 해당 값을 다운로드하도록 하려면 GET 매개변수를 download=1값에 추가하세요. |
| width | The width of the video and thumbnail. | 비디오 및 썸네일의 너비입니다. |
| height | The height of the video and thumbnail. | 동영상 및 미리보기 이미지의 높이입니다. |
| size | The approximate size of the video in bytes. | 비디오의 대략적인 크기(바이트)입니다. |
| thumbnail | The URL of the poster image for this rendition. | 이 변환의 포스터 이미지 URL입니다. |
| views | Total number of views. | 총 조회수입니다. |
| downloads | Total number of downloads. | 총 다운로드 수입니다. |
| likes | Total number of likes. | 총 좋아요 수입니다. |
| comments | Total number of comments. | 총 댓글 수입니다. |
| user_id, user | User ID and name of the contributor. Profile URL: https://pixabay.com/users/{ USERNAME }-{ ID }/ | 사용자 ID 및 기여자의 이름입니다. 프로필 URL: https://pixabay.com/users/{ 사용자 이름 }-{ ID }/ |
| userImageURL | Profile picture URL (250 x 250 px). | 프로필 사진 URL(250x250픽셀). |

