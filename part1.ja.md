# はじめに

> 効率とは賢く怠けることである （作者不詳）

> 無精：エネルギーの総支出を減らすために，多大な努力をするように，あなたをかりたてる性質。(Larry Wall）

優れたプログラマが持つハッカー気質のひとつに「無精」があります。大好きなコンピュータの前から一時も離れずにどうやってジャンクフードを手に入れるか――普通の人からするとただの横着に見えるかもしれませんが，ハッカー達にとってそれはいつでも大きな問題でした。たとえば，ハッカーの巣窟として有名なMITのAIラボにはかつて，UNIXのコマンド一発でピザをFAX注文するxpizzaコマンドが存在しました（「xpizza MIT」でググると，1991年当時のmanページが読めます。http://bit.ly/mYAJwZ）。また，RFC 2325として公開されているコーヒーポットプロトコルでは，遠隔地にあるコーヒーポットのコーヒーの量を監視したり，コーヒーを自動的に淹れたりするための半分冗談のインターフェースを定義しています。

こうした「ソフトウェアで楽をする」ハックのうち，もっとも大規模な例が最新鋭の巨大データセンターです。クラウドサービスの裏で動く巨大データセンターは極めて少人数の管理者によって運用されており，大部分の管理はソフトウェアによって極限まで自動化されているという記事を読んだことがある人も多いでしょう。ピザやコーヒーのようなお遊びから，巨大データセンターのように一筋縄ではいかない相手まで，プログラムで「モノ」を思いどおりにコントロールするのはもっとも楽しいハックの一種です。

# OpenFlowの登場

その中でもネットワークをハックする技術の1つが，本連載で取り上げるOpenFlowです。OpenFlowはネットワークスイッチの内部動作を変更するプロトコルを定義しており（OpenFlowの仕様書や標準化に関する情報は，[こちら](http://www.openflow.org/)で得られます。），スイッチをコントロールするソフトウェア（OpenFlowの世界ではコントローラと呼ばれます）によってネットワーク全体をプログラム制御できる世界を目指しています（図1）。

図1　OpenFlowスイッチとコントローラ

OpenFlowの登場によって，今までは専門のオペレータによって管理されていたネットワークがついにプログラマ達にも開放されました。ネットワークをソフトウェアとして記述することにより，たとえば「アプリに合わせて勝手に最適化するネットワーク」や「障害が起こっても自己修復するネットワーク」といった究極の自動化も夢ではなくなります！

本連載では，このOpenFlowプロトコルを使ってネットワークを「ハック」する方法を数回に渡って紹介します。職場や自宅のような中小規模ネットワークでもすぐに試せる実用的なコードを通じて，「OpenFlowって具体的に何に使えるの？」というよくある疑問に答えていきます。OpenFlowやネットワークの基礎から説明しますので，ネットワークの専門家はもちろん，普通のプログラマもすんなり理解できると思います。

まずは，OpenFlowプログラミングのためのフレームワーク「Trema（トレマ）」を紹介しましょう。