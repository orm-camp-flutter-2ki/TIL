240401 (Mon)

플러터 과정 21일차

#### 메모
mapper 만들때 형변환에 주의
num의 경우는 Json을 확인해서 정확한 형태로 변환 시켜주고 Nullable로 만들기

equatable은 4종세트

**freezed** 는 serializabel  + equatable 느낌

클래스 6종을 생성 해준다.

boilerplate 맨날 쓰는 코드

enum은 클래스 만큼 자유롭지 않다

sealed class 서브타입을 봉인한다.

패턴 매칭을 활용하여 모든 서브 타입에 대한 처리를 하기 용이하다.

result패턴은 형태가 일정하지 않다.

sealed class Result<D, E> 면 D는 데이터, E는 에러

error로 string으로 해도 되고, exception도 된다.

enum값도 줄수 있다.


# 문제 1번 pixabayApi 공부 메모
### 비율 제한

기본적으로 분당 100개의 요청을 할 수 있다. 요청은 ip주소가 아닌 api 키를 활용해 연결한다.

| 헤더 이름  | 설명 |
| --- | --- |
| X-RateLimit-Limit | 소비자가 30분 동안 만들수 있는 최대 요청 수 |
| X-RateLimit-Remaining | 현재 비율 제한 창에 남은 요청 수 |
| X-RateLimit-Reset | 현재 속도 제한 창이 재설정된 후 남은 시간(초)입니다. |

대량 다운로드는 허용하지 않는다.

API를 올바르게 구현했으면 언제든 한도를 늘릴  수 있다.

### 핫링크

반환된 이미지 URL은 일시적으로 검색 결과를 표시하는 데 사용될 수 있습니다. 그러나 이미지의 영구적인 핫링크는 허용되지 않는다. 이미지를 사용하려면 먼저 서버에 다운로드하세요. 비디오는 애플리케이션에 직접 삽입될 수 있습니다. 그러나 서버에 저장하는 것이 좋습니다.

### 오류 처리

오류가 발생하면 적절한 HTTP 오류 상태 코드가 포함된 응답이 반환됩니다. 이 응답 본문에는 문제에 대한 일반 텍스트 설명이 포함되어 있습니다. 예를 들어, 속도 제한을 초과하면 "API 속도 제한 초과"(”API rate limit exceeded”)메시지와 함께 HTTP error 429("Too Many Requests")를 받게 됩니다.

### Search Image

**http://picabay.com/api/**

### parameters

| key (required) | str | Your API key: 43171013-2e645214e257431880726c2d5 |  |
| --- | --- | --- | --- |
| q | str | A URL encoded search term. If omitted, all images are returned. This value may not exceed 100 characters.Example: "yellow+flower" | URL로 인코딩된 검색어입니다. 생략하면 모든 이미지가 반환됩니다. 이 값은 100자를 초과할 수 없습니다.예: "노란색+꽃” |
| lang | str | Language code of the language to be searched in.Accepted values: cs, da, de, en, es, fr, id, it, hu, nl, no, pl, pt, ro, sk, fi, sv, tr, vi, th, bg, ru, el, ja, ko, zhDefault: "en" | 검색할 언어의 언어 코드입니다. 허용되는 값: cs, da, de, en, es, fr, id, it, hu, nl, no, pl, pt, ro, sk, fi, sv, tr, vi , th, bg, ru, el, ja, ko, zh 기본값: "en” |
| id | str | Retrieve individual images by ID. | ID별로 개별 이미지를 검색합니다. |
| image_type | str | Filter results by image type.Accepted values: "all", "photo", "illustration", "vector"Default: "all" | 이미지 유형별로 결과를 필터링합니다. 허용되는 값: "모두", "사진", "그림", "벡터" 
기본값: "모두” |
| orientation | str | Whether an image is wider than it is tall, or taller than it is wide.Accepted values: "all", "horizontal", "vertical"Default: "all" | 이미지의 너비가 높이보다 큰지, 너비보다 큰지 여부입니다. 허용되는 값: "all", "horizontal", "vertical" 기본값: "all” |
| category | str | Filter results by category.Accepted values: backgrounds, fashion, nature, science, education, feelings, health, people, religion, places, animals, industry, computer, food, sports, transportation, travel, buildings, business, music | 카테고리별로 결과를 필터링합니다. 허용되는 값: 배경, 패션, 자연, 과학, 교육, 감정, 건강, 사람, 종교, 장소, 동물, 산업, 컴퓨터, 음식, 스포츠, 교통, 여행, 건물, 비즈니스, 음악 |
| min_width | int | Minimum image width.Default: "0" | 최소 이미지 너비. 기본값: "0” |
| min_height | int | Minimum image height.Default: "0" | 최소 이미지 높이. 기본값: "0” |
| colors | str | Filter images by color properties. A comma separated list of values may be used to select multiple properties.Accepted values: "grayscale", "transparent", "red", "orange", "yellow", "green", "turquoise", "blue", "lilac", "pink", "white", "gray", "black", "brown" | 색상 속성을 기준으로 이미지를 필터링합니다. 쉼표로 구분된 값 목록을 사용하여 여러 속성을 선택할 수 있습니다. 허용되는 값: "회색조", "투명", "빨간색", "주황색", "노란색", "녹색", "청록색", "파란색", " 라일락", "핑크", "화이트", "그레이", "블랙", "브라운” |
| editors_choice | bool | Select images that have received an Editor's Choice award.Accepted values: "true", "false"Default: "false" | Editor's Choice 상을 받은 이미지를 선택하세요. 허용되는 값: 'true', 'false' 
기본값: 'false’ |
| safesearch | bool | A flag indicating that only images suitable for all ages should be returned.Accepted values: "true", "false"Default: "false" | 모든 연령에 적합한 이미지만 반환해야 함을 나타내는 플래그입니다. 허용 값: "true", "false" 기본값: "false” |
| order | str | How the results should be ordered.Accepted values: "popular", "latest"Default: "popular" | 결과 정렬 방법.허용 값: "인기", "최신" 기본값: "인기” |
| page | int | Returned search results are paginated. Use this parameter to select the page number.Default: 1 | 반환된 검색 결과는 페이지가 매겨져 있습니다. 이 매개변수를 사용하여 페이지 번호를 선택합니다. 기본값: 1 |
| per_page | int | Determine the number of results per page.Accepted values: 3 - 200Default: 20 | 페이지당 결과 수를 결정합니다.허용 값: 3 - 200 기본값: 20 |
| callback | string | JSONP callback function name | JSONP 콜백 함수 이름 |
| pretty | bool | Indent JSON output. This option should not be used in production.Accepted values: "true", "false"Default: "false" | JSON 출력을 들여쓰기합니다. 이 옵션은 프로덕션에서 사용하면 안 됩니다. 허용되는 값: "true", "false"기본값: "false” |

## example

| Response key | Description |  |
| --- | --- | --- |
| total | The total number of hits. | 총 히트 수입니다. |
| totalHits | The number of images accessible through the API. By default, the API is limited to return a maximum of 500 images per query. | API를 통해 액세스할 수 있는 이미지 수입니다. 기본적으로 API는 쿼리당 최대 500개의 이미지를 반환하도록 제한됩니다. |
| id | A unique identifier for this image. | 이 이미지의 고유 식별자입니다. |
| pageURL | Source page on Pixabay, which provides a download link for the original image of the dimension imageWidth x imageHeight and the file size imageSize. | Pixabay의 소스 페이지는 imageWidth x imageHeight 크기와 파일 크기 imageSize의 원본 이미지에 대한 다운로드 링크를 제공합니다. |
| previewURL | Low resolution images with a maximum width or height of 150 px (previewWidth x previewHeight). | 최대 너비 또는 높이가 150픽셀(previewWidth x PreviewHeight)인 저해상도 이미지. |
| webformatURL | Medium sized image with a maximum width or height of 640 px (webformatWidth x webformatHeight). URL valid for 24 hours.Replace '_640' in any webformatURL value to access other image sizes:Replace with '_180' or '_340' to get a 180 or 340 px tall version of the image, respectively. Replace with '_960' to get the image in a maximum dimension of 960 x 720 px. | 최대 너비 또는 높이가 640px(webformatWidth x webformatHeight)인 중간 크기 이미지입니다. 24시간 동안 유효한 URL입니다.다른 이미지 크기에 액세스하려면 webformatURL 값에서 '_640'을 바꾸세요. 이미지의 높이가 각각 180px 또는 340px인 버전을 얻으려면 '_180' 또는 '_340'으로 바꾸세요. 최대 크기 960 x 720픽셀의 이미지를 얻으려면 '_960'으로 바꾸세요. |
| largeImageURL | Scaled image with a maximum width/height of 1280px. | 최대 너비/높이가 1280px인 크기가 조정된 이미지입니다. |
| views | Total number of views. | 총 조회수입니다. |
| downloads | Total number of downloads. | 총 다운로드 수입니다. |
| likes | Total number of likes. | 총 좋아요 수입니다. |
| comments | Total number of comments. | 총 댓글 수입니다. |
| user_id, user | User ID and name of the contributor. Profile URL: https://pixabay.com/users/{ USERNAME }-{ ID }/ | 사용자 ID 및 기여자의 이름입니다. 프로필 URL: https://pixabay.com/users/{ 사용자 이름 }-{ ID }/ |
| userImageURL | Profile picture URL (250 x 250 px). | 프로필 사진 URL(250x250픽셀). |

## **Search Videos**

GEThttps://pixabay.com/api/videos/

### **Parameters**

| key (required) | str | Your API key: 43171013-2e645214e257431880726c2d5 | 귀하의 API 키:43171013-2e645214e257431880726c2d5 |
| --- | --- | --- | --- |
| q | str | A URL encoded search term. If omitted, all videos are returned. This value may not exceed 100 characters.Example: "yellow+flower" | URL로 인코딩된 검색어입니다. 생략하면 모든 동영상이 반환됩니다. 이 값은 100자를 초과할 수 없습니다. 예: "노란색+꽃" |
| lang | str | https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes of the language to be searched in.Accepted values: cs, da, de, en, es, fr, id, it, hu, nl, no, pl, pt, ro, sk, fi, sv, tr, vi, th, bg, ru, el, ja, ko, zhDefault: "en" | 검색할 언어의 https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes. 허용되는 값: cs, da, de, en, es, fr, id, it, hu, nl, no, pl, pt, ro, sk, fi, sv, tr, vi , th, bg, ru, el, ja, ko, zh 기본값: "en" |
| id | str | Retrieve individual videos by ID. | ID별로 개별 동영상을 검색합니다. |
| video_type | str | Filter results by video type.Accepted values: "all", "film", "animation"Default: "all" | 비디오 유형별로 결과를 필터링합니다.허용되는 값: "all", "film", "animation" 기본값: "all" |
| category | str | Filter results by category.Accepted values: backgrounds, fashion, nature, science, education, feelings, health, people, religion, places, animals, industry, computer, food, sports, transportation, travel, buildings, business, music | 카테고리 별로 결과를 필터링합니다.허용되는 값: 배경, 패션, 자연, 과학, 교육, 감정, 건강, 사람, 종교, 장소, 동물, 산업, 컴퓨터, 음식, 스포츠, 교통, 여행, 건물, 비즈니스, 음악 |
| min_width | int | Minimum video width.Default: "0" | 최소 비디오 너비. 기본값: "0" |
| min_height | int | Minimum video height.Default: "0" | 최소 비디오 높이. 기본값: "0" |
| editors_choice | bool | Select videos that have received an https://pixabay.com/editors_choice/ award.Accepted values: "true", "false"Default: "false" | https://pixabay.com/editors_choice/ 상을 받은 동영상을 선택하세요 .허용되는 값: "true", "false" 기본값: "false" |
| safesearch | bool | A flag indicating that only videos suitable for all ages should be returned.Accepted values: "true", "false"Default: "false" | 모든 연령에 적합한 동영상만 반환해야 함을 나타내는 플래그입니다.허용되는 값: "true", "false" 기본값: "false" |
| order | str | How the results should be ordered.Accepted values: "popular", "latest"Default: "popular" | 결과를 정렬하는 방법.허용되는 값: "인기", "최신" 기본값: "인기" |
| page | int | Returned search results are paginated. Use this parameter to select the page number.Default: 1 | 반환된 검색 결과는 페이지가 매겨져 있습니다. 이 매개변수를 사용하여 페이지 번호를 선택합니다. 기본값: 1 |
| per_page | int | Determine the number of results per page.Accepted values: 3 - 200Default: 20 | 페이지당 결과 수를 결정합니다.허용되는 값: 3 - 200 기본값: 20 |
| callback | string | JSONP callback function name | JSONP 콜백 함수 이름 |
| pretty | bool | Indent JSON output. This option should not be used in production.Accepted values: "true", "false"Default: "false" | JSON 출력을 들여쓰기합니다. 이 옵션은 프로덕션에서 사용하면 안 됩니다.허용되는 값: "true", "false" 기본값: "false" |

### **Example**

Retrieving videos about "yellow flowers". The search term q needs to be URL encoded.

[https://pixabay.com/api/videos/?key=43171013-2e645214e257431880726c2d5&q=yellow+flowers](https://pixabay.com/api/videos/?key=43171013-2e645214e257431880726c2d5&q=yellow+flowers&pretty=true)

| Response key | Description |  |
| --- | --- | --- |
| total | The total number of hits. | 총 히트 수입니다. |
| totalHits | The number of videos accessible through the API. By default, the API is limited to return a maximum of 500 videos per query. | API를 통해 액세스할 수 있는 동영상 수입니다. 기본적으로 API는 쿼리당 최대 500개의 비디오를 반환하도록 제한됩니다. |
| id | A unique identifier for this video. | 이 동영상의 고유 식별자입니다. |
| pageURL | Source page on Pixabay. | Pixabay의 소스 페이지. |
| videos | A set of differently sizes video streams:
• large usually has a dimension of 3840x2160. If a large video version is not available, an empty URL value and a size of zero is returned.|
|• medium usually has a dimension of 1920x1080, older videos have a dimension of 1280x720. This size is available for all Pixabay videos.|
|• small typically has a dimension of 1280x720, older videos have a dimension of 960x540. This size is available for all videos.|
|• tiny typically has a dimension of 960x540, older videos have a dimension of 640x360. This size is available for all videos.Object keyDescriptionurlThe video URL. Append the GET parameter download=1 to the value to have the browser download it.widthThe width of the video and thumbnail.heightThe height of the video and thumbnail.sizeThe approximate size of the video in bytes.thumbnailThe URL of the poster image for this rendition. | 다양한 크기의 비디오 스트림 세트:
• large일반적으로 크기는 3840x2160입니다. 큰 비디오 버전을 사용할 수 없는 경우 빈 URL 값과 0 크기가 반환됩니다.|
|• medium일반적으로 크기는 1920x1080이고 이전 비디오의 크기는 1280x720입니다. 이 크기는 모든 Pixabay 비디오에 사용할 수 있습니다.
|• small일반적으로 크기는 1280x720이고 이전 비디오의 크기는 960x540입니다. 이 크기는 모든 비디오에 사용할 수 있습니다.|
|• tiny일반적으로 크기는 960x540이고 이전 비디오의 크기는 640x360입니다. 이 크기는 모든 비디오에 사용할 수 있습니다.객체 키설명URL동영상 URL입니다. 브라우저가 해당 값을 다운로드하도록 하려면 GET 매개변수를 download=1값에 추가하세요.너비비디오 및 썸네일의 너비입니다.키동영상 및 미리보기 이미지의 높이입니다.크기비디오의 대략적인 크기(바이트)입니다.미리보기 이미지이 변환의 포스터 이미지 URL입니다. |
| views | Total number of views. | 총 조회수입니다. |
| downloads | Total number of downloads. | 총 다운로드 수입니다. |
| likes | Total number of likes. | 총 좋아요 수입니다. |
| comments | Total number of comments. | 총 댓글 수입니다. |
| user_id, user | User ID and name of the contributor. Profile URL: https://pixabay.com/users/{ USERNAME }-{ ID }/ | 사용자 ID 및 기여자의 이름입니다. 프로필 URL: https://pixabay.com/users/{ 사용자 이름 }-{ ID }/ |
| userImageURL | Profile picture URL (250 x 250 px). | 프로필 사진 URL(250x250픽셀). |

이미지를 사용할때 http://pixabay.com/api/?{Api_key}&{key}&{key}

이런 식으로 사용한다.

이미지 하나를 검색할 때는 id에 값을 넣어준다.

이미지 타입 없이 검색하면 모든 이미지 종류중 하나로 랜덤으

예)

[](https://pixabay.com/api/?key=43171013-2e645214e257431880726c2d5&q=dance+couple&image_type=photo)

동영상의 경우에는 http://pixabay.com/api/videos/?{Api_key}&{key}&{key}

이런 식을 사용한다.
