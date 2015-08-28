http://martinfowler.com/bliki/InversionOfControl.html

制御の逆転という現象は、フレームワークを拡張とするといつも現れる。 制御の逆転こそが、フレームワークをフレームワークたらしめる特徴であると考えられている場合も多い。

単純な例で考えてみよう。 ユーザーに情報を入力させるプログラムを書いていると思ってほしい。 コマンドライン入力で、情報を取得している。こんな感じだ。

    #ruby
    puts 'What is your name?'
    name = gets
    process_name(name)
    puts 'What is your quest?'
    quest = gets
    process_quest(quest)

この場合、書いたコードがプログラムの制御を握っている。質問の表示、入力の取得、結果の処理を行うタイミングは、これらのコードが制御している。

ただし、ウィンドウシステムをつかって似たようなことをやろうとすると、 今度は、ウィンドウを設定して行うことになる。

    require 'tk'
    root = TkRoot.new()
    name_label = TkLabel.new() {text "What is Your Name?"}
    name_label.pack
    name = TkEntry.new(root).pack
    name.bind("FocusOut") {process_name(name)}
    quest_label = TkLabel.new() {text "What is Your Quest?"}
    quest_label.pack
    quest = TkEntry.new(root).pack
    quest.bind("FocusOut") {process_quest(quest)}
    Tk.mainloop()

これらの２つのプログラムでは、制御の流れが大きく違う。特にprocess_nameメソッドとprocess_questメソッドの呼び出しを制御するところだ。

コマンドライン版では、書かれたコードがメソッドをいつ呼び出すかを決めている。ウィンドウ版ではそうではない。ウィンドウ版では、メソッドを呼び出すタイミングの決定はウィンドウシステムにゆだねられている(Tk.mainloopコマンドによって)。 ウィンドウシステムは、フォームを作成したときのバインド設定にしたがって、書かれたコードを呼び出すタイミングを決定する。つまり、制御が逆転している。フレームワークを呼び出すのではなく、フレームワークに呼び出されるのだ。この現象を「制御の逆転」と呼ぶ(ハリウッド原則とも呼ばれる、「我々を呼ぶな。我々が呼ぶから」だ)。

""フレームワークの第一の重要な特徴は、フレームワークに合わせて利用者が定義したメソッドが、アプリケーションコードからはあまり呼ばれず、フレームワーク自身からよく呼び出されるという点だ。 フレームワークは、アプリケーションの動作を調整したり、動作の順番を制御したりするためのメインプログラムとしての役割を果たす。 制御の逆転によって、フレームワークを拡張可能なスケルトンとして動作することができる。 フレームワークが定義した汎用アルゴリズムにあわせて、利用者はメソッドを作成し、個別のアプリケーションをつくりあげる。

[[Ralph Johnson and Brian Foote|http://www.laputan.org/drc/drc.html]]

制御の逆転の存在が、フレームワークとライブラリを決定的に違うものにしている。 ライブラリとは、基本的に呼び出し可能な関数の集まりである。最近では、通常はクラスの集まりとして構成されている。 関数を呼び出すと、何らかの作業を行い、クライアントに制御を返す。

一方、フレームワークは、抽象的な設計を含んでおり、より多くの振る舞いが組み込まれている。 フレームワークを使うには、作成したクラスを、サブクラス化やプラグインによって、フレームワークに組み込む。フレームワークのコードが、作成したクラスのコードを組み込まれた場所で呼び出す。

呼び出されるコードをフレームワークに組み込むには、様々な方法がある。 上のRubyでの例だと、イベント名とClosureとを引数にして、テキスト入力フィールのbindメソッドを呼び出している。 テキストボックスはそのイベントを検知すると、クロージャのコードを呼び出す。 クロージャをこのように使うのは大変便利だが、サポートしている実装言語は多くない。

別の方法は、フレームワークにイベントを定義させ、クライアントコードからそのイベントをサブスクライブするという方法だ。 .NETはウィジットにイベントを定義できる言語特性をもったプラットフォームの良い例だ。 delegateを使って、メソッドをイベントにbindできる。

上に挙げたアプローチ（本当にそっくりだが）は単純なケースでは、実によく機能する。 しかし、いくつかの必要なメソッド呼び出しをひとつの拡張にまとめたくなるだろう。 そんなときは、フレームワークに、クライアントコードが関連する呼び出しを実装しなければならないインターフェースを定義することができる。

EJBはこういった制御の逆転の良い例だ。 Session Beanを開発するとき、EJBコンテナから様々なポイントで呼び出されるメソッドを実装できる。 例えばSession Beanインターフェースは、ejbRemove、ejbPassive（補助ストレージへの永続化）、ejbActivate（パッシブ状態からのリストア）などを定義している。 あなたは、これらのメソッドの呼び出しを制御することはできない。 ただ、どう動かすかを定義するだけだ。 コンテナが我々を呼び出し、我々はコンテナを呼び出さないのだ。

これらは制御の逆転の複雑なケースであるが、もっと簡単な状況に出会うことがある。 テンプレートメソッドが良い例だ。 スーパークラスが制御の流れを定義し、サブクラスがメソッドや抽象メソッドをオーバーイドして拡張する。 JUnitでは、フレームワークのコードがsetUpとtearDownメソッドを呼び出し、あなたの書く本文部分の準備と掃除をしてくれる。 フレームワークは呼び出しを行い、それにあなたのコードが反応する——そう、また制御が反転している。

最近、IoCコンテナの盛り上がりにより、制御の逆転の意味をめぐっていくつかの混乱がある。 ここで挙げた一般的な原則を、[[依存性注入|http://martinfowler.com/articles/injection.html]](dependency injection){{fn '訳注：邦訳 http://www.kakutani.com/trans/fowler/injection.html'}}のような特化したスタイルの制御の逆転と混同している人がいる。 IoCコンテナがEJBの競合と見なされるため、その名前が（皮肉にも）紛らわしいのだろう。 EJBも制御の逆転をIoCコンテナ以上に使っているのだが。

語源：ここまで述べてきた「制御の逆転」という言葉は、1988年、Object-Oriented Programming誌に掲載されたJohnsonとFooteの論文『[[Designing Reusable Classes|http://www.laputan.org/drc/drc.html]]』に最初に登場した。 この雑誌は古いが、15年以上経った今でも十分に読む価値がある。 彼らはこの言葉をどこか別の場所で手に入れたと考えているが、どこなのかは思い出せないようだ。

この言葉はその後、オブジェクト指向コミュニティに取り込まれ、GoF本に表れた。 より鮮やかな同義語「ハリウッド原則」は、1983年、Mesaについての[[Richard Sweetの論文|http://www.digibarn.com/friends/curbow/star/XDEPaper.pdf]]が初出のようだ。 Desing Goalsの章で彼は、

""我々を呼ぶな。我々が呼ぶ。（ハリウッド規則）：ツールは、「ユーザーにコマンドや実行を尋ねる」モデルを採用するのではなく、Tajo(訳注：Mesaプロジェクトにおけるユーザーインターフェース部品)をあらかじめ準備して、利用者がツールにイベント知らせたいと思ったときに通知できるようにすべきだ。

と書いている。 John Vlissidesは[[C++レポートというコラム|http://www.research.ibm.com/designpatterns/pubs/ph-feb96.txt]]のなかで、「ハリウッド原則」の概念についてうまく説明している。（語源は、Brian FooteとRalph Johnsonにご協力いただいた。ありがとう。）

2005-06-28 (火) 18:13:38 pline? : adminさん、清書してもらってすみません。ちょっとだけ直しました。