---
title: プラットフォーム独立の誤用
tags: [uml]
---

モデル駆動型アーキテクチャ(MDA)の主張は、プラットフォーム独立のモデル(PIM)でシステム開発をすれば、.NETやJavaのようなテクノロジを想定したプラットフォーム特化モデルに変換できる、というものである。注意深い読者はこう言うべきだ。「ちょっと待て。プラットフォーム独立というのはJavaの特徴じゃないか？ どうして、もう一段階独立するプラットフォーム独立テクノロジーが必要になるんだ？」

プラットフォーム独立について考えるには、最初にプラットフォームが何を指すのかを定義する必要がある。Javaのようなテクノロジにとっては、プラットフォームとはハードウェアやOSを指す。Windows上で書いたJavaプログラムをUNIXで動かすことはさほど困難じゃない。これが慣れ親しんできたプラットフォームの用法である。

MDAがプラットフォーム独立を論じるとき、それはプラットフォームとしてのプログラミング環境のことを指す。しかし、これは全くくだらない。MDAはOMG標準（UML、MOF、XMI、CWM）群を使っている。
これらの標準は全て山のようなJavaプラットフォームと同じようなものだ。（.NETも同じ）
あるプラットフォーム独立プログラミング環境を別のものと入れ替えているに過ぎない。今以上の独立は得られないということだ。

それどころか事態はもっと悪い。プログラマなら誰でも書かされる最も簡単なプログラムを取り上げよう。Hello Worldだ。OMGのPIMプラットフォームを相手にどう実装するんだ？ そう、無理だ。OMGのPIM標準には、I/Oライブラリは規定されていないからだ。特定のプラットフォームを呼び出すか、自分で独自ライブラリ（当然、非標準だ）を組み込むしか方法はない。

単にMDAは時間の無駄という意味ではない。MDAのメッセージには他の可能性がある。しかし、プラットフォーム独立の議論は建設的ではない。

### Note

:malapropism:【名】 言葉｛ことば｝の誤用｛ごよう｝ 

## コメント

*2006-08-24 (木) 22:28:12 名無しさん : 「山のような」の原文は「stack」。低レベルから高レベルへとソフトウェアが積み重なって（そしてプラットフォーム独立が達成されている）というイメージでしょう。「山」だと単に「大量にある」という感じしか出てないように思います。が、適当な訳が...。
*2008-05-08 (木) 21:09:20 yasu : プラットフォームの捉え方を少し考える必要があるのではないでしょうか。
