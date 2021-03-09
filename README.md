# 間違えてコミットしてしまった、コミットする前時点に戻したい。
*間違ったコミットを公開していないシナリオ*

>ブラウザから操作
## case01と同じ操作でcase03のリポジトリをフォークする
https://github.com/git-study-session-demo/case03
(略)

>コマンドから操作
## フォークしたリポジトリをローカルにクーロンして、その中に入る

```bash
git clone <your repository url> case03
cd case03
```
### 開発ブランチ01を作成する

```
git switch -c feature/case0301
```
## サンプルファイルを追加して、そのファイルをコミットする

```
touch sample.txt
echo "hello, world" > sample.txt
git add .
git commit -m 'add sample.txt'
```

## sample02.txtとconfig.txt　のサンプルファイルを追加して、そのファイルをコミットする

```
touch sample02.txt
echo "hello, world" > sample02.txt
touch config.txt
echo "個人設定" > config.txt
git add .
git commit -m 'add sample02 file'
```

## config.txt を間違ってコミットしたことをすぐに気付き、そのコミットを取消し
git logコマンドで取り消したいコミットとその直前のコミットのコミットIDを確認する。

```
git log
git reset --hard <取り消したいコミットの直前のコミットのコミットID>
```
そして、再度 sample02.txtのみをコミットする

```
touch sample02.txt
echo "hello, world" > sample02.txt
touch config.txt
echo "個人設定" > config.txt
git add sample02.txt
git commit -m 'add sample02 file'
```

## 開発ブランチをプッシュする

```
git push origin feature/case0301
```
## case01と同様操作で、PRを作成し・マージを行う
(略)  
*mainブランチに sample.txtとsample02.txt ファイルは取り込んでいて、そして config.txt は取り込んでいないことを確認*

## ローカルの開発ブランチを削除

```
git branch -d feature/case0301
```

## 考える
今回のシナリオでは、下記コマンドを実行する前に、コミットした内容をリモート側にプッシュしていません。  
もし、先にプッシュを実行してからコマンドを実行すると、どうなるのでしょうか？
>git reset --hard <取り消したいコミットの直前のコミットのコミットID>
