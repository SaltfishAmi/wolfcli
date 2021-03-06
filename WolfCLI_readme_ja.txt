WOLF RPGエディター コマンド ライン インタプリタ システム コモン 作者：SaltfishAmi
現在のバージョンはWOLF RPGエディターのバージョン2.10に基づいて作られています。

ちょっとずつ日本語説明書を追加して行きますが、これからもゲーム内のコメント文や最新の情報は常に英語で書かれると予想されています。
ご理解・ご容赦の程お願い致します。

このコモンを使用することで、コマンドラインインタフェース的な機能が得られます。主な機能は以下の通り：
（注意：未だに実装されていない機能が多数あります。詳しくはもっと下に「■■■注意：」をご覧ください。）
- 基本的なコマンド：
     - 標準入出力コマンド：echo（文字表示）, msgbox（メッセージボックス、選択肢あり）, getchar（キーボード1文字入力）, getline（キーボード文字列入力）など
     - ファイル入出力コマンド：fread（ファイル読込）, fgetline（ファイル1行読込）, fwrite（ファイル書込）など
     - ディレクトリツリー：cd（フォルダ切替）, ls（ファイルリスト）, md（新規フォルダ作成）など
     - 変数操作：3+2, a+b, c=a+bなど
     - 文字列操作：concat（文字列連結）, pushline（上に1行追加）, popline（上から1行読込後消去）, substr（位置を指定して切り出し）, pos（サブ文字列の出現位置）など
     - ウディタEv呼び出し：ev(500223,1)など
     - コマンド別名：alias("refresh(","common(223,") - 今のところ予定されていません
     - ファイル名によるスクリプト実行（パラメータあり）：start.wcs "test"
- コマンド入力と文字出力が可能なコマンドラインインタフェース
- 複数行文字列をスクリプトとして解釈及び実行
- ウディタ変数とは別に、名前によって呼び出せる変数（例えばa="test"）
- ウディタ変数のアクセス（_s_3000000→文字列変数S[3]、_i_1600001→このコモンのセルフ変数01など）
- ゲームによって変わるような変数位置をコンフィグファイルから読み込むことによって、コマンドで直接ゲーム内変数（HPなど）をアクセスする - 今の所予定されていません
     - 例えば、プレイヤーHPの変数呼出値とプレイヤー情報表示コモンの呼び出し方法をコンフィグに記載すると、
     - それを読み込んでからHP=9999（HPを設定する）とrefresh（情報更新）を実行するだけでHPを変更できます
- 複数行のスクリプトでのみ使える簡単な条件判断（if-else-endif）やループ（loop-break-next）など
- ローカルディスクとインターネット両方のファイルアクセス

■■■注意：未だに実装されていない機能が多数あります。今のところ使えるコマンドは以下の通り：
assign, break, cat, cd, cls, cmd, concat, dl, echo, else, endif, exit, getchar, getline, help, if, int, loop, ls, length, lines, md, msgbox, next, return, str
このうちスクリプトファイルでのみ使えるコマンドは break, else, endif, if, loop, next, returnです。
ファイル名を入力してスクリプトとして実行するのもできます。

文法などは同梱のスクリプトサンプル「startup.wcs」「move.wcs」をご覧ください。中身は普通のテキスト形式です。

このコモンを使用することで高度なデバッグやチートモードなどを作れます。
あるいはウイルス的な使い方をして、プレイヤー様の真っ青な顔を見て楽しむのもいいですね！（やらないでください。俺はやるけど）

このコモンは今のところ未完成でバグだらけですがある程度には使える（遊べる？）と思います。
楽しんでくれると幸いです。バグ報告と新機能の提案は歓迎します。

バグ報告や、新機能の提案などは有り難く受け付けますが、すぐに処理できると約束できません。
このアドレスにメールをお送りください：aaabbb1112221575@gmail.com
英語・中国語・日本語を理解できます。

導入の際、手動で調整する必要のある設定は一番最初のコモンEv「■WolfRPG CLI System」にあります。
お手数をおかけしますが、必要に応じて調整をお願い致します。
コモンEv「■WolfRPG CLI System」の中にも細かい説明（日本語あり）がありますので更新する度に読んでみてください。
また、ゲーム内で初めてWolfCLI機能をお使いになる前に必ず一度「■WolfRPG CLI System」を呼び出してください。
タイトルスクリーンイベントで呼び出すことをお勧めします。

スクリプトサンプルはこういう風にテストできます：
 |■イベントの挿入： コモンXXX：[ 0■WolfRPG CLI System ]
 |■文字列操作：S0[[サンプル]一時文字列] =<ﾌｧｲﾙ内容読込> "startup.wcs"
 |■イベントの挿入： S0[[サンプル]一時文字列] = コモンXXX：[ 2├■MultiLineParser ] / S0[[サンプル]一時文字列]
returnで返される値はS0[[サンプル]一時文字列]に格納されます。
また、
 |■イベントの挿入： コモンXXX：[ 9├■CmdMode ]
のように、コマンドプロンプトを呼び出してファイル名をタイプしてテストすることもできます。

ChangeLog:
2019/06/12 初公開
2019/06/12 間抜けを修正
2019/06/14
新コマンド実装：getchar getline
文字列のバイト数（半角=1、全角=2）を計算する内部処理を実装
（これで、日本語フォルダ名によるカーソルの座標の狂いは解消される）
行数計算の実装と、それに関する内部処理の修正
多重ループの実装
新機能に合わせて説明書の加筆修正
新機能を使用したサンプルスクリプトを追加
その他いろいろ間抜けを修正
2019/07/07
lsコマンドでフォルダ項目の色が変更しない不具合を修正
画面がいっぱいの時にgetlineコマンドを使用すると自動的に1行空けておくように修正
2019/12/10
lsフォルダー判別方法を読み込み<NoFile>からフォルダー切り替え<<ERROR>>に修正