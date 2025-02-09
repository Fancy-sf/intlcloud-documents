Content Delivery Network(CDN)을 사용하여 Cloud Object Storage(COS) 버킷에 저장된 콘텐츠를 대량 다운로드/전송할 수 있으며, 이는 동일한 콘텐츠를 반복적으로 다운로드해야 하는 경우에 이상적입니다. Origin-pull 인증 기능을 통해 CDN은 개인 읽기 버킷에 저장된 콘텐츠를 가속화할 수 있습니다. CDN 인증 기능은 데이터 보안 위험과 불필요한 트래픽 비용 발생을 방지하기 위해 승인된 사용자만 콘텐츠를 다운로드할 수 있습니다.


>?사용자가 CDN 가속 도메인 이름을 활성화한 후 CDN 가속 도메인 이름을 사용하여 데이터를 다운로드하고 액세스하면 CDN Origin-pull 트래픽과 CDN 트래픽이 생성됩니다. 자세한 내용은 [COS가 CDN 원본 서버로 작용할 때 발생하는 트래픽](https://intl.cloud.tencent.com/document/product/436/33776)을 참고하십시오.


## CDN

#### CDN의 정의

CDN은 전 세계에 분산된 고성능 엣지 노드로 구성된 Internet 에코시스템 레이어입니다. 이러한 노드는 캐시 정책에 따라 콘텐츠를 저장합니다. 사용자가 콘텐츠를 요청하면 액세스 속도를 높이고 가용성을 향상시키기 위해 요청이 사용자와 가장 가까운 엣지 노드로 라우팅됩니다.

CDN에는 캐시 및 Origin-pull이 포함됩니다. 사용자가 URL에 액세스할 때 요청한 콘텐츠가 엣지 노드에 캐시되지 않았거나 캐시된 콘텐츠가 만료된 경우 해당 콘텐츠를 원본에서 가져옵니다.

#### 적용 시나리오

- 응답 지연 및 다운로드 속도에 대한 요구 사항이 높은 시나리오.
- 지역, 국가, 대륙 간 GB ~ TB 용량의 데이터를 전송하는 시나리오
- 같은 콘텐츠를 짧은 시간에 반복적으로 다운로드하는 시나리오.

#### 보안 유형

- Origin-pull 인증: 요청한 콘텐츠가 엣지 노드에 캐시되지 않은 경우 콘텐츠를 원본에서 가져옵니다. COS가 원본으로 사용되고 Origin-pull 인증이 활성화된 경우 CDN 엣지 노드는 특수 서비스 ID를 사용하여 COS 원본에 액세스하여 프라이빗 버킷의 데이터를 획득하고 캐시합니다.
 - CDN 서비스 인증: CDN 엣지 노드가 특수 서비스 ID를 사용하여 COS 원본에 액세스하고 콘텐츠를 가져올 수 있도록 CDN 서비스를 인증할 수 있습니다.
- CDN 인증: 사용자가 엣지 노드에 액세스하여 캐시 데이터를 획득하면 엣지 노드는 인증 구성 규칙에 따라 액세스 URL의 인증 필드를 확인합니다. 이를 통해 무단 액세스 및 링크 도용을 방지하여 엣지 노드에 캐시된 데이터의 보안과 안정성을 향상시킵니다.

## COS 액세스 노드

#### 액세스 노드의 정의

액세스 노드는 버킷의 리전 및 이름에 따라 버킷에 할당되는 도메인 이름입니다. 이 도메인 이름을 사용하여 버킷에 저장된 데이터에 액세스할 수 있습니다.

정적 웹사이트 기능이 활성화되면 기본 액세스 노드와 다른 응답을 구성할 수 있는 정적 웹사이트 액세스 노드가 제공됩니다.

#### 액세스 노드

- 액세스 노드: 버킷이 생성되면 COS는 RESTful API를 사용하여 액세스할 수 있는 &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com 형식의 XML 액세스 노드를 버킷에 할당합니다. 노드에 액세스하고 [API 문서](https://intl.cloud.tencent.com/document/product/436/7751)를 참고하여 버킷을 구성하거나 객체를 업로드/다운로드할 수 있습니다.
- 정적 웹 사이트 노드: 콘솔의 버킷에 대한 기본 구성 페이지에서 정적 웹 사이트 기능을 활성화할 수 있습니다. 그런 다음 &lt;BucketName-APPID>.cos-website.&lt;Region>.myqcloud.com 형식의 액세스 노드가 제공됩니다. 객체 다운로드만 허용하는 정적 웹 사이트에 대한 특수 인덱스 페이지(IndexPage), 오류 페이지(ErrorPage) 및 리디렉션을 구성할 수 있습니다. 사용자는 정적 웹 사이트 도메인 이름을 사용하여 콘텐츠를 얻을 수 있습니다.

#### 액세스 권한

- 공개 읽기: 버킷이 공개 읽기로 설정되어 있으면 누구나 해당 도메인 이름을 사용하여 버킷에 액세스할 수 있습니다. 공개 읽기 버킷을 원본으로 사용하는 경우 CDN 인증 및 Origin-pull 인증을 활성화하지 않고도 CDN 가속을 직접 활성화할 수 있습니다.
- 개인 읽기: 버킷이 개인 읽기로 설정된 경우 액세스 정책을 생성하여 버킷에 액세스할 수 있는 사람을 관리하고 CDN 권한 부여를 관리할 수 있습니다. 개인 읽기 버킷을 원본으로 사용하고 Origin-pull 인증을 활성화하지만 CDN 인증은 활성화하지 않으면 권한이 없는 사용자가 CDN을 통해 버킷에 액세스할 수 있습니다. 따라서 **데이터 보안을 보장하기 위해 개인 읽기 버킷에 대해 Origin-pull 인증과 CDN 인증을 모두 활성화하는 것이 좋습니다**.

## CDN을 사용하여 COS 액세스 가속화

다음 두 도메인 이름을 관리하여 COS에 대한 액세스를 가속화할 수 있습니다.

- 기본 CDN 가속 도메인 이름: COS에서 제공하는 기본 CDN 가속 도메인 이름(예: &lt;BucketName-APPID>.file.mycloud.com)으로 필요에 따라 활성화 또는 비활성화할 수 있습니다.
- 사용자 정의 CDN 가속 도메인 이름: ICP 비안이 완료된 사용자 정의 도메인 이름을 사용하고 COS 버킷을 원본으로 사용할 수 있습니다. 이를 통해 사용자 정의 도메인 이름을 사용하여 버킷의 객체에 대한 액세스를 가속화할 수 있습니다.

>? 기본 CDN 가속 도메인 이름과 사용자 정의 CDN 가속 도메인 이름을 총칭하여 CDN 가속 도메인이라고 합니다.

#### 공개 읽기 버킷

버킷이 공개 읽기로 설정되고 COS가 CDN 풀링의 원본으로 사용되는 경우 Origin-pull 인증을 활성화할 필요가 없으며 CDN 엣지 노드는 COS 버킷에 저장된 객체를 가져와 캐시할 수 있습니다.

CDN 콘솔에서 [인증 설정](https://intl.cloud.tencent.com/document/product/228/35237)을 활성화하여 버킷의 객체를 **어느 정도** 보호할 수 있습니다. 이 기능의 활성화 여부에 관계없이 버킷 액세스 도메인 이름을 아는 사용자는 버킷의 모든 객체에 액세스할 수 있습니다. 사용자가 다양한 CDN 인증 구성에서 공개 읽기 버킷에 액세스할 수 있는지 여부는 다음 표에 설명되어 있습니다.

| CDN 인증 | CDN 가속 도메인 이름으로 액세스 | COS 도메인 이름으로 액세스 | 사용 사례                                        |
| ------------ | ---------------- | ------------ | ----------------------------------------------- |
| 비활성화(디폴트) | 액세스 가능           | 액세스 가능       | CDN 또는 원본을 통해 전체 웹사이트에 대한 모든 공개 액세스 허용       |
| 활성화         | URL 인증 필요  | 액세스 가능       | 원본이 아닌 CDN을 통한 액세스에 대해 링크 도용 방지 활성화(권장하지 않음) |

#### 개인 읽기 버킷

버킷이 개인 읽기(기본값)로 설정되고 COS가 CDN 풀링의 원본으로 사용되는 경우 CDN 엣지 노드는 **객체를 가져오고 캐시할 수 없습니다**. 따라서 버킷 정책(Bucket Policy)에 CDN 서비스 ID를 추가하고 ID에 다음 작업을 수행할 수 있는 권한을 부여해야 합니다.

- GET Object: 객체 다운로드
- HEAD Object: 객체 메타데이터 쿼리
- OPTIONS Object: CORS 실행 전 요청 구성

**CDN 서비스 인증 추가**를 클릭하면 [CDN 콘솔](https://console.cloud.tencent.com/cdn) 또는 [COS 콘솔](https://console.cloud.tencent.com/cos5)에서 클릭 한 번으로 ID를 인증할 수 있습니다. 그런 다음 「Origin-pull 인증」을 활성화합니다. 이러한 방식으로 CDN 엣지 노드는 서비스 ID를 사용하여 COS 객체에 액세스할 수 있습니다.

>!
> 1. 버킷이 개인 읽기로 설정된 경우 CDN 서비스 권한 부여를 추가하고 origin-pull 인증을 활성화해야 합니다. 그렇지 않으면 COS에 대한 액세스가 거부됩니다.
> 2. CDN 엣지 노드는 각 루트 계정에 대한 서비스 계정을 생성합니다. 따라서 계정 인증은 가속 도메인 이름이 속한 루트 계정에 대해서만 유효합니다. 가속 도메인 이름이 다른 계정에 바인딩된 경우 액세스가 거부됩니다.

CDN 서비스 권한 부여를 추가하고 Origin-pull 인증을 활성화하면 CDN 엣지 노드가 데이터를 가져와 캐시할 수 있습니다. 따라서 버킷에 저장된 개인 데이터를 보호해야 하는 경우 [인증 설정](https://intl.cloud.tencent.com/document/product/228/35237)을 활성화하는 것이 좋습니다. 다양한 CDN 인증 구성에 대한 개인 읽기 버킷 액세스 가능 여부는 다음 표에 설명되어 있습니다.

| CDN 인증 | CDN 가속 도메인 이름으로 액세스 | COS 도메인 이름으로 액세스 | 사용 사례                                        |
| ------------ | ---------------- | --------------- | ----------------------------------- |
| 비활성화(디폴트) | 액세스 가능           | COS 인증 필요 | 원본의 콘텐츠를 보호하기 위해 CDN 도메인 이름에 대한 직접 액세스 허용   |
| 활성화         | URL 인증 필요  | COS 인증 필요 | 포괄적인 액세스 보안(CDN 인증을 위한 링크 도용 방지 지원) |

