## 소개

Tencent Cloud COS는 악성 프로그램 URL에 의한 공용 네트워크 트래픽 도용이나 악의적 수단에 의한 리소스 도용으로 사용자가 불필요한 손해를 입지 않도록 링크 도용 방지 설정을 지원하고 있습니다. 보안을 위해 콘솔의 링크 도용 방지 설정 항목에서 블록리스트와 얼로우리스트를 설정할 것을 권장합니다.

>! 
> - 객체 액세스 시 서명(URL과 Header 모두 해당)이 있으면 링크 도용 방지 인증을 진행하지 않습니다.
> - 링크 도용 방지 설정 시, 대용량 파일 멀티파트 요청 시나리오에 대한 링크 도용 방지 얼로우리스트에 자신의 도메인을 추가할 수 있습니다.
> 

## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인 후 왼쪽 메뉴바에서 [버킷 리스트]를 클릭하여 버킷 리스트 페이지로 이동합니다.
2. 링크 도용 방지 설정이 필요한 버킷을 찾아 버킷 이름을 클릭하여 버킷 관리 페이지로 이동합니다.
3. [보안 관리] > [링크 도용 방지 설정]을 클릭하여 링크 도용 방지 설정을 찾고, [편집]을 클릭하여 편집이 가능한 상태로 이동합니다.
   ![](https://main.qcloudimg.com/raw/235d3158684e32b4b92daf0e81bd6db6.png)
4. 현재 상태를 활성화로 변경한 뒤 리스트 유형(블록리스트 또는 얼로우리스트)을 선택합니다. 대상 도메인의 설정이 완료되면 [저장]을 클릭합니다. 다음은 설정 항목에 관한 설명입니다.
 - **블록리스트**: 해당 리스트에 포함된 도메인이 버킷의 기본 액세스 주소에 액세스할 때 이를 **차단합니다.** 리스트 내 도메인이 버킷의 기본 액세스 주소로 액세스하면 403을 반환합니다.
 - **얼로우리스트**: 해당 리스트에 포함된 도메인이 버킷의 기본 액세스 주소에 액세스할 때 이를 **허용합니다.** 리스트에 없는 도메인이 버킷의 기본 액세스 주소로 액세스하면 403을 반환합니다.
 - **Null referer**: HTTP 요청 header가 null referer입니다(referer 필드를 포함하지 않거나 referer 필드가 null).
 - **Referer**: 최대 10개의 도메인을 설정할 수 있으며, 동일한 접두사로 매칭할 수 있습니다. 각 행은 한 줄만 허용되니, 한 줄을 초과할 경우 행을 바꾸십시오. 다음 예시와 같이 도메인, IP, 임의 문자 기호 `*` 등 형식의 주소를 지원합니다.
    - `www.example.com` 설정: `www.example.com/123`, `www.example.com.cn`과 같이 `www.example.com`을 접두사로 하는 주소를 제한할 수 있습니다.
    - `www.example.com:8080`, `10.10.10.10:8080` 등의 주소와 같이 포트가 있는 도메인과 IP를 지원합니다.
    - `*.example.com` 설정: `a.b.example.com/123`, `a.example.com` 등의 주소를 제한할 수 있습니다.
     ![](https://main.qcloudimg.com/raw/6a02d7abf3ec8630ca9a89959554e2cd.png)
		
>? CDN 도메인으로 가속 액세스할 경우, CDN의 링크 도용 방지 규칙이 우선적으로 실행된 뒤 COS의 링크 도용 방지 규칙이 실행됩니다.
>


## 예시

APPID가 1250000000인 사용자가 examplebucket-1250000000이라는 이름의 버킷을 생성하고, 루트 디렉터리에 picture.jpg 이미지 한 장을 넣은 경우, COS는 규칙에 따라 기본 액세스 주소 하나를 생성합니다.

```plaintext
examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

사용자 A가 보유한 웹 사이트:

```plaintext
www.example.com
```

해당 이미지를 초기 화면 index.html에 삽입합니다.

이때 웹마스터 B가 보유한 웹 사이트:

```plaintext
www.fake.com
```

웹마스터 B는 이 이미지를 `www.fake.com`로 옮기고 싶지만 트래픽 요금 발생을 원치 않아 다음 주소를 통해 picture.jpg를 인용한 뒤 `www.fake.com` 웹 사이트의 초기 화면 index.html로 옮겼습니다.

```plaintext
examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

위와 같은 경우, 사용자 A의 손해를 막기 위해 두 가지의 링크 도용 방지 수단을 활성화할 수 있습니다.

#### 활성화 방법 1

**블록리스트** 모드로 설정하여 도메인 설정에 `*.fake.com`을 입력한 뒤 저장 및 적용합니다.

#### 활성화 방법 2

**얼로우리스트** 모드로 설정하여 도메인 설정에 `*.example.com`을 입력한 뒤 저장 및 적용합니다.

#### 활성화 이전

`http://www.example.com/index.html` 액세스 시, 이미지가 정상적으로 표시됩니다.
`http://www.fake.com/index.html` 액세스 시, 이미지가 정상적으로 표시됩니다.

#### 활성화 이후

`http://www.example.com/index.html` 액세스 시, 이미지가 정상적으로 표시됩니다.
`http://www.fake.com/index.html` 액세스 시, 이미지가 표시되지 않습니다.

## 미니프로그램 관련 설명

1. 미니프로그램의 네트워크에서 요청한 referer의 형식은 `https://servicewechat.com/{appid}/{version}/page-frame.html`로 정해져 있습니다.
2. 버킷에 링크 도용 방지를 위한 조치를 취한 상태에서 미니프로그램의 COS 이미지 로딩을 허용하려면, [COS 콘솔](https://console.cloud.tencent.com/cos5)에서 `servicewechat.com`을 링크 도용 방지를 위한 얼로우리스트로 설정합니다.
