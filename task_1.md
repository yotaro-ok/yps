# yps1 task#1

## 1. GitHubアカウントの作成

***

## 2. AWS無料枠アカウントの作成

[AWS 無料利用枠](https://aws.amazon.com/jp/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc)

[住所を英語に変換できるサイト](https://kimini.jp/)
<br>
<br>
#### Step.1 メールアドレスとクレジットカードを用意してAWSアカウントを作成してください　AWSアカウント名は適当で構いません
![スクリーンショット 2020-07-18 20-30-12](https://user-images.githubusercontent.com/63440984/87853259-b5e69200-c943-11ea-996a-4e014ebeced9.png)
#### Step.2 ベーシックプランを選択してください
![スクリーンショット 2020-07-18 20-36-28](https://user-images.githubusercontent.com/63440984/87853263-ba12af80-c943-11ea-8bf4-de4a00f66a94.png)

#### なんやかんや入力したと思いますが完了です

<br>
<br>

***

## 3. EC2上にCentOS7でインスタンス作成

#### Step.1 EC2　を選択してください
![スクリーンショット 2020-07-18 20-54-50](https://user-images.githubusercontent.com/63440984/87853267-be3ecd00-c943-11ea-9635-87ec4f1a6a69.png)
#### Step.2 インスタンス　を選択してください
![スクリーンショット 2020-07-18 20-56-02](https://user-images.githubusercontent.com/63440984/87853269-c0a12700-c943-11ea-9c7b-5540f24ff89f.png)
#### Step.3 インスタンスの作成　を選択してください
![スクリーンショット 2020-07-18 20-56-42](https://user-images.githubusercontent.com/63440984/87853271-c39c1780-c943-11ea-97fb-c16ba63dcd10.png)
#### Step.4 無料利用枠のみ　を選択してください
![スクリーンショット 2020-07-18 20-58-08](https://user-images.githubusercontent.com/63440984/87853275-c6970800-c943-11ea-89f1-699a788a4dc8.png)
![スクリーンショット 2020-07-18 20-59-03](https://user-images.githubusercontent.com/63440984/87853278-ca2a8f00-c943-11ea-804b-9acd99f06a5b.png)
#### Step.5 AWS Marketplace　を選択して検索欄に　CentOS7　を入力してください
![スクリーンショット 2020-07-18 21-00-48](https://user-images.githubusercontent.com/63440984/87853280-cdbe1600-c943-11ea-93b9-20ef24fe857c.png)
#### Step.6 Continue を選択してください
![スクリーンショット 2020-07-18 21-01-58](https://user-images.githubusercontent.com/63440984/87853282-d0207000-c943-11ea-812d-617f83399686.png)
![スクリーンショット 2020-07-18 21-02-57](https://user-images.githubusercontent.com/63440984/87853284-d282ca00-c943-11ea-92fc-eb9b3411b956.png)
#### Step.7 インスタンスのタイプ：t2.micro vCPU：1 メモリ:1 を選択して　次のステップ：インスタンスの詳細の設定　を選択してください
![スクリーンショット 2020-07-18 21-03-40](https://user-images.githubusercontent.com/63440984/87853286-d6165100-c943-11ea-9b1c-0100d5ce0b8f.png)
#### Step.8 次のステップ：ストレージの追加　を選択してください
![スクリーンショット 2020-07-18 21-04-30](https://user-images.githubusercontent.com/63440984/87853290-e0d0e600-c943-11ea-91a5-075a33578d34.png)
#### Step.9 サイズ（GiB）に　30　を入力して　次のステップ：タグの追加　を選択してください
![スクリーンショット 2020-07-18 21-06-04](https://user-images.githubusercontent.com/63440984/87853295-e62e3080-c943-11ea-90be-e985f3d61f93.png)
#### Step.10 セキュリティグループの設定　を選択してください
![スクリーンショット 2020-07-18 21-07-00](https://user-images.githubusercontent.com/63440984/87853299-e9292100-c943-11ea-8053-8091a2182daf.png)
#### Step.11 確認と作成　を選択してください
![スクリーンショット 2020-07-18 21-09-32](https://user-images.githubusercontent.com/63440984/87853301-ec241180-c943-11ea-8f64-3fb67848f0ea.png)
#### Step.12 起動　を選択してください
![スクリーンショット 2020-07-18 21-10-31](https://user-images.githubusercontent.com/63440984/87853305-efb79880-c943-11ea-933b-c3f6fecc9509.png)
![スクリーンショット 2020-07-18 21-11-51](https://user-images.githubusercontent.com/63440984/87853307-f2b28900-c943-11ea-9f80-f5a79206f716.png)
#### Step.13 新しいキーペアの作成　を選択し、適当なキーペア名を入力後にキーペアのダウンロード　を選択してください
#### Step.14 インスタンスの作成　を選択してください
![スクリーンショット 2020-07-18 21-13-30](https://user-images.githubusercontent.com/63440984/87853309-f8a86a00-c943-11ea-94a8-9d0d6b5587fe.png)
#### Step.15 少し待ちます
![スクリーンショット 2020-07-18 21-14-13](https://user-images.githubusercontent.com/63440984/87853311-fba35a80-c943-11ea-9d82-fe8d6b6898f6.png)
![スクリーンショット 2020-07-18 21-16-14](https://user-images.githubusercontent.com/63440984/87853313-fe9e4b00-c943-11ea-89ef-4983c4c8f261.png)
#### Step.インスタンスの表示　を選択してください
![スクリーンショット 2020-07-18 21-16-50](https://user-images.githubusercontent.com/63440984/87853314-01993b80-c944-11ea-9988-5afccef15ec6.png)
#### Step.16 インスタンスの状態が　running　となっていることを確認してください
![スクリーンショット 2020-07-18 21-17-31](https://user-images.githubusercontent.com/63440984/87853316-03fb9580-c944-11ea-9090-7cee8da26a78.png)
![スクリーンショット 2020-07-18 21-19-09](https://user-images.githubusercontent.com/63440984/87853318-0827b300-c944-11ea-937c-79f9f9029789.png)

#### インスタンスの作成完了です　おめでとうございます！

<br>
<br>

***

## 4. SSH接続、環境設定、アップデート

![スクリーンショット 2020-07-18 21-20-00](https://user-images.githubusercontent.com/63440984/87853320-0a8a0d00-c944-11ea-8bbe-dd662fe4827a.png)
![スクリーンショット 2020-07-18 21-28-38](https://user-images.githubusercontent.com/63440984/87853321-0d84fd80-c944-11ea-8a1f-2e33b4bc5e72.png)
![スクリーンショット 2020-07-18 21-29-19](https://user-images.githubusercontent.com/63440984/87853323-107fee00-c944-11ea-8f94-4a46b8241478.png)
![スクリーンショット 2020-07-18 21-32-12](https://user-images.githubusercontent.com/63440984/87853325-12e24800-c944-11ea-8113-b006f0a511ac.png)
![スクリーンショット 2020-07-18 21-36-41](https://user-images.githubusercontent.com/63440984/87853326-1544a200-c944-11ea-8f65-2c588f2fee67.png)
![スクリーンショット 2020-07-18 21-37-20](https://user-images.githubusercontent.com/63440984/87853328-17a6fc00-c944-11ea-8588-ac6410caa1c3.png)
![スクリーンショット 2020-07-18 21-38-24](https://user-images.githubusercontent.com/63440984/87853329-1a095600-c944-11ea-8cab-b01a90b31109.png)
![スクリーンショット 2020-07-18 21-39-19](https://user-images.githubusercontent.com/63440984/87853330-1d044680-c944-11ea-95bd-02b6ed8b604f.png)
![スクリーンショット 2020-07-18 21-39-35](https://user-images.githubusercontent.com/63440984/87853334-1f66a080-c944-11ea-8047-4ac43d53afaa.png)
![スクリーンショット 2020-07-18 21-50-05](https://user-images.githubusercontent.com/63440984/87853337-22619100-c944-11ea-8648-bbbbf5f05c4f.png)
![スクリーンショット 2020-07-18 21-52-44](https://user-images.githubusercontent.com/63440984/87853338-255c8180-c944-11ea-9e0b-51a0bbbb29db.png)
![スクリーンショット 2020-07-18 21-53-23](https://user-images.githubusercontent.com/63440984/87853341-27bedb80-c944-11ea-9c40-d4f69b37adce.png)
![スクリーンショット 2020-07-18 21-54-04](https://user-images.githubusercontent.com/63440984/87853344-2a213580-c944-11ea-9c36-66517a256c38.png)
![スクリーンショット 2020-07-18 22-04-10](https://user-images.githubusercontent.com/63440984/87853348-2c838f80-c944-11ea-91f3-7d2c841b96e2.png)

***

#### TODO: 資料を纏める
[資料用スクショツイート](https://twitter.com/yotaro__ok/status/1284454044077965313)
<br>
[元ネタツイート](https://twitter.com/yotaro__ok/status/1284115619034484737)
<br>
#### 参考
[miyupaca](https://twitter.com/@miyupacaaa)さんのブログ[2020-07-17 yps学習記録その1](https://paca-gatsby.netlify.app/2020-07-17/)
<br>
[はなえ](https://twitter.com/kon_hanae)さんの纏め[EC2インスタンス作成～SSH接続](https://github.com/hana329/yps/blob/master/task_1.md)
