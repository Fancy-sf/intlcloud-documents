## 소개

COS 콘솔을 이용해 버킷을 정적 웹 사이트 호스팅으로 설정하고, 버킷의 액세스 도메인으로 정적 웹 사이트에 액세스할 수 있습니다. 정적 웹사이트에 대한 자세한 내용은 [정적 웹 사이트 호스팅](https://intl.cloud.tencent.com/document/product/436/30958)을 참조하십시오.

>!
>- 버킷을 사용해 정적 웹 사이트를 호스팅하는 경우, 먼저 버킷의 액세스 권한을 **공개 읽기 및 개인 쓰기**로 설정해야 합니다.
>- 정적 웹 사이트 설정을 활성화하면 정적 웹사이트 도메인을 사용해 COS 원본 서버에 액세스해야 합니다. COS 기본 도메인을 사용해 액세스하는 경우 정적 웹 사이트 효과가 적용되지 않습니다.
>

## 전제 조건

생성된 버킷에 대한 자세한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309) 문서를 참고하십시오.

## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 클릭합니다.
3. 정적 웹사이트를 호스팅할 버킷을 찾아 버킷의 이름을 클릭하여 버킷 상세 페이지로 이동합니다.
4. 왼쪽 사이드바에서 **권한 관리 > 버킷 ACL(액세스 제어 목록)**을 클릭합니다. 그 다음 공용 권한에 대해 **공개 읽기/개인 쓰기**를 선택하고 저장을 클릭합니다.
![](https://main.qcloudimg.com/raw/460f2cdd71d3a21a74911a52218e7670.png)
5. 왼쪽 사이드바에서 **기본 구성 > 정적 웹 사이트**를 선택합니다. 정적 웹 사이트 열에서 **편집**을 클릭하고 **상태** 스위치를 켭니다.
6. 구성 항목을 설정합니다.
![](https://main.qcloudimg.com/raw/e7365ffd7beca545f275ec36cdaa8cce.png)
설정은 다음 내용을 참고하십시오.
 - **강제 HTTPS(옵션)**: 강제 HTTPS를 활성화하면 사용자가 정적 웹 사이트에 액세스할 때 정적 웹 사이트의 액세스 노드에서 강제로 HTTPS 프로토콜을 사용해 액세스합니다.
>! 사용자 정의 도메인으로 정적 웹 사이트에 액세스하고 정적 웹 사이트에 강제 HTTPS가 활성화되어 있는 경우, 해당 사용자 정의 도메인에 관련 인증서가 올바르게 설정되어 있는지 확인하십시오. 인증서에 이상이 있는 경우 기본 도메인으로 리디렉션되어 액세스됩니다.
>
 - **html 확장명 무시(옵션)**: 액세스 경로가 index인 경우, index.html 객체를 자동 매칭하여 반환합니다.
 - **인덱스 문서(필수)**: 정적 웹 사이트의 첫 페이지인 인덱스 문서는 사용자가 웹 페이지의 루트 디렉터리 또는 서브 디렉터리에 요청을 보낼 때 반환되는 웹 페이지로, 일반적으로 index.html로 이름이 생성됩니다.
>! 버킷에 폴더를 생성하면 폴더 계층별로 인덱스 문서를 추가해야 합니다.
>
 - **오류 문서(옵션)**: 오류 문서는 정적 웹 사이트로 액세스할 때 오류 발생 시 반환되는 페이지입니다. 해당 설정 항목으로 오류 문서를 직접 정의할 수 있습니다. 정적 웹 사이트가 사용자의 요청에 응답하지 못할 때, 지정한 사용자 정의 오류 페이지를 반환하게 됩니다. 예를 들어 이름이 error.html인 오류 문서를 설정한 경우, 액세스 시 HTTP 에러가 발생하면 페이지에서 error.html 페이지를 반환하여 도움말 가이드를 제공합니다. 오류 문서를 설정하지 않은 경우, 액세스 시 HTTP 에러가 발생하면 기본으로 설정된 오류 정보를 반환합니다.
>! 오류 문서 설정 시 버킷의 루트 디렉터리 또는 서브 디렉터리의 파일을 지원합니다. 브라우저에서 식별 가능한 `.html` 또는 `.htm` 등 포맷 파일을 사용하십시오. `.zip` 파일과 같이 브라우저에서 식별하지 못하는 파일을 사용하는 경우, 대부분의 브라우저에서 오류 정보에 액세스할 수 없거나 액세스 요청이 거부되었다는 정보가 표시됩니다.
>
 - **오류 문서 응답 코드**: 오류 문서를 설정한 경우 해당 항목이 표시됩니다. 오류 문서 반환 시의 HTTP 응답 코드를 기존 에러 코드 또는 200으로 설정할 수 있습니다.
 - **리디렉션 규칙(옵션)**: 리디렉션 규칙을 적용하면 특정한 파일 경로나 요청 시 포함된 접두사 및 응답 코드를 통해 조건에 따라 리디렉션을 요청할 수 있습니다.
예를 들어, 버킷에 있는 파일을 삭제하거나 이름을 변경한 경우 리디렉션 규칙을 추가하여 해당 파일에 대한 액세스 요청을 다른 파일로 리디렉션할 수 있습니다.
    - 에러 코드: 현재 리디렉션 규칙은 `4xx` 에러 코드(예: 404)에만 적용됩니다. 선택적으로 오류 페이지를 사용자 정의하여 해당 HTTP 오류가 트리거된 경우, 해당 오류 페이지에 기타 가이드를 제공할 수 있습니다.
    - 접두사 매칭: 접두사 매칭 규칙을 사용해 버킷에 있는 파일 또는 폴더에 리디렉션을 설정할 수 있습니다. 자세한 예시는 [리디렉션 규칙 예시](https://intl.cloud.tencent.com/document/product/436/30958#.E9.87.8D.E5.AE.9A.E5.90.91.E8.A7.84.E5.88.99)를 참조하십시오.
7. 구성 완료 후 **저장**을 클릭합니다.