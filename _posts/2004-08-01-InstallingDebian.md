---
title: Debianのインストール
tags: [tools]
---

https://martinfowler.com/bliki/InstallingDebian.html

ここ数週間ばかし、[Debian](http://www.debian.org/) Linux のインストールをやってみた。
ここ数ヶ月間、新しい環境をいろいろとセットアップしなきゃいけなかったんだよ。
新しいデスクトップを手に入れたから、Windows XPをインストールしたでしょう？ それから、MacOS Xの入ったPowerbookでしょう？ それからそれから、Windows XPの入った仕事用のノートでしょう？ あーなんかいろんな作業があるんですけど……。仕事用のノートにはThoughtWorksが設定したWindows XPがインストールされてるんだけど、私が仕事に使うアプリケーションは別途インストールしなきゃいけないわけじゃない？（面倒くせー）

では、このお話のDebianの章に移ろう。それには2つの物語があったのじゃ……。
まず、地下のLinuxサーバをRedHatからDebianに変えた。それから、プライマリなデスクトップマシンにもDebianをインストールした。

サーバへのインストールはいつも緊張するよね。ちゃんと動いていて欲しいもんね。
マシンは古いけど（6年位前に買った）、主にファイルサーバ（smbとcvs）と音楽サーバ（[Slimp3](/Slimp3)）としてしっかり動いている。
サーバのOSが古いのは（RedHat 7.2）、アップグレードがダルいからやってないだけ。
Debianを選んだのは、あまりアップグレードしないからだ。それと、安定したディストリビューションだって定評もあるしね。

もちろん、Debianのインストールはひどい。だけど、サーバへのインストールだとXを使わなくてもいいから、インストール作業は非常に楽である。
まだ他にもある。
Debianをちゃんとマシンにインストールしたんだけど、
おニューの250GBハードディスクをちゃんと認識してくれない。
どうやらカーネルのバージョンを上げないといけないみたいだ。
Debianパッケージが使えるやつの1リビジョン上のやつ。
こうなったらカーネルの再構築だ。
とはいっても、カーネルの再構築なんて今までやったことない。
上がりっぱなしの血圧は下がる様子もない。
でも、[これ](http://www.osnews.com/story.php?news_id=2949)と[これ](http://newbiedoc.sourceforge.net/system/kernel-pkg.html)のおかげで、うまく乗り越えることが出来たよ。

インストールが出来たら出来たで、今度はRedHatで動いていたやつをDebianで動かさなければならない。結論から言おう。アプリケーションがDebianパッケージ管理システム（apt-get）をきちんとサポートしていれば、そんなのごりっと丸写し気分で解決である。 面倒くさいのは、パッケージがapt-getに対応してないとき（Java）と、apt-getのパッケージが全くアップデートされてないとき（rexml）。 それでも他のunixと比べて悪くはなんだけど、単にapt-getを使ってでもインストールできないというのが余計に悪く感じるんだよね。

デスクトップの方はそんなに悩まなかったけど、それでもいろいろ試行錯誤した。
実は古いデスクトップマシンでは、数ヶ月ほどDebianを使っていたのだ。
新しいマシンを手に入れたときから、Debianをデュアル・ブートさせようと考えていた。
Debianをデスクトップで使うときのヒント1。オフィシャルなインストーラーを使うべからず。それがsarge用の[新しいインストーラー](http://www.debian.org/devel/debian-installer/)であってもだ。
sarge用のインストーラーは今んところ大丈夫のようだけど、
Xの設定がまだ十分ではない。
Xの設定をしようと思ったら、インストーラーがわけわからん質問を次々と投げかけてくる。んなもん答えられないってば。
新しいデスクトップにWindowsをインストールするのと、Xをちゃんと設定するのって、どっちがマシかよく分からない。

幸い、[Knoppix](http://www.knoppix.org/)（または[カスタマイズ版](http://www.knoppix.net/docs/index.php/KnoppixCustomizations)）を使えば、この苦悩から逃れることができる。
以前のテストマシンには、[Morphix Lite GUI](http://www.morphix.org/modules/news/)（Knoppixをカスタマイズして軽量UIをくっつけたもの）を使っていた。これなら古いマシンでもちゃんと動く。
新しいマシンにはもう少しパワフルなのがいい。KDEとかGnomeとか。
でもこれらは私が望む以上に複雑だった。
インストールは何の問題もなく終わったが、
apt-getアップグレード最中に、3度ぐちゃぐちゃになった。
そのうち2回はブートレコードが壊れ、CDから再インストールしなくてはならなかった。
どうにか動くようになり、KDEをアップデートできたが、googleとこれまでの経験がないと、確実にハマっていたと思う。

結局、Knoppixみたいなものもあるけど、それでもまだインストール作業は簡単なもんじゃないよね。まだKDEを試す時間がないけど、他のディストリビューションのほうが簡単なのかもしれない。RedHat 9 のインストールは確実に簡単だったよ。あ、でも、アップグレードの呪縛があるんだよね。

### Update - August 2004

上で語ったことは全部、いまもそのままだ。しかし、もうちょっとだけ話がある。 デスクトップへのMorphixベースのインストールはおおむねうまくいったんだが、いくつか些細な部分でイラつくことがあった。その一番はUIの問題だ。 Xの設定が、どうしてかは知らないが画面の左右1/4インチくらいがモニタの外へはみ出てしまう。 そのため、ウィンドウやアイコンが画面の右端へ移動してしまうと、画面から見えなくなってしまうのだ。我慢できなくもないけど、やはり苦痛ではある。 やはりXウィンドウの設定はヒドイ。ウィンドウズでのGUIの設定は前から簡単だったのに ね。

これを直そうして、またえらい時間を食った。新しいsarge版インストーラーの最新版をまた試してみたんだが、それに付いてくるXの設定ツールは前のと変わらず役たたずだった。 結局この問題を解決した方法は、予備のディスクの一部にRedHat 9をインストールして、そのXF86Configファイルを私のDebianシステムへコピーすることだった。 Debian側のファイルからフォントパスのエントリーを追加する必要はあったけれど、これでやっと画面端が隠れることはなくなった。 ということで、これがうまくいったのは良かったんだが、GUIの問題を解決するのにこんな奇怪な方法をやらなきゃならんとは困ったもんだ。
