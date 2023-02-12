# 第 5 回課題

## 組み込みサーバーでサンプルアプリ起動

1.EC2 に SSH 接続<br> 2.パッケージのアップデート（今回は特にアップデート無し）<br>
3.Node.js,yarn インストール
<br>
5.git,opnssl 等のパッケージインストール<br>
6.rbenv インストール<br>
7.bash profile 編集<br>
8.ruby-build,ruby インストール<br>
9.MySQL インストール（GPG 鍵更新してから）<br> 10.サンプルアプリを clone<br>
11.bundler,gem インストール<br> 12.環境変数の設定・確認<br>
13.database.yml を編集（development 環境の passward,host,user）<br>
14.MySQL 起動<br> 15.データベースを作成・マイグレーション実行<br> 16.手動でプリコンパイル<br>
17.puma 起動<br>
18.アプリが表示されることを確認<br>
<img width="800" alt="puma" src="https://user-images.githubusercontent.com/110516041/218292317-6968ed6b-638b-46f3-87bd-b32e395fd089.png">


## unicorn 単体でサンプルアプリ起動

1.config/unicorn.rb を編集（root パス,ポートログを記録するファイル等指定）<br>
2.development 環境で unicorn 起動<br> 3.アプリが表示されることを確認


## nginx と unicorn でサンプルアプリ起動

1.nginx インストール<br> 2.バージョンが表示されることを確認<br>
3.nginx 起動<br> 4.ブラウザで http://[EC2 のパブリック IP アドレス]でアクセス<br>
5.nginx の初期ページが表示されることを確認<br>
6.nginx.conf を編集（upstream unicorn や server 等の設定を追記）<br>
7.config/unicorn.rb の listen 部分を編集<br>
8.nginx と unicorn を起動したが、アプリが表示されず「502 Bad Gateway」と表示される<br> 9.エラーを見ると「13:Permission denied」とあり、エラー文を訳すと「上流への接続に失敗」と記載されている<br>
→ 原因は nginx のユーザーが「nginx」だったこと<br>
10.nginx.conf の user を「ec2-user」に変更<br>
11.nginx と unicorn を起動<br> 12.アプリが表示されることを確認<br>
<img width="800" alt="niginx" src="https://user-images.githubusercontent.com/110516041/218292365-2f483c4b-fcef-434e-8283-93ee6219f2b6.png">
<img width="800" alt="nginx_unicorn" src="https://user-images.githubusercontent.com/110516041/218292347-9363c8a9-efa7-4c56-821d-aae2ba2c2c4f.png">
<img width="800" alt="nginx_unicorn(2)" src="https://user-images.githubusercontent.com/110516041/218292352-a3da89a9-16ac-4874-806c-c46053ce3ee6.png">


## ELB 追加

1.事前にターゲットグループを作成・設定<br> 2.ターゲットグループに対象の EC2 を登録<br>
3.ELB のセキュリティグループを作成・設定<br>
4.EC2 のセキュリティグループを修正し、ELB からの接続を許可<br>
5.ELB を作成し ELB 用セキュリティグループを登録<br> 6.ヘルスチェックで「healthy」と表示されていることを確認<br> 7.ブラウザで http://[DNS 名]でアクセスし、アプリが表示されることを確認<br>
<img width="800" alt="ELB" src="https://user-images.githubusercontent.com/110516041/218292371-ac07a711-4638-4243-974e-04002f432d71.png">
<img width="800" alt="ELB(2)" src="https://user-images.githubusercontent.com/110516041/218292377-7e895ef5-2780-4645-942e-b25f54bd7901.png">


## S3 バケット追加

1.S3 バケットを作成・設定<br> 2.「AmazonS3FullAccess」の IAM ロール作成<br>
3.EC2 にアタッチ<br>
4.EC2 上でバケットが表示できることを確認<br> 5.development.rb でデータ保存先を「amazon」に変更<br>6.storage.yml の amazon 部分にバケット名を入力<br>7.IAM ユーザーのアクセスキー ID・シークレットアクセスキーの環境変数を設定し、storage.yml に入力<br>

## サンプルアプリの動作確認

1.Name を入力し Image を選択後、Save ボタンを押しても画面が遷移しない<br> 2.エラーは出ておらず検索もしたが、分からなかったため質問<br> 3.開発者ツールを使用すると、Save ボタンを押した際に一瞬だけ「422 Unprocessable Entity」エラーが出ることが分かった<br>
→ 原因は nginx.conf の設定<br>
4.nginx.conf を編集し直したところ、エラー解決<br> 5.サンプルアプリが動作するようになったものの、画像が表示されない<br> 6.「Image magick をインストールして」というエラーを確認<br>
7.Image magick をインストール<br> 8.画像が表示されるようになった<br>
9.S3 にも保存されていることを確認<br>
<img width="800" alt="S3" src="https://user-images.githubusercontent.com/110516041/218292391-d3a8c3ee-b43a-4c13-8f1e-9536d5b84b6e.png">
<img width="800" alt="S3(2)" src="https://user-images.githubusercontent.com/110516041/218292404-fd55ad4b-4185-4c26-bdb3-f93e82a63458.png">


## 構成図

Raistech ポータルの動画学習教材を参考に dorawio で作成<br>
![第5回課題構成図 drawio](https://user-images.githubusercontent.com/110516041/218292410-f5377924-eb19-4038-a92a-162b8ad8ca76.png)


## 感想

画像がアップロードできない問題に気付いたのが ELB と S3 バケットを追加してからだったので、nginx と unicorn で起動した時に動作確認するべきだったと反省しました。起動出来たからと言って安心し、動作確認を忘れないように注意します。
今回の課題は難しくかなり時間がかかってしまいましたが、完了できて少し自信に繋がりました。また、質問することで頭の中が整理できるんだ、と実感しました。
