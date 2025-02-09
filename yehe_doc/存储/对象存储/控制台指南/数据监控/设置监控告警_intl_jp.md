## 概要

Basic Cloud Monitorのアラートポリシーから、COS監視指標の閾値アラートを設定できます。アラートポリシーは、名前、ポリシータイプ、アラートトリガー条件、アラートオブジェクト、アラート通知テンプレートという5つの必要な部分によって構成されています。次のガイドラインに基づいて、COSアラートポリシーを作成することができます。

>?Tencent CloudのBCMは、クラウド製品のリソースのリアルタイム監視とアラートに対するサービスです。ユーザーは、BCMからCOSの監視指標に対するアラートルールの設定、アラート履歴の確認、アラート通知の受信を行うことができます。詳細については、[Tencent Cloud BCMアラートポリシー](https://intl.cloud.tencent.com/document/product/248/38916)をご参照ください。

## 操作手順

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインし、コンソールの概要ページで【アラートの設定】項目を見つけて、【アラートポリシーの設定】をクリックします。
>?また、バケットの概要ページでも【アラートの設定】を見つけることができます。
2.ジャンプインターフェースで【新規作成】をクリックし、アラートポリシーの設定を開始します。設定に関する説明は次のとおりです。
![](https://main.qcloudimg.com/raw/b8340b9590b8204ab082f28c096417e2.png)
<table>
  <tr>
    <th>設定タイプ</th>
    <th width="18%">設定項目</th>
    <th>説明</th>
  </tr>
  <tr>
    <td  rowspan="5">基本情報</td>
    <td>ポリシー名</td>
    <td>カスタムポリシー名です。</td>
  </tr>
  <tr>
    <td>備考</td>
    <td>カスタムポリシーの備考です。</td>
  </tr>
  <tr>
    <td>監視タイプ</td>
    <td>クラウド製品の監視を選択します。</td>
  </tr>
  <tr>
    <td>ポリシータイプ</td>
    <td>COSを選択します。</td>
  </tr>
  <tr>
    <td>ポリシーが属するプロジェクト</td>
    <td>ポリシーが属するプロジェクトには、次の2つの機能があります。<br>   
         <ul>
             <li>アラートポリシーを管理します。所属するプロジェクトを設定すると、アラートポリシーリストのプロジェクトにあるアラートポリシーをすぐにフィルタリングできます。</li>
             <li>インスタンスを管理します。必要に応じてプロジェクトを選択すると、アラートオブジェクトのプロジェクトにあるインスタンスをすぐに選択することができます。ビジネスタイプに基づいて、クラウド製品をそれぞれのプロジェクトに割り当てることができます。プロジェクトを作成するには、プロジェクト管理をご参照ください。プロジェクトを作成すると、各クラウド製品のコンソールで、各クラウド製品のリソースに、プロジェクトを割り当てることができます。一部のクラウド製品はプロジェクトの割り当てをサポートしていませんので、プロジェクトの権限が無い場合は、<a href="https://intl.cloud.tencent.com/document/product/248/36744">Cloud Access Management</a> をご参照のうえ、権限を付与して下さい。</li></td>   
  </tr>
  <tr>
    <td rowspan="3">アラートルールの設定</td>
    <td>アラートオブジェクト</td>
    <td>
      <ul>
			         <li>インスタンスIDを選択した場合、アラートを追加したいバケットを選択します。</li>
               <li>インスタンスグループを選択した場合、そのアラートポリシーは、ユーザーが選択したインスタンスグループにバインドされます。グループがない場合は、インスタンスグループの新規作成をクリックして、バケットに新しいグループを追加し、もう一度選択します。</li>
		            <li>すべてのオブジェクトを選択した場合、そのアラートポリシーは、現在のアカウントに権限があるすべてのバケットにバインドされます。</li>
           </ul>
        </td>
  </tr>
	<tr>
    <td>テンプレートの選択</td>
    <td> テンプレートボタンを選択し、ドロップダウンリストから設定済みのテンプレートを選択します。具体的な設定については、<a href="https://intl.cloud.tencent.com/document/product/248/38911">トリガー条件テンプレートの設定</a>をご参照ください。新規作成したテンプレートが表示されない場合は、右側の【更新】をクリックすると、トリガーするアラートテンプレートの選択リストが更新されます。</td>
  </tr>
	<tr>
    <td>手動設定<br>（インジケータアラート）</td>
    <td>
      <ul>
        <li>アラートトリガー条件：指標、比較関係、閾値、統計サイクル、持続サイクルから構成されるセマンティックの条件です。チャート上の指標のトレンドに応じて、アラートの閾値を設定することができます。<br>例えば、指標を標準ストレージの読み取りリクエスト、比較関係を> 、閾値を80回、統計サイクルを5分、持続サイクルを2サイクルとします。<br>これは、標準ストレージの読み取りリクエストデータが5分ごとに収集され、あるバケットの標準ストレージの読み取りリクエストが2回連続して80回を超えると、アラートがトリガーされることを意味します。
				<br><li>アラート頻度：アラートルールごとに、繰り返し通知ポリシーを設定できます。すなわち、アラートが発生した時に、そのアラートが特定の頻度で繰り返し通知されるように定義できます。<br>繰り返しなし、5分、10分、周期的指数関数的な増加…などの繰り返し頻度から選択することができます。<br><ul><li type="square">周期的指数関数的な増加とは、そのアラートが、1回、2回、4回、8回…という2のN乗回でトリガーされた場合に、アラート情報をユーザーに向けて送信することを意味しています。つまり、アラート情報の送信間隔を長くしていくほど、アラートの繰り返しによる煩わしさをある程度回避できます。</li>
      <li>繰り返しアラートのデフォルトロジック：アラートが発生してから24時間以内に、繰り返し通知用に設定した頻度に基づき、繰り返しアラート通知が送信されます。アラート発生からまるまる24時間が経過すると、1日1回アラート通知が送信されるようになります。</li></ul></li>
      </ul></td>
  </tr>
   <tr>
        <td>アラート通知の設定</td>
        <td>アラート通知</td>
        <td>システムプリセット通知テンプレートとユーザーカスタム通知テンプレートの選択がサポートされます。各アラートポリシーは、最大で3つの通知テンプレートにのみバインドできます。詳細については、<a href="https://cloud.tencent.com/document/product/248/50394">通知テンプレート</a>をご参照ください。</td>
    </tr>
		<tr>
      <td>高度な設定</td>
      <td>自動スケーリング</td>
      <td>有効にして正常に設定されると、アラート条件に達した場合、自動スケーリングがトリガーされ、容量が縮小または拡張されます。</td>
     </tr>
</table>

3. 上記の情報を設定し、【保存】をクリックすれば、COSアラートポリシーの作成は完了です。
