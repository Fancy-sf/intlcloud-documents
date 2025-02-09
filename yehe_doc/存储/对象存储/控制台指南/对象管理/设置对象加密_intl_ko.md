## 소개

Cloud Object Storage(COS) 콘솔에서 버킷에 저장된 객체를 암호화하여 데이터 유출을 방지할 수 있습니다. 암호화에 대한 자세한 내용은 [서버 측 암호화 개요](https://intl.cloud.tencent.com/document/product/436/18145)를 참고하십시오. 다음은 객체 암호화를 구성하는 방법을 보여줍니다.

>!
> - 이 작업은 아카이브 유형의 객체 암호화 설정은 지원하지 않습니다. 암호화가 필요할 경우 먼저 객체 [복구 작업](https://intl.cloud.tencent.com/document/product/436/30961)을 진행하고 복구 완료 후 암호화를 구성하기 전에 저장소 유형을 스탠다드 스토리지 또는 스탠다드IA 스토리지로 수정하십시오.
> - 객체에 대한 액세스 권한이 있는 한 객체의 암호화 여부에 관계없이 객체 액세스 환경은 동일합니다.
> - 서버 암호화는 객체 데이터 암호화만 지원하며 객체 메타데이터 암호화는 지원하지 않습니다. 서버로 암호화한 객체의 경우에는 반드시 익명 사용자가 아닌 유효한 서명으로 액세스해야 합니다.
> - 버킷의 객체를 나열하면 암호화 여부에 관계없이 모든 객체가 나열됩니다.
> 

## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 클릭합니다.
3. 객체가 속한 버킷을 찾아 해당 버킷 이름을 클릭합니다.
4. 왼쪽 사이드바에서 **파일 리스트**를 클릭합니다.
5. 대상 객체를 찾고 오른쪽의 작업 열에서 **세부 정보**를 클릭합니다.
![](https://main.qcloudimg.com/raw/05c7a0e867badbd56242b93f6425561d.png)
6. ‘서버 측 암호화’ 열에서 대상 암호화 방법을 선택합니다.

다음 두 가지 암호화 방법이 현재 지원됩니다.
 - SSE-COS: COS에서 관리하는 키를 통한 서버 측 암호화 방식입니다. SSE-COS 암호화에 대한 자세한 내용은 [서버 암호화 개요: SSE-COS](https://intl.cloud.tencent.com/document/product/436/18145#sse-cos-.E5.8A.A0.E5.AF.86)를 참고하십시오.
 - SSE-KMS: Tencent Cloud Key Management System(KMS)에서 관리하는 키로 서버 측 암호화입니다. 기본 키를 사용하거나 키를 생성할 수 있습니다. 키에 대한 자세한 내용은 [키 생성](https://intl.cloud.tencent.com/document/product/1030/31971)을 참고하십시오. SSE-KMS에 대한 자세한 내용은 [서버 측 암호화 개요](https://intl.cloud.tencent.com/document/product/436/18145#sse-kms-.E5.8A.A0.E5.AF.86)의 SSE-KMS 암호화 섹션을 참고하십시오.
7. **저장**을 클릭합니다.
>!
> - SSE-KMS 암호화를 처음 사용한다면 [KMS 서비스 활성화](https://buy.cloud.tencent.com/kms)가 필요합니다.
> - 현재 SSE-KMS 암호화는 베이징, 상하이, 광저우 리전에서만 지원합니다.
> 
여러 객체를 일괄 암호화하려면 여러 객체를 선택하고 상단의 **추가 작업 > 암호화 방법 수정**을 클릭합니다.



