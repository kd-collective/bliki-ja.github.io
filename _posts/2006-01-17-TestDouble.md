---
title: テストダブル
tags: [testing]
---

http://martinfowler.com/bliki/TestDouble.html

2006/01/17 



Gerard Meszarosが、様々な[Xunit](http://martinfowler.com/bliki/Xunit.html)フレームワークを使用したパターンを集めた[書籍を執筆中](http://tap.testautomationpatterns.com:8080/Book%20Outline.html)である。
彼は、ある厄介なことに出くわしている。
システムの一部分をテストするためにスタブ化することがあるが、
その名前というのが、スタブ、モック、フェイク、ダミーなど、色々とあるのだ。
そのため彼は、自身の用語集を作成した。
この用語集は広く普及すべきものだろう。



彼が一般的な用語として使っているのは、「Test Double（テスト代役）」という言葉だ（スタントの代役(double)を想像してほしい）。
Test Doubleは、テスト用にオブジェクトを入れ替えるときに一般的に用いられる言葉である。
Gerardが作成したリストには、様々なDoubleが載っている。


* '''ダミーオブジェクト'''は、受け渡されることはあるが実際に使用されることはない。パラメータリストを埋めたいだけといった場合に利用されることが多い。 

* '''フェイク'''オブジェクトは実際に動作するよう実装されてはいるが、手抜きがされているので製品版には向かない（[[InMemoryDatabase]]が良い例である）。 

* '''スタブ'''はテスト時の呼び出しに対して、あらかじめ用意された結果を返す。通常、テスト用にプログラムされたところ以外には応答しない。スタブは呼び出しの情報を記録することもある。例えば、Eメールゲートウェイスタブは「送られた（とされる）」メッセージを記録するような場合だ。単に「送られた（とされる）」メールの数を記録する場合もあるだろう。

* '''モック'''は、エクスペクテーションが事前にプログラムされたものである。エクスペクテーションとは、受信する一連の呼び出しの仕様を表わしたものである。期待されない呼び出しが行なわれた場合は例外をスローする。また、テスト実行後の検証(verification)で、期待された呼び出しがすべてきちんと行われたかどうかが確認される。 

 