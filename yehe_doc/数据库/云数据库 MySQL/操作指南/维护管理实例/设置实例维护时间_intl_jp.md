## 操作シナリオ
メンテナンス時間はTencentDB for MySQLとって非常に重要です。お客様のTencentDB for MySQLインスタンスの安定性を保証するために、バックエンドのシステムは不定期でメンテナンス時間帯に、インスタンスのメンテナンス操作を行います。業務インスタンスに対して許容可能なメンテナンス時間を設定することをお勧めします。一般的には、業務のオフピーク期間に設定すると、業務への影響を最小限に抑えられます。

また、インスタンス仕様の調整、インスタンスのバージョンアップ、インスタンスカーネルのアップグレードなど、データの移行に関わる操作も、メンテナンス時間帯（現在、マスターインスタンス、読み取り専用インスタンス、ディザスタリカバリインスタンスはいずれもメンテナンス時間をサポートします）に設定することをお勧めします。

データベースインスタンス仕様のアップグレードを例にすると、インスタンス仕様のアップグレードがデータ移行に関わる場合、アップグレード完了時に秒レベルのデータベースの瞬断が起きます。アップグレードを始める際に**切り替え時間**を【メンテナンス時間帯】に選択することで、インスタンス仕様の切り替えがインスタンスのアップグレード完了後の次の**メンテナンス時間**帯に実行されます。ただし、切り替え時間を【メンテナンス時間帯】に選択した場合、データベース仕様のアップグレードが完了した後には直ちに切り替え作業を実行せず、インスタンスの**メンテナンス時間**帯に切り替えを開始するまでは同期を維持します。そのため、インスタンス全体のアップグレードに要する時間が長くなる場合があります。

>?
>- TencentDB for MySQLはメンテナンス実施前に、Tencent Cloudアカウント内に設定された連絡先担当者にショートメッセージとメールを送信しますので、受け取りにご注意ください。
>- インスタンス切り替え時に、秒レベルのデータベースの瞬断が起きます。業務に確実に再接続機能が備わっていることを確認してください。

## 操作手順
### メンテナンス時間の設定
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb/)にログインし、インスタンスリストのインスタンス名または「操作」の列の【管理】をクリックし、インスタンス詳細画面に入ります。
2. 詳細画面の「メンテナンス情報」で【変更】をクリックします。
![](https://main.qcloudimg.com/raw/388e3aa6ca18c6cb947eb4d053ad1eb5.png)
3. ポップアップされたダイアログボックスで、必要な「メンテナンス周期」と「メンテナンス時間」を選択して、【OK】をクリックします。
![](https://main.qcloudimg.com/raw/001fee80a9e1e7f5f55c2de15802a613.png)

<span id="lijiqiehuan"></span>
### 今すぐ切り替え
特定のタスクをメンテナンス時間帯に切り替えることを選択したものの、特殊な事情によりメンテナンス時間前に切り替える必要がある場合、「操作」列の【今すぐ切り替え】をクリックすることができます。
![](https://main.qcloudimg.com/raw/fd9780d4f9e1d8094bcb82f215deb366.png)

>?
>- 今すぐ切り替えはインスタンス仕様のアップグレード、バージョンアップ、インスタンスカーネルのアップグレードなど、データの移行に関わる操作に適用されます。
>- バージョンアップ操作では、インスタンスが複数のインスタンスに関連付けられている場合、切替順序は、災害準備インスタンス、読取り専用インスタンス、プライマリインスタンスの順に行われます。
