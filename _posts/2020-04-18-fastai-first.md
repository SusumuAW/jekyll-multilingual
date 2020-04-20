---
layout: post
title:  "Fastai2 First post"
ref: fastai
categories: jekyll update
lang: en
---

I just finished the 02_production section of fastbook and successfully modify the codes to use MR images, instead of images of bears used in this tutorial (https://github.com/fastai/fastbook).

There are several points that I want to mention because I had a hard time to set up the environment. The fastbook recommended to use one of the online services with free GPU times. I tested PaperSpace Gradient. This was very handy because fastai environment is already set up and ready to use. However, I decided to use my workstation, in which I just installed Nvidia 2080ti. Then, the fastbook notebook doesn't run at the first cell because of many missing modules. After many tries and errors, I finally got it working with the following import statements;

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

Please note that in the original fastbook, the first cell is;

---
from utils import *  
from fastai2.vision.widgets import *  
---

Apparently, I need to not only download many Python modules with "conda install xxx" or "pip3 install xxx", but also download python files from fastai2 and fastcore from github, as you can see that I needed to specify the path to fastai2 and fastcore in my computer directories.

This step could be hard for beginners who do not know, for example, what is github, but I guess there is no other ways but keep trying to learn things. It won't be hard as much as you would imagine but you do need patience just like learning new languages.

Once past this phase, the rest of the fastbook 02_production section is simple; just follow the contents and there should not be any errors.

The modifications of the contents for MR images were also straightforward. Instead of teddy, black, and grizzly bears, I use axial, sagittal, and coronal images from one 3D MRI volume. Just using the CNN example in the tutorial book, I got almost perfect prediction. There were some errors but they are all because the slices didn't contain the brain or at the very edges of the brain.

I also needed to turn off the data augmentation and random sized crop for some reason, but I guess we don't need these for MRI images for now except for the consistent resizing because we can assume that FOVs for MRI are consistent in a way that always covers the brain well.
