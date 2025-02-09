## 소개

COS 콘솔을 통해 객체의 이전 버전을 최신 버전으로 복원할 수 있습니다. 본 문서에서는 콘솔에서 버킷 객체의 이전 버전을 복원하는 방법을 설명합니다. 버전 관리에 대한 자세한 내용은 [버전 관리 개요](https://intl.cloud.tencent.com/document/product/436/19883)를 참고하십시오.

>? 
>- 객체 복원은 이전 버전을 최신 버전으로 복원하는 것을 말하며, 이전 버전은 그대로 보관됩니다.
>- 이전 버전을 삭제하려면 [버전 관리 설정](https://intl.cloud.tencent.com/document/product/436/19881), [객체 삭제](https://intl.cloud.tencent.com/document/product/436/13323)를 참고하시기 바랍니다.
>- 단일 객체 복원 작업을 지원하며, 일괄 복원은 지원되지 않습니다.
>


## 사용 수칙

다음은 복원된 객체의 적용 시나리오 및 규칙에 대한 설명입니다.

<table>
	<tr><th>적용 시나리오</th><td><ul  style="margin: 0;"><li>버전 관리가 활성화된 버킷은 객체 복원을 지원합니다. </li><li>버킷에 대해 버전 관리를 활성화한 다음 비활성화하면 객체 복원이 지원되지 않습니다. </li><li>버전 관리가 활성화된 적이 없는 버킷은 객체 복원을 지원하지 않습니다. </li></ul></td></tr>
	<tr><th>복원 규칙</th><td><ul  style="margin: 0;"><li>이전 버전: 복원이 가능합니다.</li><li>최신 버전: 복원할 수 없습니다.</li><li>삭제 표시가 있는 버전: 복원할 수 없습니다.</li></ul></td></tr>
</table>


## 전제 조건

객체를 복원하기 전에 버킷에 대한 버전 관리가 활성화 되어있어야 합니다. 활성화되어있지 않은 경우 [버전 관리 설정](https://intl.cloud.tencent.com/document/product/436/19881) 문서를 참고하여 활성화하시기 바랍니다.

## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 클릭합니다.
3. 객체가 속한 버킷을 찾아 해당 버킷 이름을 클릭합니다.
4. 왼쪽 사이드바에서 **파일 리스트**를 클릭합니다.
5. **버전 기록 조회**를 활성화하고 복원할 객체를 찾습니다. 오른쪽 작업 열에서 **복원**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/01cf0bbcee0fd999f6ef482516e3625a.png)
6. 파일 복원 팝업창에서 복원된 객체의 버전 정보를 확인합니다. 올바른지 확인한 후 **확인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9a2bdf5f5c15f0b6e1edb15dbd427c5b.png)
7. 이로써 객체 복원 작업이 완료됩니다. 파일 목록에서 버전이 성공적으로 복원되었음을 확인할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/11393ba7760f0ad8deffbc61acf7cd36.png)

