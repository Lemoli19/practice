# 第 6 回課題

## CloudTrail

> 見つけたイベントの中にはどんな情報が含まれていますか。
> イベント名と、含まれている内容 3 つをピックアップしてください。<br>

StopDBInstance<br>
"eventTime": "2023-02-11T13:18:45Z",<br>
"eventSource": "rds.amazonaws.com",<br>
"eventName": "StopDBInstance",<br>
"awsRegion": "ap-northeast-1"など

StopInstances<br>
"eventTime": "2023-02-07T08:52:22Z",<br>
"eventSource": "ec2.amazonaws.com",<br>
"eventName": "StopInstances",<br>
"awsRegion": "ap-northeast-1"など

## CloudWatch アラーム

> アラームとアクションを設定した状態で、Rails アプリケーションが使える、使えない状態に
> して、動作を確認してみてください。どうなりますか？<br>

→ 使える状態にすると、OK 状態ですよというメールが届き、コンソール画面も OK に変化しました。<br>
使えない状態にすると、アラーム状態ですよというメールが届き、コンソール画面もアラーム状態に変化しました。
<img width="800" alt="CloudWatchアラーム（3）" src="https://user-images.githubusercontent.com/110516041/222367046-c2e75cb7-dfea-4cb8-bd9e-f6dcbd6c06d9.png">
<img width="800" alt="CloucWatchアラーム（2）" src="https://user-images.githubusercontent.com/110516041/222367215-1995774e-2d6a-484b-bb30-e2c71709d55c.png">
<img width="673" alt="ClouWatchアラーム（5）" src="https://user-images.githubusercontent.com/110516041/222370623-62ac80cb-1560-4119-93a0-8f745bf7c09b.png">
<img width="800" alt="CloucWatchアラーム（1）" src="https://user-images.githubusercontent.com/110516041/222367788-54171347-15b3-44fe-a3e7-e9a92f48d16f.png">
<img width="800" alt="CloudWatchアラーム（4）" src="https://user-images.githubusercontent.com/110516041/222370298-024cd9f3-4a9d-44ad-bfa1-fb690b9ed133.png">

## AWS 利用料の見積

https://calculator.aws/#/estimate?id=2a868c9024a35a399cb5be2a2bb30026b77a26cd

## 現在の利用料確認

> 先月の請求情報から、EC2 の料金がいくらか確認してください。
> 無料利用枠で収まっていますか？<br>

→ ＄ 0.00 で、無料利用枠に収まっています。（Cost Explorer で確認）
<img width="800" alt="EC2利用料" src="https://user-images.githubusercontent.com/110516041/222367404-a12086ef-b8fe-4712-8f44-82f56dbb283f.png">
<img width="800" alt="EC2利用料（2）" src="https://user-images.githubusercontent.com/110516041/222367644-df96dd70-2f3b-4e1d-8daa-e0cec2eb2edf.png">

## 感想

CloudWatch アラームで、設定した通りのアクションを起こせることに面白さを感じました。
また昨年 9 月を除き、利用料が無料利用枠に収まっていて安心しましたが、改めてこまめに確認することが大切だと感じました。講座で紹介されていた他のサービスも色々試してみたいと思います。
