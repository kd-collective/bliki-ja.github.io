http://martinfowler.com/bliki/Buildix.html

//I've talked many times about the virtues of Continuous Integration. To get such an environment working you need a continuous integration server, and a source code control system. To make a project run smoothly you could also do with an issue tracker for bug tracking and the like, and a wiki to help capture all sorts of project knowledge.

[[継続的インテグレーション|http://martinfowler.com/articles/continuousIntegration.html]]（[[邦訳|http://www.objectclub.jp/community/XP-jp/xp_relate/cont-j]]）の長所については、何度もお話してきた。
継続的インテグレーションを行うには、インテグレーション用のサーバとソースコード管理システムが必要となる。
プロジェクトをよりスムーズに進めるためには、バグトラッキングなどに使うイシュートラッカーと、プロジェクトのナレッジをまとめるWikiが必要である。

//Getting a good environment with all of these things up and integrated together is a tougher job than you might think. Inevitably we found we would be messing around for a week or so on new projects to get the build server set up with all this stuff. I mentioned before that our London office has grown a really sharp deployment team, one of their side jobs has been to sort out putting together a build server.

以上のようなツールを組み合わせて環境を作っていくのは、思っている以上に面倒な作業である。
新しいプロジェクトを始めるときには、だいたい1週間程度、このような環境の構築に時間をかけることになる。
以前にもお話したが、ロンドンオフィスでは、切れ味の鋭い開発チームを育成してきた。
彼らのもうひとつの仕事は、ビルドサーバをうまくまとめることだった。

//It's been trialled on a few ThoughtWorks projects, and now it's available for everyone. Buildix is a complete development server, tested in the field by ThoughtWorkers (a very demanding lot), and available for free.

これまでThoughtWorks社内のプロジェクトで試験的に使用してきたが、ようやくみんなにお披露目することができる。
[[Buildix|http://buildix.thoughtworks.com/]]はすべてを統合した開発サーバである。
ThoughtWorkerたち（要望の激しい人たち）の手によって現場でテストされたものだ。
これは無料で使用することができる。

//It's free because it's a collection of open-source software that our deployment wizards (Chris Read, Julian Simpson, and Tom Sulston) have integrated together with some of that magic powder they found in the fridge.

なぜ無料なのかというと、オープンソースソフトウェアを組み合わせたものだからだ。
これらは弊社のウィザードたち（[[Chris Read|http://www.chris-read.net/]], Julian Simpson, and Tom Sulston）が、冷蔵庫で見つけた魔法の力を使って統合した。

//The server uses Knoppix (a Debian Linux distro) as its operating system. It's a live CD so will run just off the CD drive if you want to play with it. As with any of these live CDs you can then install it to your hard drive easily and you have the full server ready to go. There's also a VMWare Image.

サーバのOSには[[Knoppix|http://www.knoppix.org/]]（Debian Linuxディストリビューションのひとつ）を使用している。これはライブCDになっているため、CDドライブに入れれば起動することができる。
他のライブCDと同様、ハードドライブに簡単にインストールすることもできる。
これで完璧なサーバが利用可能となる。
VMWareのイメージ版も存在する。

//In the box in Subversion, Cruise Control, and Trac. It also is setup to run Samba (to provide windows shares), DNS, and DHCP if you need them.

ここには[[Subversion|http://subversion.tigris.org/]]、[[Cruise Controll|http://cruisecontrol.sourceforge.net/]]、そして[[Trac|http://projects.edgewall.com/trac/]]が含まれている。
必要であれば、Samba（Windowsと共有するために）、DNS、DHCPの設定も行うことができる。

//See Chris's blog post for some more background.

詳細については[[Chrisのblogの投稿|http://www.chris-read.net/?p=8]]を見てほしい。