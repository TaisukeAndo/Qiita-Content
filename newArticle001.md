---
title: newArticle001
tags:
  - ''
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
# new article body

# Git&GitHub環境構築マニュアル

---

GitとGithubの習得はIT企業で仕事をするのにはマストです。システム開発に携わるエンジニアとなる人は必ずマスターしましょう！

株式会社DREAMSQUARE CTO 安藤太亮

# 準備

---

本記事は、GitやGithubの概念についての理解があることを前提でGitとGithubの使い方の説明を行っています。バージョン管理の概念やGitの仕組みなどについては以下の動画を参考に学習を行ってください。

[https://www.youtube.com/watch?v=yzNPC_QzgFM](https://www.youtube.com/watch?v=yzNPC_QzgFM)

# インストール

---

## １．VsCodeのインストール

以下のリンクからVscodeをインストールします。すでに、インストールをしている人は次に進んでください。

[](https://code.visualstudio.com/download)

## ２．Gitのインストール

以下のリンクから、使用している環境に合ったGitのインストーラーをダウンロードして、インストールしてください。

[Git - Downloads](https://git-scm.com/downloads)

# Gitの設定

---

## １．VsCodeでGitBashを起動

VsCodeでターミナル（Terminal）を起動します

![Untitled](Git&GitHub%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89%E3%83%9E%E3%83%8B%E3%83%A5%E3%82%A2%E3%83%AB%201bf757f0fe01436e8ca5eaa4cae089b2/Untitled.png)

起動したターミナルの右端にある、ターミナルの追加の選択から「GitBash」を選択します。

![Untitled](Git&GitHub%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89%E3%83%9E%E3%83%8B%E3%83%A5%E3%82%A2%E3%83%AB%201bf757f0fe01436e8ca5eaa4cae089b2/cd2ade05-dc16-4e7e-bccd-d0912ba6de52.png)

## ２．Gitのユーザー登録

ユーザー名を登録します。ここでは、社内の誰が見ても個人を認識できる名前を設定してください。「example-name」の部分にユーザー名を入力してGitBashのコマンドラインで実行してください。

```bash
git config --global user.name example-name
```

次に、メールアドレスを設定します。「example@mail.com」の部分に個人のメールアドレスを入力してGitBashのコマンドラインで実行してください。

```bash
git config --global user.mail example@mail.com
```

（省略可）最後に、上で入力したユーザー名とメールアドレスが正しく登録されていることを以下のコマンドを実行して確認してください。

```bash
git config --list
```

※コマンドを実行すると、下のほうに「:」が表示される場合があります。この表示があるときは、「下矢印キー」を押すと表示をスクロールすることができます。

※表示を終了するときは「Qキー」を押してください。

# GitHubの設定

---

## ０．アカウント作成

ここでは、社用のGitHubアカウントがある前提で説明します。アカウントをまだ持っていない人は以下のリンクからアカウントの作成を行ってください。

[GitHub でのアカウントの作成 - GitHub Docs](https://docs.github.com/ja/get-started/start-your-journey/creating-an-account-on-github)

## １．SSHキー（秘密鍵・公開鍵）の生成

まず初めにSSHキーを生成します。下記のコマンドの「example@mail.com」を自分のメールアドレスに書き換えて実行してください。この時、「Enter file in which to save the key」と表示されるのでEnterキーを押してください。すると、「Created directory」の欄に鍵の保存先が表示されます。次に、パスフレーズ（パスワードのようなもの）の入力を求められます。「Enter passphrase」に続いて任意のパスフレーズを入力してEnterキーを押してください。

```bash
ssh-keygen -t ed25519 -C "example@mail.com"
```

※パスフレーズは入力しても画面上には何も表示されません。

※パスフレーズは同じものを２回入力する必要があります。

## ２．公開鍵をコピー

次に、生成したSSHキーのうち、公開鍵をクリップボードにコピーします。OSの種類によってコマンドが異なるので実行する際には注意してください。実行する際は、「example/.ssh」の部分をSSHキーを生成する際に確認した鍵の保存先のパスに書き換えてください。

### Windows

```bash
Clip < example/.ssh/id_ed25519.pub
```

### macOS

```bash
pbcopy < example/.ssh/id_ed25519.pub
```

## ３．公開鍵をGitHubに登録

以下のリンクにアクセスしてGitHubのSSHキーの登録画面を開きます。

[](https://github.com/settings/ssh/new)

![Untitled](Git&GitHub%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89%E3%83%9E%E3%83%8B%E3%83%A5%E3%82%A2%E3%83%AB%201bf757f0fe01436e8ca5eaa4cae089b2/Untitled%201.png)

画面を開いたら、「Title」、「Kye」をそれぞれ設定します。「Title」には任意の全角半角文字列を設定できます。「Kye」にはうえでコピーした公開鍵を張り付けてください。入力が終わったら、「Add SSH Kye」を押して登録を完了してください。

※KyeTypeは「Authentication Key（認証キー）」と「Signing Key（署名キー）」の２種類選択できますが、ここでは認証を行うための公開鍵を登録するので、デフォルト「Authentication Key」にしてください。

## ４．GitとGithubのSSH接続

以下のコマンドをコマンドライン上に入力しSSH接続を行ってください。実行すると、「Are you sure you want to continue connectiong（yes/no）?」が表示されるので、「yes」と入力してEnterキーを押してください。その後、上で設定したパスフレーズを入力してEnterキーを押してください。「You’ve successfully authenticated」と表示されたら接続成功です。

```bash
ssh -T git@github.com
```

※パスフレーズは入力しても画面上には何も表示されません。

# リモートリポジトリの登録

---

ここでは、Gitによるローカルでのバージョン管理および、GitHubを用いた共同開発のプロジェクトを立ち上げる際の手順を説明します。すでに社内で進行中のプロジェクトに参加する際は（２）から作業を進めてください。

## １．GitHub上でリポジトリを新規作成

以下のリンクにアクセスして、リモートリポジトリを新規作成します。

[](https://github.com/new)

![Untitled](Git&GitHub%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89%E3%83%9E%E3%83%8B%E3%83%A5%E3%82%A2%E3%83%AB%201bf757f0fe01436e8ca5eaa4cae089b2/Untitled%202.png)

アクセスできたら、「Repository name」、「公開設定」をそれぞれ設定します。「Repository name」には半角の文字列を設定してください。「公開設定」はリポジトリの用途に合わせて設定してください。一般向けに公開する場合は「Public」、社内作業に使用する場合は「Private」に設定してください。入力が完了したら、「Create repository」を押してください。

※「Description」は任意でリポジトリの説明（全角半角）を追加できます。

## ２．GitHubとGitのリポジトリを同期

リポジトリの作成が完了したら遷移する以下の画面から、「HTTPS・SSH」を「SSH」に設定して、右側に表示されたコードをコピーします。

![Untitled](Git&GitHub%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89%E3%83%9E%E3%83%8B%E3%83%A5%E3%82%A2%E3%83%AB%201bf757f0fe01436e8ca5eaa4cae089b2/Untitled%203.png)

次に、ローカルリポジトリにリモートリポジトリを登録します。以下のコマンドの「git@github.com:example/Project.git」を上でコピーしたSSHリンク（すでにリポジトリがある場合は、社内で指定されたSSHリンク）に書き換えて実行してください。

```bash
git remote add origin git@github.com:example/Project.git
```

（省略可）正しく登録されていることを確認するため、以下のコマンドを実行してください。正常に登録されている場合、上で設定したSSHリンクが「fetch」と「push」の２種類表示されます。

```bash
git remote -v
```

## ３．ローカルリポジトリの作成

バージョン管理の対象となるディレクトリを作成したいフォルダの階層に移動します。下記のコマンドの「example/」の部分に相対パスもしくは絶対パスを入力して実行してください。

```bash
cd example/
```

次に、バージョン管理の対象となるディレクトリを作成します。下記コマンドの「example」の部分に任意の名前を設定してください。

```bash
mkdir example
```

最後に、上で作成したディレクトリに移動してローカルリポジトリを作成します。下記の「example」の部分を上で設定したディレクトリ名に書き換え、実行してください。

```bash
cd example
git init
```

バージョン管理の対象とするファイルはすべて上で設定したディレクトリ「example（任意の名前）」上に作成してください。

# ファイルの編集

---

以下の手順をファイルの編集を行う度（適当なタイミング）に実行することでバージョン管理を行います。

## １．ブランチの作成

まず初めに、ブランチを作成します。以下のコードの「example」を任意の半角文字列に設定して実行してください。

```bash
git branch example
```

次に、作成したブランチに切り替えます。以下のコマンドの「example」に上で作成したブランチの名前を入力して実行してください。

```bash
git checkout example
```

※README.mdに限らず、すべての編集を行う際は必ずブランチの作成（masterブランチからの切り替え）を行ってください。

## ２．README.mdの作成

ローカルリポジトリ上に「README.md」を作成します。「README.md」はリポジトリの説明書（マニュアル）のようなものであり、リポジトリを新規作成する際は必ず作成しましょう。

![Untitled](Git&GitHub%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89%E3%83%9E%E3%83%8B%E3%83%A5%E3%82%A2%E3%83%AB%201bf757f0fe01436e8ca5eaa4cae089b2/Untitled%204.png)

作成したら、コマンドライン上で「README.md」をステージングエリアに追加します。

```bash
git add README.md
```

※拡張子の入力は必須です。

※コミットする対象のファイルが複数ある場合は、ずべてのファイルをステージングエリアに追加してください。

（省略可）次に、対象のファイルがステージングエリアに登録されていることを確認します。下記のコマンドを実行し、上で登録したファイルがすべて表示されていることを確認してください。

```bash
git status
```

次に、ステージングエリアに登録したファイルをコミットします。実行する際は、必ずコミットメッセージを書き換えてください。

```bash
git commit -m"README.mdの作成"
```

## ３．リモートリポジトリに変更を同期

始めに、以下のコマンドを実行してマスターブランチに切り替えます。

```bash
git checkout master
```

次に変更した内容をリモートリポジトリ転送します。以下のコマンドの「example」を上で作成したブランチの名前に書き換えて実行してください。

```bash
git push origin example
```

次にプルリクエストを作成します。Githubの「Code」画面に表示されている「Compare&pull request」をクリックします。

![Untitled](Git&GitHub%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89%E3%83%9E%E3%83%8B%E3%83%A5%E3%82%A2%E3%83%AB%201bf757f0fe01436e8ca5eaa4cae089b2/Untitled%205.png)

遷移した画面から「Add a description」に変更の詳細を記入して「Create pull request」をクリックします。

![Untitled](Git&GitHub%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89%E3%83%9E%E3%83%8B%E3%83%A5%E3%82%A2%E3%83%AB%201bf757f0fe01436e8ca5eaa4cae089b2/Untitled%206.png)

共同編集を行っているチームメンバーに変更内容のフィードバックをもらい、確認が取れたらマージします。以下の画面の「Merge pull request」をクリックしてください。最後に遷移した画面の「Confirm merge」をクリックして完了です。

![Untitled](Git&GitHub%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89%E3%83%9E%E3%83%8B%E3%83%A5%E3%82%A2%E3%83%AB%201bf757f0fe01436e8ca5eaa4cae089b2/3f7b3270-b5ea-461a-8a4e-e3532d1a9caa.png)

## ４．ローカルリポジトリの更新

最初に、以下のコマンドを実行して、マスターブランチに切り替えます。

```bash
git checkout master
```

次に、以下のコマンドを実行してリモートリポジトリの変更をローカルリポジトリに反映（プル）します。

```bash
git pull origin master
```

# 付録

---

## 絶対に覚えてほしいコマンドリスト

下記のリストはPowerShellやコマンドプロンプトなど、他のコマンドラインでも共通で使えるものがほとんどです。

| cd | ディレクトリの移動 |
| --- | --- |
| mkdir | 新しいディレクトの作成 |
| dir | ファイルの一覧を表示 |

## よく使うGitBashコマンドリスト

Gitを業務で使用する際に、最低限覚えておく必要のあるコマンドリストです。

| git branch | ブランチの確認・作成 |
| --- | --- |
| git checkout | ブランチの切り替え |
| git add | ステージングエリアに登録 |
| git commit | ステージングエリアに登録した内容をコミット |
| git push | ローカルリポジトリの変更をリモートリポジトリに反映 |
| git pull | リモートリポジトリの変更をローカルリポジトリに反映 |

## 覚えておくと便利な機能

下記の内容を覚えて活用できるようになると、仕事の効率が上がります。

| *（アスタリスク） | アスタリスクは任意の半角文字列を表します。アスタリスクを使用することで、長いファイル名を入力する手間を省けます。
（使用例：cd *.c / git add file_*.txt） |
| --- | --- |
| 上下矢印キー | コマンドライン上で、過去に入力したコマンドをもう一度実行する際に、上下の矢印キーを使用することで、コマンドを遡って再度表示させることができます。 |
| git reset HEAD | ステージングエリアへの登録を取り消すコマンド |
| git git reset --soft HEAD^ | 直前のコミットをなかったことにするコマンド |
| git merge master | 移動先のブランチにマスターブランチの内容を反映（マージ）するコマンド |

# 参考文献

---

[イケてるレポジトリのREADME.mdには何を書くべきか - Qiita](https://qiita.com/autotaker1984/items/bce70c8c67a8f6fb1b9d)

[Git - Reference](https://git-scm.com/docs)

# 更新履歴

---

| 2024/4/1 | 記事の完成 |
| --- | --- |
|  |  |
|  |  |