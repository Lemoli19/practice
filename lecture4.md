# 第4回講座での学び
## 課題で行ったこと
1. AWS上でVPC・サブネットを作成
1. 作成したVPC上にEC2を構築。セキュリティグループも併せて作成<br>
（インバウンドルールにSSH,HTTP,HTTPS追加）<br>

1. 作成したVPC上にRDSを構築。【EC2コンピューティングリソースに接続】にチェックを入れると、セキュリティグループは自動的に作成してくれたため楽でした。<br>
参考：https://aws.amazon.com/jp/about-aws/whats-new/2022/08/amazon-rds-setting-up-connectivity-rds-database-ec2-compute-instance-1-click/
1. EC2 Instance ConnectでEC2にSSH接続
1. EC2からRDSに接続

## 感想
受講開始前にAWSハンズオンで事前学習をしていたため、スムーズに課題を進められました。何回も実際に構築してみることで、より理解が深まると感じました。徐々に課題が難しくなっていくのでしっかり復習します！