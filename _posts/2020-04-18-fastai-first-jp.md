---
layout: post
title:  "Fastai2 チュートリアル　初回ポスト"
ref: fastai
categories: jekyll update
lang: jp

---

数日前からFastaiのチュートリアルサイトを使ってディープラーニングの勉強をしております（https://course.fast.ai/）。
現在02_02_productionのセクションなのですが、例として使っている三種類のクマの映像の判別を、さっそく本職であるMRIの映像判別に置き換えて試してみました。
映像判別と言っても、三種類の映像方向（Axial, Sagittal, coronal）の判別で、一つの３D画像から作った数百枚ずつのスライスを使っただけですが。
意外と簡単にこの変更ができ、結果もほとんど１００％正確でした。最もトレーニングデータを使ってテストしたのでチーティングですけど。

この過程で、一番苦労したのが最初の環境設定です。
このチュートリアルでは、オンラインサービスでGPUが使えるサイトを使うことを推奨しています。わたしも最初はそのうちの一つ、PaperSpace Gradientを使いました。
このサイトでは、すでにFastai2がすべてインストールされている環境を選べ、チュートリアルがそのまま走ります。
しかし、私はUbuntuワークステションにせっかくNvidia2080Tiをセットしたばかりでしたので、これを使うことにしたのですが、環境設定に手間取りましたので、その経験を述べたいと思います。

結果から先にいうと、Jupyter Notebookの最初のセルの設定は下記で動きました。

---
import sys sys.path.append('pass_to/fastai_DL/fastbook/')  
sys.path.append('pass_to/fastai2/')  
sys.path.append('pass_to/fastcore/')  
from fastai2 import *  
from fastcore import *  
from utils import *  
from fastai2.vision.widgets import *  
from fastai2.data import *  

---

ちなみに、チュートリアルでは、対応するオリジナルのセルは;

---
from utils import *  
from fastai2.vision.widgets import *  

---

と非常にシンプルです。
これをこのまま使おうとすると、芋づる式に足りないModuleが出てきます。
これを説明しますと、まず、三種類のライブラリーをGitHubからダウンロードする必要があります。まずFastbookですが、これはチュートリアルそのものですので、これはすでにダウンロードしてあるはずです。
次の2つ、Fastai2とFastcoreというのが別途必要となります。これらのダウンロード場所をsys.pathという機能をつかってNotebookに知らせます。
これにより、それに続く5行のImport機能が正常に働きます。

ただ、最初にこのセルを入力しますと、XXXモジュールがない、というエラーが続きます。そのたびに、"conda install xxx" や "pip3 install xxx"を使ってModulesをくみこむ必要があります。
私も初心者ですが、はじめたばかりの人にとって、「GitHubからダウンロード」と聞いただけで、ナンノコッチャと思われるかもしれませんが、こればかりは習うより慣れろ、でトライし続ける以外にありません。

これさえ終われば、あとの「クマ判別」はそのまま動くはずです。わたしのMRIスライス判定も、クマの絵をMRI画像に置き換えるだけで、そのまま動きました。
すごいですね、おどろきました。
最も、どういうわけか、画像クロップやAugementationは取り除かないとエラーがでました。もともと脳の画像は全てにおいて脳がちゃんと画像に入ってますし、何かに隠れているとか、一部しか写ってない、ということはありえないと仮定できるので、これらのトリックは必要ないと思います。
