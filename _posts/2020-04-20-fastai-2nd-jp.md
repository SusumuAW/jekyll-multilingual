---
layout: post
title:  "Fastai2 ２回目　ポスト"
ref: fastai
categories: jekyll update
lang: jp

---

本日は04_mnist_basicsを勉強中です。ここまでのところで、チュートリアルの例として使われている、番号の３と７の判別についてコメントします。
実はこの作業は私の研究に似ているところがあります。例えばMRI画像の中で、脳の部位を自動的に判定する、というのも画像判別の一種です。

例にある「３」の判別をする際、一番わかり易いのが、「３」という形のマスクを作り、それを画像の上に重ねてみる、という作業です。
これにはまず判別しようとする画像の準備が必要かもしれません。例えば、画像のサイズを皆、２８ｘ２８に揃え、できれば数字の位置を真ん中に持ってくる必要があるかもしれません。
その後、「３」の形をしたマスクを重ねた場合、画像が３を示していれば、マスクを重ねても３が認識できるのに対し、画像が７だったら、なんの数字が表示されているのかわからないかもしれません。

コンピューターに判別アルゴリズムを組み込む際、マスクのありなしであまり画像が変化しなければ、そこに示されているのは３である、と言うようなことが可能になります。
同様に、「１」、「２」、「３」、「４」といったすべての数字のマスクをつくり、それぞれをあてはめて、どれが一番変化を起こさなかったかを記録すれば、どの数字でも自動判別できるようになります。

ただ、ここで問題になるのは、どうやってこのマスクを作るのか、という点です。チュートリアルでは、手書きの３の1,000の画像を全て２８ｘ２８のサイズに揃え、単純に皆加算し、それを1,000で割った平均画像をマスクに使う方法を紹介しています。
これは、古典的な工学的手法であり、私達が現在使っているMRIの自動構造認識なども、似たような考えに基づいています。
この古典的なアプローチは、合理的な理論を組み立てて全ての段階を人間が作る、という作業に基づいています。

チュートリアルでは、これは人工知能ではない、と指摘しています。なぜなら、コンピューターが自分で学習する要素がないからです。
ニューラルネットワークを用いたアプローチでは、まずこのマスクをランダム発生します。例えば２８ｘ２８の画像であれば、その一つ一つのピクセルの信号強度を０−１の範囲でランダムに発生させます。
これをマスクと使い、いろいろな数字に当てはめても、全く判別能力はありません。３に当てはめても、７に当てはめても、画像の変化度もランダムでしかありません。ですから、３と７の判別能力はありません。

そこで、このひとつひとつのピクセルの信号強度を少しずつ動かし、３（あるいは７）の識別性能が上がるかをテストします。もし、少し変えてそれで識別能力が上がれば、その方向に動かし続けます。
この「すこし動かし」を２８ｘ２８ピクセル全てに行わないといけないので、大変な作業です。そして、どちらに動かせばいいのか、という指針が必要になります。ここで登場するのが「Gradient]（勾配）というもので、深層学習ににおいて頻出する概念です。

わたしの理解では、ニューラルネットワークにひとつだけのリニアー層を用いると、この作業の結果は上記の平均画像で作ったマスクに非常に似たものになるはずなのですが、それは今後わかることになると思います。
