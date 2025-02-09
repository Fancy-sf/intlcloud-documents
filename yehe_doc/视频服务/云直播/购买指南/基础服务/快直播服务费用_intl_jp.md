## 注意事項
- 課金方式：**日次決済、料金後払い**。
- 課金周期：1日単位で請求します。毎日のトラフィック料金は翌日の請求書発行時に差し引かれます。詳細な請求と請求時間については請求書をご覧ください。
- **グローバル/中国香港・中国マカオ・中国台湾リージョンのエリア説明**：
  - アジア太平洋地域リージョン1：中国香港、シンガポール、中国マカオ、ベトナム、タイ、ネパール、カンボジア、パキスタン。
  - アジア太平洋地域リージョン2：中国台湾、日本 、マレーシア、インドネシア、韓国。
  - アジア太平洋地域リージョン3：フィリピン、インド、オーストラリア。
  - 北アメリカ：アメリカ、カナダ、メキシコ。
  - ヨーロッパ：オランダ、ドイツ、ロシア、イギリス、アイルランド、イタリア、スペイン、フランス。
  - 中東：アラブ首長国連邦、トルコ、カタール、サウジアラビア、バーレーン、イラク。
  - アフリカ：南アフリカ。
  - 南アメリカ：ブラジル、コロンビア、アルゼンチン。
- トラフィック/帯域幅の変換単位は1000です。例えば、1TB = 1000GBとなります。
- CSSは、北京時間の00:00から23:59までを1暦日としてカウントします。
- ライブイベントストリーミングは超低遅延リンクを採用しているため、トラフィック/帯域幅料金は標準ライブストリーミングより若干高くなります。
- ユーザーがライブイベントストリーミングを使用する際、正常に再生するにはCSSストリームのBフレームを削除する必要があります。プッシュされたCSSストリームがBフレームを含む場合は、システムがデフォルトでトランスコードによってBフレームを削除します。これにより別途CSSトランスコード料金が発生します。
- Web端末のブラウザプルが標準WebRTCプロトコルのみサポートし、AACオーディオ形式をサポートしていない場合は、プッシュされたAACオーディオ形式をOPUSオーディオ形式に変換して再生する必要があります。これによりオーディオトランスコード料金が発生します。
- Tencent Cloud CSSは、**2022年1月4日0時**より、ライブイベントストリーミングの基本機能サービスの日次決済見積価格と価格勾配を調整しています。これに伴い、グローバル/中国香港・中国マカオ・中国台湾の消費価格は一元課金からリージョン別課金に変更され、それぞれのリージョンに応じた価格設定が行われるようになります。詳細な調整のお知らせについては、[価格調整のお知らせ](https://intl.cloud.tencent.com/document/product/267/43055)をご参照ください。

>! 
>- デフォルトでは、ダウンストリーム再生のみ課金され、アップストリームとダウンストリームの使用が不均衡な業務シーン（ダウンストリーム再生：アップストリームプッシュ < 10:1）の場合、1日のプッシュのピーク帯域幅が100Mbpsを超えると、実際のプッシュ使用量に応じて追加のプッシュ料金が課金されます。
>
>- アップストリームプッシュと[標準ライブストリーミングのダウンストリーム再生](https://intl.cloud.tencent.com/document/product/267/2818)の**課金方式、公表価格および課金エリア（中国本土/中国本土以外）は同じであり**、使用量がある段階に達すると独立して課金されます。**アップストリームプッシュ課金は2021年7月1日0時から開始しています**。
>
>- 課金の例：
>
>  **ライブイベントストリーミングのアジア太平洋地域リージョン1の日次トラフィック課金を例にすると**、ダウンストリーム再生トラフィックが9GB、アップストリームプッシュトラフィックが1GB、プッシュの1日のピーク帯域幅が101Mbpsの場合、再生：プッシュ = 9:1 < 10:1であり、かつプッシュの1日のピーク帯域幅が100Mbpsを超えていることから、ライブストリーミングトラフィックの請求額は次のようになります。
>
> 1日のトラフィックライブストリーミング料金 = アップストリームトラフィック料金 + ダウンストリームトラフィック料金 = 0.1496（米ドル/GB）×（9（GB）+ 1 （GB））= 1.496米ドル。



[](id:overseas)
## グローバル/中国香港・中国マカオ・中国台湾のアクセラレーション

ライブイベントストリーミングのグローバル/中国香港・中国マカオ・中国台湾のトラフィックと帯域幅の統計データは、ユーザーがグローバル/中国香港・中国マカオ・中国台湾の各リージョンのアクセラレーションオリジンサーバーとの間で接続を確立することによって発生したダウンストリームトラフィック・帯域幅のデータです。日次決済の料金後払いの課金方式としては、[トラフィック課金](#overseas_flow)と[帯域幅課金](#overseas_bandwidth)という2種類が提供されており、新規ユーザーがライブストリーミングをアクティブにした場合、デフォルトでトラフィック課金が適用されます。

>! ライブイベントストリーミングのグローバル/中国香港・中国マカオ・中国台湾のトラフィックと帯域幅課金は、2021年4月20日から本格的な課金がスタートし、2021年4月21日からこの課金ルールに従って請求が行われます。

[](id:overseas_flow)
### グローバル/中国香港・中国マカオ・中国台湾のトラフィック課金

#### 課金価格
ライブイベントストリーミングのグローバル/中国香港・中国マカオ・中国台湾のトラフィック課金では、リージョンごとに1日の到達量による従量課金が適用されます。各リージョンの日次決済のトラフィック課金の段階的価格の詳細については、次の表のとおりです。

<table>
<thead>
<tr>
<th rowspan=2>トラフィック段階</th>
<th colspan=8 style="text-align:center;">各リージョンの価格(米ドル/GB/日)</th>
</tr>
<tr>
<th>アジア太平洋地域リージョン1</th>
<th>アジア太平洋地域リージョン2</th>
<th>アジア太平洋地域リージョン3</th>
<th>北アメリカ</th>
<th>ヨーロッパ</th>
<th>中東</th>
<th>アフリカ</th>
<th>南アメリカ</th>
</tr>
</thead>
<tbody>
<tr>
<td>0 - 2TB</td>
<td>0.1496</td>
<td>0.2472</td>
<td>0.2276</td>
<td>0.1431</td>
<td>0.1431</td>
<td>0.3902</td>
<td>0.3902</td>
<td>0.3350</td>
</th>
<tr>
<td>2TB（2TBを含む）～ 50TB</td>
<td>0.1398</td>
<td>0.2276</td>
<td>0.2081</td>
<td>0.1268</td>
<td>0.1268</td>
<td>0.3577</td>
<td>0.3577</td>
<td>0.3187</td>
</tr>
<tr>
<td>50TB（50TBを含む）～ 100TB</td>
<td>0.1171</td>
<td>0.2114</td>
<td>0.1821</td>
<td>0.1008</td>
<td>0.1008</td>
<td>0.3350</td>
<td>0.3350</td>
<td>0.2927</td>
</tr>
<tr>
<td>100TB（100TBを含む）～ 1PB</td>
<td>0.1008</td>
<td>0.1821</td>
<td>0.1626</td>
<td>0.0650</td>
<td>0.0650</td>
<td>0.3089</td>
<td>0.3089</td>
<td>0.2764</td>
</tr>
<tr>
<td>≥ 1PB</td>
<td>0.0911</td>
<td>0.1691</td>
<td>0.1431</td>
<td>0.0520</td>
<td>0.0520</td>
<td>0.2764</td>
<td>0.2764</td>
<td>0.2602</td>
</tr>
</tbody></table>

#### 課金説明
- 課金項目：ライブイベントストリーミング視聴によって発生したグローバル/中国香港・中国マカオ・中国台湾におけるネットワーク全体のダウンストリームトラフィック。
- 課金ルール：到達段階に応じて日次決済で課金されます。1暦日の各リージョンのトラフィック累計値に対応する段階の単価を乗じて算出します。

#### 課金の例
- ライブストリーミングのビットレートが500kbps（このビットレートはオーディオビットレートとビデオビットレートの合計ですが、トランスコーディングをオンにして特定のビットレートを設定している場合、この設定値はビデオのみのビットレートとなり、オーディオビットレートを加えてトラフィックを計算する必要があります）、ライブストリーミング時間が1時間、視聴者数が100人となる場合、消費されるトラフィックは、およそ500/8 × 3600 × 100 = 22500000KB = 22.5GBとなります。
- 2022年1月4日にライブイベントストリーミングのグローバル/中国香港・中国マカオ・中国台湾サービスを利用し、中国香港で22.5GBのダウンストリームトラフィックが発生した場合、2022年1月5日に支払うべきライブストリーミングトラフィックの請求額は、次のようになります。
  1日あたりのライブストリーミングトラフィック料金は、0.1496（米ドル/GB） × 22.5(GB) = 3.366米ドルとなります。
- デフォルトでは、ダウンストリーム再生のみ課金され、アップストリームとダウンストリームの使用が不均衡な業務シーン（ダウンストリーム再生：アップストリームプッシュ < 10:1）の場合、1日のプッシュのピーク帯域幅が100Mbpsを超えると、実際のプッシュ使用量に応じて追加のプッシュ料金が課金されます。アップストリームプッシュはダウンストリーム再生の課金方式、公表価格と同じであり、使用量がある段階に達すると個別に課金されます。

[](id:overseas_bandwidth)

### グローバル/中国香港・中国マカオ・中国台湾の帯域幅課金
#### 課金価格
ライブイベントストリーミングのグローバル/中国香港・中国マカオ・中国台湾の帯域幅課金では、リージョンごとに到達段階に応じて日次決済で課金されます。当日のグローバル/中国香港・中国マカオ・中国台湾の各リージョンのピーク帯域幅を課金値とします。各リージョンの日次決済のピーク帯域幅課金の段階的価格は、次の表のとおりです。

<table>
<thead>
<tr>
<th rowspan=2>帯域幅段階</th>
<th colspan=8 style="text-align:center;">各リージョンの価格(米ドル/Mbps/日)</th>
</tr>
<tr>
<th>アジア太平洋地域リージョン1</th>
<th>アジア太平洋地域リージョン2</th>
<th>アジア太平洋地域リージョン3</th>
<th>北アメリカ</th>
<th>ヨーロッパ</th>
<th>中東</th>
<th>アフリカ</th>
<th>南アメリカ</th>
</tr>
</thead>
<tbody>
<tr>
<td>0 - 500Mbps</td>
<td>0.4098</td>
<td>1.2033</td>
<td>1.2455</td>
<td>0.3967</td>
<td>0.3967</td>
<td>1.8667</td>
<td>1.8667</td>
<td>1.6911</td>
</tr>
<tr>
<td>500Mbps（500Mbpsを含む）～ 5Gbps</td>
<td>0.3707</td>
<td>1.0829</td>
<td>1.2098</td>
<td>0.3610</td>
<td>0.3610</td>
<td>1.8407</td>
<td>1.8407</td>
<td>1.6553</td>
</tr>
<tr>
<td>5Gbps（5Gbpsを含む）～ 20Gbps</td>
<td>0.3415</td>
<td>0.9659</td>
<td>1.1122</td>
<td>0.3363</td>
<td>0.3363</td>
<td>1.8016</td>
<td>1.8016</td>
<td>1.6130</td>
</tr>
<tr>
<td>≥ 20Gbps</td>
<td>0.3252</td>
<td>0.8455</td>
<td>1.0081</td>
<td>0.3187</td>
<td>0.3187</td>
<td>1.7821</td>
<td>1.7821</td>
<td>1.5935</td>
</tr>
</tbody></table>

#### 課金説明

- 課金項目：ライブイベントストリーミング視聴によって発生したグローバル/中国香港・中国マカオ・中国台湾におけるネットワーク全体のダウンストリーム帯域幅。
- 課金ルール：到達段階に応じて日次決済で課金されます。1暦日の各リージョンの帯域幅ピーク値に対応する段階の単価を乗じて算出します。

#### 課金の例
-  ライブストリーミングのビットレートが500kbps（このビットレートはオーディオビットレートとビデオビットレートの和となりますが、トランスコーディングを有効にして特定のビットレートを設定している場合、この設定値がビデオのみのビットレートとなりますので、オーディオビットレートを加えて帯域幅を計算する必要があります）、当日の同時視聴者数が最大100人の場合、1日の帯域幅ピーク値は次のようになります。
500（kbps） × 100 = 50000（kbps） = 50Mbps。
-  2022年1月4日にライブイベントストリーミングのグローバル/中国香港・中国マカオ・中国台湾サービスを利用し、中国マカオで50Mbpsのダウンストリーム帯域幅が発生した場合、2022年1月5日に支払うべきライブストリーミング帯域幅の請求額は次のとおりです。
   1日あたりのライブストリーミング帯域幅の料金 = 0.4098（米ドル/Mbps/日） × 50（Mbps） = 20.49米ドル。
-  デフォルトでは、ダウンストリーム再生のみ課金され、アップストリームとダウンストリームの使用が不均衡な業務シーン（ダウンストリーム再生：アップストリームプッシュ < 10:1）の場合、1日のプッシュのピーク帯域幅が100Mbpsを超えると、実際のプッシュ使用量に応じて追加のプッシュ料金が課金されます。アップストリームプッシュはダウンストリーム再生の課金方式、公表価格と同じであり、使用量がある段階に達すると個別に課金されます。

[](id:domestic)

## トラフィック帯域幅

ライブストリーミングのトラフィック/帯域幅料金は、Tencent Cloudライブイベントストリーミングの基本的な課金項目ですが、これは、ライブイベントストリーミングサービスによってライブストリーミングコンテンツを視聴するときに発生するダウンストリームのトラフィック/帯域幅の料金のことです。
日次決済、料金後払いの課金方式として、[トラフィック課金](#flow) と[帯域幅課金](#bandwidth)の2つの課金方式を提供しています。ユーザーは実際のニーズに応じて、自分に適した課金方式を選択できます。**新規ユーザーがライブイベントストリーミングをアクティブにした場合、デフォルトでトラフィック課金が適用されます**。

[](id:flow)

### トラフィック課金

#### 課金価格

ライブイベントストリーミングのトラフィック課金では、毎日の料金を段階的に設定する従量課金制が適用されます。日次決済トラフィック課金の段階的価格の詳細については、次のとおりです。

| トラフィック段階          | 価格（米ドル/GB/日） |
| ----------------- | ---------------- |
| 0 - 2TB           | 0.0846           |
| 2TB（2TBを含む）～10TB   | 0.0813           |
| 10TB（10TBを含む）～50TB  | 0.0780           |
| 50TB（50TBを含む）～100TB | 0.0715           |
| 100TB（100TBを含む）～1PB  | 0.0618           |
| ≥ 1PB             | 0.0520           |

#### 課金説明

- 課金項目：ライブイベントストリーミング視聴によって発生した中国本土（大陸）におけるネットワーク全体のダウンストリームトラフィック。
- 課金ルール：到達段階に応じて日次決済で課金されます。1暦日のトラフィック累計値に対応する段階の単価を乗じて算出します。

#### 課金の例

- ライブストリーミングのビットレートが500kbps（このビットレートはオーディオビットレートとビデオビットレートの合計ですが、トランスコーディングをオンにして特定のビットレートを設定している場合、この設定値はビデオのみのビットレートとなり、オーディオビットレートを加えてトラフィックを計算する必要があります）、ライブストリーミング時間が1時間、視聴者数が100人となる場合、消費されるトラフィックは、およそ500/8 x 3600 x 100 = 22500000KB = 22.5GBとなります。
- 2022年1月4日にライブイベントストリーミングサービスを利用し、22.5GBのダウンストリームトラフィックが発生した場合、2022年1月5日に支払うべきライブストリーミングトラフィックの請求額は、次のようになります。
  1日あたりのライブストリーミングトラフィック料金は、0.0846（米ドル/GB） × 22.5(GB) = 1.9035米ドルとなります。
- デフォルトでは、ダウンストリーム再生のみ課金され、アップストリームとダウンストリームの使用が不均衡な業務シーン（ダウンストリーム再生：アップストリームプッシュ < 10:1）の場合、1日のプッシュのピーク帯域幅が100Mbpsを超えると、実際のプッシュ使用量に応じて追加のプッシュ料金が課金されます。アップストリームプッシュはダウンストリーム再生の課金方式、公表価格と同じであり、使用量がある段階に達すると個別に課金されます。

[](id:bandwidth)

### 帯域幅課金

#### 課金価格

ライブイベントストリーミングの帯域幅課金では、1日の到達量による従量課金が適用され、その日のピーク帯域幅が課金値となります。日次決済のピーク帯域幅課金の段階的価格の詳細については、次の表のとおりです。

|帯域幅段階             | 価格（米ドル/Mbps/日） |
| -------------------- | ------------------ |
| 0 - 500Mbps          | 0.2114             |
| 500Mbps（500Mbpsを含む）～5Gbps | 0.2049             |
| 5Gbps（5Gbpsを含む）～20Gbps  | 0.1984             |
| ≥ 20Gbps             | 0.1886             |

#### 課金説明

- 課金項目：ライブイベントストリーミング視聴で発生する中国内地（大陸）のネットワーク全体のダウンストリーム帯域幅。
- 課金ルール：到達段階に応じて日次決済で課金されます。1暦日の帯域幅ピーク値に対応する段階の単価を乗じて算出します。

#### 課金の例

-  ライブストリーミングのビットレートが500kbps（このビットレートはオーディオビットレートとビデオビットレートの和となりますが、トランスコーディングを有効にして特定のビットレートを設定している場合、この設定値がビデオのみのビットレートとなりますので、オーディオビットレートを加えて帯域幅を計算する必要があります）、当日の同時視聴者数が最大100人の場合、1日の帯域幅ピーク値はおよそ次のようになります。
   500Kbps × 100 = 50000kbps = 50Mbps。
- 2022年1月4日にライブイベントストリーミングサービスを使用し、50Mbpsのダウンストリーム帯域幅が発生した場合、2022年1月5日に支払いが必要なライブストリーミング帯域幅の請求書は次のようになります。
   1日あたりのライブストリーミング帯域幅の料金 = 0.2114（米ドル/Mbps/日） × 50（Mbps） = 10.57米ドル。
-  デフォルトでは、ダウンストリーム再生のみ課金され、アップストリームとダウンストリームの使用が不均衡な業務シーン（ダウンストリーム再生：アップストリームプッシュ < 10:1）の場合、1日のプッシュのピーク帯域幅が100Mbpsを超えると、実際のプッシュ使用量に応じて追加のプッシュ料金が課金されます。アップストリームプッシュはダウンストリーム再生の課金方式、公表価格と同じであり、使用量がある段階に達すると個別に課金されます。

>? ライブストリーミングの業務量が大量にあり、日次決済の課金方式ではお客様のニーズを満たせない場合、お客様の課金方式と価格をTencent Cloudの担当者と協議して設定することができます。[チケットを提出](https://console.cloud.tencent.com/workorder/category)して詳細をお問い合わせください。

