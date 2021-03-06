Ethereumと複雑なブロックチェーンプログラムは新しく、実験的なものです。
新しいバグやセキュリティリスクが発見され、新しいベストプラクティスが開発されると、セキュリティの状況に絶え間ない変化が予想されるはずです。 
したがって、この文書のセキュリティプラクティスに従うことは、スマートコントラクトエンジニアとして行う必要があるセキュリティ対策の始まりに過ぎません。

スマートコントラクトプログラミングには、あなたが慣れ親しんでいたのとは異なるエンジニアリングの考え方が必要です。
障害のコストは高くなる可能性があり、変更は困難な場合があります。Webやモバイル開発よりも、ハードウェアや金融サービスのプログラミングに似ています。
したがって、既知の脆弱性を守るだけでは十分ではありません。開発の新しい哲学を学ぶ必要があります。

## 失敗する準備

全ての重要なコントラクトには不具合が含まれる可能性があります。
よってコードはバグや脆弱性に正常に対応できる必要があります。

  - 事態が悪化しそうな時にコントラクトを一時停止する('サーキットブレーカー')
  - リスクに備えて資金を管理する(レート制限、最大使用量)
  - バグ修正と改善のためのアップグレード方法を準備する

## 慎重にリリースする

本番リリース前にバグを発見できるようにしましょう。

  - コントラクトを徹底的にテストし、新しい攻撃方法が発見された時にテストを追加する
  - [バグバウンティプログラム](#bounties)による報奨金制度を提供する
  - 段階的にリリースし、各段階で使用量とテストを増やす

## コントラクトをシンプルに保つ

複雑さはエラーの可能性を高めます。

  - コントラクトのロジックがシンプルであることを確認する。
  - コントラクトや関数を小さく保つためにモジュール化する
  - 可能なら、既に存在するツールやコードを使用する(例えば、オリジナルの乱数ジェネレーターを書かない)
  - 可能な限りパフォーマンスを明確にする
  - 分散を必要とする部分にのみブロックチェーンを使用する


## コードをこまめにアップデートする

下記を参考にセキュリティ対策を続けてください。

  - 新しく発見されたバグを確認する
  - ツールまたはライブラリの最新バージョンにできるだけ早くアップグレードする
  - 有効と思われる新しいセキュリティ技術を採用する

## ブロックチェーンのプロパティに注意する

あなたのプログラミング経験の多くはEthereumプログラミングに役立ちますが、注意すべきいくつかの落とし穴があります。

  - 悪質なコードを実行したり、制御フローを変更したりする可能性のある外部のコントラクトをコールする際は十分注意してください。
  - コントラクトコードは公開されていることを理解してください。悪意を持って呼び出される可能性があります。データは誰でも見ることが出来ます。
  - ガスコストとブロックガスの制限を念頭に置いてください。

## 根本的なトレードオフ: シンプルさ vs 複雑さ

スマートコントラクトの構造とセキュリティを評価する際に考慮すべき複数の根本的なトレードオフがあります。
スマートコントラクトの一般的な推奨事項は、これらの根本的なトレードオフの適切なバランスを特定することです。

理想的なスマートコントラクトは、ソフトウェアエンジニアリングによるモジュール化であり、
コードを複製せずに再利用し、アップグレード可能なコンポーネントをサポートします。

ただし、セキュリティとソフトウェアエンジニアリングのベストプラクティスが一致しない場合があるという重要な例外があります。
いずれの場合も、以下のようなコントラクトシステムの規模に合った最適な特徴の組み合わせを特定することによって、適切なバランスを知ることが出来ます。

- アップグレード不可 vs アップグレード可能
- モノリシック vs モジュラー
- 重複 vs 再利用

### アップグレード不可 vs アップグレード可能

このような複数のリソースは、キルしやすい、アップグレード可能、または変更可能な可用性を強調しますが、
可用性とセキュリティの間には根本的なトレードオフがあります。

定義による可用性パターンは複雑さと潜在的な攻撃面を追加します。
シンプルさは、スマートコントラクトが管理不要で有効期限のあるトークンセールシステムなど、
あらかじめ定義された期間、限られた機能を実行する場合の複雑さに対して特に効果的です。

### モノリシック vs モジュラー

モノリシックな自己完結型コントラクトは、すべての知識をローカルに識別して読み取り可能にします。
モノリスとして存在する高性能なコントラクトシステムはほとんど存在しませんが、コードレビューの効率を最適化する場合など、
データとフローの極端な地域に対して議論が必要です。

ここで考慮されている他のトレードオフと同様に、セキュリティのベストプラクティスは、
単純な短命契約のソフトウェアエンジニアリングのベストプラクティスと、
より複雑な永続契約システムの場合のソフトウェアエンジニアリングのベストプラクティスへの傾向から離れています。

### 重複 vs 再利用

ソフトウェアエンジニアリングの観点から見たスマートコントラクトシステムは、合理的なところで再利用を最大限にしようとしています。
Solidityでコントラクトコードを再利用する方法はたくさんあります。
あなたが所有している証明済みの以前にデプロイされたコントラクトを使うことは、一般的にコードの再利用を達成する最も安全な方法です。

自己所有の以前に展開された契約が利用できない場合、複製は頻繁に使用されます。
[Live Libs](https://github.com/ConsenSys/live-libs)や
[Zeppelin Solidity](https://github.com/OpenZeppelin/zeppelin-solidity)のような取り組みは、
安全なコードを重複することなく再利用することができます。
コントラクト上のセキュリティ分析には、対象のスマートコントラクトシステムでリスクのある資金と釣り合ったレベルの信頼を以前に
確立していない再利用されたコードが含まれていなければなりません。