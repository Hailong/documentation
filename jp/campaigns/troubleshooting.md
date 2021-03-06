# キャンペーントラブルシューティング

## ページ訪問者が認識されない

いくつかの理由が考えられます:

1) Mauticにログイン中にテストはしていないか確認してください。Mauticはユーザーの生成したアクティビティは無視するので、アノニマスセッションや別のブラウザーを使うか、Mauticからログアウトしてください。

2) 追跡しているコンタクトがキャンペーン内に存在するようにしてください。そのコンタクトのページヒットでのタイムラインを見直せが、これを簡単に確認できます。

3) キャンペーンは連続して実行され、コンタクトごとには繰り返されません。コンタクトがキャンペーンのページに既に訪問していてページディシジョン訪問をトリガーしていれば、続いて訪問してもそのディシジョンに関連付けられたアクションを再トリガーすることはありません。

4) キャンペーンアクション内のURLが訪問したURLに_正確に_マッチするようにするか、もしくはワイルドカードを使用するようにしてください。(<a href="https://ja.wikipedia.org/wiki/Uniform_Resource_Locator" target="_blank">URLにはスキーマ、ホスト/ドメイン、パス、クエリーパラメータ、そして/もしくはフラグメントが含まれることに留意してください)

例えば、`http://example.com`というURLを持っていたとして、ページヒットが`http://example.com/index.php?foo=bar`を登録したとすると、キャンペーンディシジョンはトリガーされません。しかし、`http://example.com*`をURLとして使うとマッチするのでトリガーされます。

別の例としては、別のページヒットを特定のキャンペーンに関連付けたい場合があります。仮にキャンペーンAとキャンペーンBがあるとしましょう。両方のキャンペーンで同じベースURLとパス、しかし別のクエリーパラメータを使いたい場合、キャンペーンAでは`http://example.com/my-page?utm_campaign=A*`、キャンペーンBでは`http://example.com/my-page?utm_campaign=B*`、をページディシジョンに設定できます。これでコンタクトは望ましい特定のキャンペーンのみをトリガーできます。もしクエリーパラメータに関係なく両方のキャンペーンをトリガーさせたい場合は、`http://example.com/my-page*`を使います。
