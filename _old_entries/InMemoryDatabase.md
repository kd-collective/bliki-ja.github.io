---
title: InMemoryDatabase
tags: TAGS
---

https://martinfowler.com/bliki/InMemoryDatabase.html

最後の部分を更新

メモリ内データベース（別名：組込みデータベース）とは、ディスクにアクセスすることなく、完全に主記憶装置内だけで動作するデータベースのことである。
プロセスが起動した時点で作成され、プロセス内で動作し、プロセス終了時に破棄される。

一見すると、このすばらしいアイデアは、バカげた話のように聞こえる。
データベースの主な目的は、プロセス終了後の情報の永続化と、複数のプロセスからの同時アクセスの制御の2つだ。
だが、メモリ内データベースはそのどちらも行わない——では、利点は何なのだろう？

最近よく見かけるのは、テスト用に使うことだ。
エンタープライズ アプリケーションを開発する際、データベースに接続するテストは、テストスイーツを実行するたびに膨大な時間をくってしまう。
メモリ内データベースに変更すれば、ビルド時間を大幅に短縮できるような、桁違いの効果が得られるだろう。
多くのThoughtWorkerはグリーンバーをしばらく見ないと震えあがるので、これは我々にとっては大きな違いである。

メモリ内データベースをテスト用に採用するには、2つの方法がある。
まず、SQLメモリ内データベース ライブラリを使用することだ。
Javaの世界でポピュラーなのは、[HSQLDB](http://hsqldb.org/)だろう。
その他の世界では、[SQLite](http://www.sqlite.org/)や[Firebird](http://firebird.sourceforge.net/)が登場している。
これらのツールがナイスなのは、標準SQLで問い合わせができる点だ。
逆に問題なのは、使用するデータベースと同じ方言をサポートしていなかったり、すべての機能を持っていなかったりする点である。
似たようなことは、RAMディスクにファイル ベースのデータベースを走らせればできる。

もうひとつの方法は、すべてのデータベース アクセスを抽象化して、[レポジトリ](PofEAA:Repository)の背後に置くことである。
そうすることで、データベースをメモリ内のデータ構造に置き換えることができる。
通常、オブジェクト グラフの最初のポイントを指すハッシュ テーブルがあれば十分だ。
レポジトリの強みは、一貫した方法で非SQLデータソースにもアクセス（そして、スタブ化も）できる点である。
つまり、あなたのオブジェクト リレーショナル マッピング システムもレポジトリの中に隠すことができるわけだ。

中にはメモリ内データベースを毛嫌いする人もいる。
SQLやオブジェクト リレーショナル マッパーのコードをドメイン モデルに撒き散らしたいという信念をもっているからだ。
メモリ内データベースは、アクセス速度を大幅に向上させる以外にも、
レポジトリがないという「臭い」を消すデオドラントとしても機能する。

これまでのところ、テストが主な使い道になっている。
しかし、メモリ内データベースにはまだ多くの使い道があると思う。
メモリサイズは、アプリケーション データベースの多くをロードできるほど、十分にある。
もし、アプリケーションの状態のすべての変更をイベントログとして記録するならば、
ログを読み込んだ結果のキャッシュとしてメモリ内データベースを使用することができ、
必要に応じてログの再構築をしたり、スナップショットを撮ったりすることができる。
これは、読み出しは多いが書き込みは少ない場合には、非常にスケーラブルかつ高パフォーマンスなスタイルになるだろう。

[Prevayler](http://www.prevayler.org/)はこの種のアプローチを採用しており、多くの注目を集めている。
実際に試した人間は、メモリ内オブジェクトと密結合されており、マイグレーション ツールが無いために深刻な問題になるだろうと述べていた。
しかし私は、記録システムとして変更ログを永続化するアプローチは、これから深く掘り下げていくことのできる肥沃な土地だと考えている。

### フォローアップ

このページを書いてから、興味深いメールを何通かいただいた。
ここでいくつかポイントを共有しようと思う。

ある方は、SQLは得意だがオブジェクトが苦手なことにメモリ内データベースを使っているようだ。
SQLが好きな開発者は、普通はマイノリティのようだが、
たしかにSQLの方がオブジェクトや手続き型コードよりもエレガントに解決できることもある。

同僚のSteve Sparksが、最近のプロジェクトについて教えてくれた。
まず最初に、稼働中のデータベースからデータを引っ張り出し、
それをファイルに保存して、メモリ内レポジトリを初期化し、テストを行う。
そうすることで、その後のクエリはデータベースにアクセスせずに済むのだ。
私はこの手法をC3プロジェクトで最初に目にした。
そこでは、SQLクエリストリングをkeyにしたハッシュテーブルにデータを格納していた。
valueがない場合は、DB2にアクセスして結果をキャッシュした。

（
Peter Becker、Zane Rockenbaugh、Steve Sparksからのコメントに感謝。
また、社内メーリングリストで有用なコメントをくれたThoughtWorkersにも感謝したい。
）
