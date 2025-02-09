
TencentDB for MySQLインスタンスを同じリージョン内の他のアベイラビリティーゾーンに移行することができます。アベイラビリティーゾーンを移行しても、インスタンスの属性、設定、接続アドレスはすべて変更されません。移行にかかる時間はインスタンスのデータ量によります。

以下のシナリオにおいて、アベイラビリティーゾーンの移行を選択することができます。
- インスタンスのタイプを変更しようとしていますが、現在のアベイラビリティーゾーンにおいて新しいタイプのインスタンスを有効化できないと仮定します。このシナリオにおいて、インスタンスをそのタイプを有効化できるアベイラビリティーゾーンへ移行することができます。
- 現在のアベイラビリティーゾーンに拡張を行うリソースがない状況において、インスタンスを同じリージョン内の他のリソースが充分なアベイラビリティーゾーンへ移行し、ビジネスニーズを満たすことができます。

##  前提条件
- インスタンスステータスが実行中であること。
- インスタンスのあるリージョンに複数のアベイラビリティーゾーンがあり、アベイラビリティーゾーン移行機能をサポートしていること。

## 料金説明
本機能は無料です。インスタンスをシングルアベイラビリティーゾーンからマルチアベイラビリティーゾーンへ移行したとしても、料金はかかりません。

## 機能説明
- 切り替える際にインスタンスアベイラビリティーゾーンは一時的に影響を受けるため、アプリに自動再接続メカニズムを備えるようにしてください。
- アベイラビリティーゾーンを移行しても仮想IP（VIP）の変更は発生しません。
- アベイラビリティーゾーンのマスターインスタンスとROを移行してもデカップリングされず、移行後のマスターインスタンスはま依然としてクロスリージョンのROと同期できます。
- ROインスタンスはアベイラビリティーゾーンを選択できます。
- ROインスタンスはクロスリージョン移行をサポートしていません。
- 移行して切り替える際、ROグループ経由でアクセス（排除）することはできません。
- ターゲットインスタンスがDTSプロセスにおいて、クラウドプラットフォームにタスクチェーンがある場合、クロスアベイラビリティーゾーン移行を行うことはできません。
- 実行中のDTSタスクがある場合、アベイラビリティーゾーンを移行すると、対応するDTSタスクを再起動する必要があります。
- マスターインスタンスがdumperのエクスポートプロセスにおいてクロスアベイラビリティーゾーン経由で移行して切り替える場合、DTSエクスポートは失敗します。
- デュアルノード、トリプルノードアーキテクチャ下でアベイラビリティーゾーンを移行すると、マスタースレーブアベイラビリティーゾーンの選択はリージョンとエリアの残りリソースの制限を受けます。コンソールで移行する際にターゲットアベイラビリティーゾーンを選択すると、スレーブアベイラビリティーゾーンのオプションは自動で更新されます。

## 移行タイプ

| 移行タイプ | シナリオ | サポートタイプ |
|---------|---------|---------|
| 1つのアベイラビリティーゾーンから他のアベイラビリティーゾーンへ移行 |インスタンスのあるアベイラビリティーゾーンで、フルに負荷がかかるかまたはインスタンス性能にその他影響が発生。 |マスターインスタンス、ROインスタンス、ディザスタリカバリインスタンス |
| 1つのアベイラビリティーゾーンから複数のアベイラビリティーゾーンへ移行 | インスタンスの障害復旧レベルを向上させ、コンピュータルームをまたいでの障害復旧を実現します。マスタースレーブインスタンスはそれぞれのアベイラビリティーゾーンに位置します。シングルアベイラビリティーゾーンインスタンスと比較して、マルチアベイラビリティーゾーンはより高いレベルの障害復旧に耐えることができます。例えば、シングルアベイラビリティーゾーンインスタンスはサーバーおよびラックレベルの障害に耐えることができ、マルチアベイラビリティーゾーンインスタンスはコンピュータルームレベルの障害に耐えることができます。 |マスターインスタンス、ROインスタンス、ディザスタリカバリインスタンス |
| 複数のアベイラビリティーゾーンから1つのアベイラビリティーゾーンへ移行 | 特定機能の要求を満たすため。 | マスターインスタンス、ROインスタンス、ディザスタリカバリインスタンス |

## 操作手順
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストの**インスタンスID**または操作列の**管理**をクリックし、インスタンス詳細ページに進みます。
2. **インスタンス詳細ページ**の**基本情報** > **リージョン/アベイラビリティーゾーン**の後で**アベイラビリティーゾーンの移行**をクリックするか、または**可用性情報** > **デプロイ方式**の後で**アベイラビリティーゾーンの変更**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/cd1bd1b09029548391ba986c61027907.png)
3. ポップアップしたダイアログボックスで関連設定を調整し、誤りがないことを確認してから**サブミット**をクリックします。
 - **ターゲットアベイラビリティーゾーン**：ドロップダウンリストでマスターアベイラビリティーゾーンの変更を行うことができ、**マルチアベイラビリティーゾーンのデプロイ**で**はい**を選択すると、スレーブアベイラビリティーゾーンを変更できます。
 - **データチェック遅延閾値**：（マスターアベイラビリティーゾーンを変更する際にこの設定が出現します）、閾値は1秒～10秒の整数です。
>!データ一致性チェックプロセスで遅延が発生する可能性があるため、データ遅延閾値を設定する必要があります。遅延が設定値を超えた際、データベース一致性チェックは停止され、指定閾値以下に戻ってから引き続きデータベース一致性チェックタスクが実行されます。この閾値が小さい場合、移行時間が長くなる可能性があります。
 - **切り替え時間**：選択したメンテナンス時間内または移行完了時に切り替えることができます。詳細については[インスタンスのメンテナンス時間設定](https://intl.cloud.tencent.com/document/product/236/10929)をご参照ください。
![](https://qcloudimg.tencent-cloud.cn/raw/33577bc75f50cb9805478f71b372e07f.png)

