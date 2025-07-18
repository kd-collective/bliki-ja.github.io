---
title: MDSDとDSL
tags: [domain specific language]
---

https://martinfowler.com/bliki/MDSDandDSL.html



[モデル駆動ソフトウェア開発](/ModelDrivenSoftwareDevelopment)（MDSD）と[ドメイン特化言語](/DomainSpecificLanguage)（DSL）の関係は？

MDSDの文脈でいきなり「DSL」って言葉が出てくることがよくある。 MDSDな人たちは「DSLはMDSDの世界だけに存在する」って思ってるみたいだ。書籍の執筆のためにDSLについてはいろいろと書いているんだけど、 MDSDから見たDSLについては何も書いてない。普通のプログラミングにおけるDSLの役割ばかり書いている。 DSLはテキストを使う言語の世界にも図を使うMDSDの世界のどちらにも存在していて、その役割はどちらの場合もほとんど同じものなのだ。

MDSDの場合でも、DSLは、UMLのような汎用言語と対になる特定の問題を対象とした言語である。普通の言語とDSLの関係性とまったく同じだ——汎用モデリング言語でシステムを構築し、DSLを使って特定の場面に対応するわけである。ただ、MDSDはあまり普及していないので、いつもとはちょっと違ったDSLの使い方を目にすることになるだろう。いくつかのDSLからJavaのコードを生成して、 Javaのプロジェクトに統合するなんてことをやるかもしれない。この場合、汎用MDSDモデルなんてのは存在しない——各DSLに対して個別にMDSDを行うことになる。

モデル指向DSLを使うには、ツールに[ProjectionalEditing](https://martinfowler.com/bliki/ProjectionalEditing.html)機能が必要となる。しかし、この機能はまだ完全にサポートされているとは言いがたく、それが深刻な問題となっている。独自DSLを定義するには、より特化したツールが必要である——たとえば、私が[言語ワークベンチ](/LanguageWorkbench)と呼んでいるようなものだ。

DSLは、主流のプログラミング世界よりも、MDSDの世界のほうが注目を集めている。 Cynicsは、これはMDSDコミュニティが必死に生き残りの術を模索し、MDSDのファンがMDSDの洗練さの高さの証だと見なした結果であると考えている。私は、MDSDコミュニティがまだ小さく、確立したやり方が少ないからだと考えている。

特に、MDSDの可視化サブコミュニティは、[モデル駆動アーキテクチャ](/ModelDrivenArchitecture)（MDA）を軸として展開している。私は別にMDAのファンでもなんでもないが、[MDAのDSLには特に懐疑的だ](https://martinfowler.com/articles/mdaLanguageWorkbench.html)。

モデル指向DSLはテキストDSLと共有するものが多い。私は、[意味モデル](https://martinfowler.com/dslwip/SemanticModel.html)の扱いにおいて、テキストDSLには注目している。 MDSDは、その名が示すように、モデルでシステムを駆動するものだ。 MDSD好きは、モデルをそのまま実行するのではなく、モデルからコードを生成したいと考えているようだ。

これを書いているなかで、私の著書にある言語ワークベンチについてどれだけ触れればよいか分からなかった。包括的な概念の表面的なことしか触れるつもりはなく、それほど深いものにはならないかもしれない。それは、ひとつには、テキストDSLの生成の題材が多すぎることに原因がある。また、言語ワークベンチの概念が新しく、移ろいやすく、まだ成熟していない代物だからでもある。
