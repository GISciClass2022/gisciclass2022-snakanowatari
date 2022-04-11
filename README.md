# 2022地理情報科学特論
この講義では地理情報科学に関する研究課題を理解し、Geocomputationalに地理情報の処理ができるようになることを目標とする。


## 講義スライド
TBD
## 準備
- [git](https://git-scm.com/downloads)のインストール
- [github cli](https://cli.github.com)のインストール
- [Github](https://github.com/) アカウント登録（なければ）
- [Docker](https://docs.docker.com/get-docker/)のインストール
- [VScode](https://code.visualstudio.com)のインストール
- VScodeを立ち上げて、Docker, Git extension packのExtensionsもインストール
- Github classroomの登録
- Assignmentのクローン（各自PC内。下記、環境構築を参照のこと）

## 成績評価
演習の課題（自由課題）を持って評価する。
Rmarkdownにより記述した再現可能な（コードを含めた）研究レポート（テーマの背景・分析手法・結果・考察・結論）を作成したレポジトリを提出する。

### 評価基準
- 課題設定の難易度
- レポートの完成度
- コードの可読性
- 正確性
- 再現可能性

## スケジュール
1. イントロダクション・環境構築
2. Reproducible research（１）
3. Reproducible research（２）
4. Rの導入（１）
5. Rの導入（２）
6. ジオコンピュテーション（１）
7. ジオコンピュテーション（２）
8. ジオコンピュテーション（３）
9. ジオコンピュテーション（４）
10. 地図化（１）
11. 地図化（２）
13. 演習（１）
14. 演習（２）
15. 演習（３）←課題提出

## References
すべてオンラインで閲覧可能である。
### 教科書
- [An Introduction to R](https://intro2r.com)
- [geocomputation with R](https://geocompr.robinlovelace.net/)
それぞれ`Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License`である.

### 参考資料
GIScience
- [Spatial Data Science](https://keen-swartz-3146c4.netlify.app/)
- [geospatial analysis](https://spatialanalysisonline.com/HTML/index.html)
- [Spatio-Temporal Statistics with R](https://spacetimewithr.org/)

Basic R and GIS
- [R for data science](https://r4ds.had.co.nz/)
- [GISオープン教材](https://gis-oer.github.io/gitbook/book/)



## 環境構築
関連アプリケーションがインストールできたら、レポジトリをダウンロードし、Dockerコンテナを構築する。

```
1 github cliでgithubにPCを登録する。
gh auth login
# その後対話的に処理を実行し、登録する
2 自身の好きな場所で本レポジトリをクローンする
gh repo clone 2022ISci_class/XXXXXXX #XXXXXXXは各自のものに置き換えること！
# もしくは git clone https://github.com/2022GISci_class/XXXXXXX.git
3　ダウンロードしたレポジトリに移動する
cd 2022GISci_class
4 自身の環境に応じてdocker-compose.ymlを作成する。
mac m1チップであればdocker-compose_m1.ymlをdocker-composeに、
それ以外であれば docker-compose_x86_64.ymlをdocker-composeとする
5 dockerコンテナを立てる
docker-compose up -d --build
```

上記の設定ができたら、VScodeのDockerエクステンションより、`Open by browser`をクリックするとRstudio serverが立ち上がる。
もしくは``` http://localhost:8080 ```とブラウザで指定する。
userは`rstudio`, passwordは`passwd`である。


## 参考
その他、簡易的にgeocomputation with Rの実行環境にアクセスする方法としては、
[binder](https://mybinder.org/v2/gh/robinlovelace/geocompr/master?urlpath=rstudio)、もしくは[Rstudio cloud](https://rstudio.cloud/project/1642300)がある。
しかしながら、環境としては課題実行には向いていない。
