# Text Block Segmentation Competition ICPR2020

The code for the ICPR 2020 [Text BLock Segmentation Competition](https://www.mathematik.uni-rostock.de/forschung/projekte/citlab/projects/text-block-segmentation-competition-icpr2020/competition-details/). 

[Results](https://www.mathematik.uni-rostock.de/forschung/projekte/citlab/projects/text-block-segmentation-competition-icpr2020/results/):

|             | F-Value Simple Track | F-Value Complex Track|
| ----------- | -------------------- | -------------------- |
| CITlab      | 0.934                | 	0.768               |
| Luan Pham [^1] and Tuan Anh Tran [^1] [^2]   | 0.999         | - |
| **Davood Wadi** [^3] | **0.995**                |  **0.887**               |
| Xinfeng Chang [^4], Luyan Wang [^4], Hui Li [^4], Adam Wu [^4] and Lianwen Jin [^5] | 0.997 | 0.954 |

The goal of participating in the competition is to show that simple DL architectures, such as Mask R-CNN, coupled with mainstream image augmentations, can produce competitive results (even better results) than traditional computer vision techniques that require heavy feature engineering and extensive domain knowledge.

[Dataset](https://www.mathematik.uni-rostock.de/forschung/projekte/citlab/projects/text-block-segmentation-competition-icpr2020/downloads/)

## Method

I used deep neural nets, namely Mask R-CNN, for instance segmentation to detect regions of different text blocks using the provided training datasets, independently for the simple and complex tasks.

First, I converted all the regions in the training sets to alpha mask images, in order to make them compatible for the intended deep learning architecture. The code can be found [here](https://github.com/davoodwadi/ICPR2020-TextBlockSegment/blob/master/extracting_masks-complex.ipynb).

To avoid overfitting, I used fastai (v1)’s amazing image and mask [transformation library](https://fastai1.fast.ai/vision.transform.html) that enabled data augmentation using tensor operations for masks without distorting their color coding.

After the model was trained, I used the predicted masks (arrays of the same size as the input image that have values of 1’s for the recognized text block and 0’s everywhere else) for the test sets to determine for each baseline which mask contains the largest number of the baseline points. All the points that matched a specific mask received the ArticleID of that mask. The Article IDs were named arbitrarily, as pointed out by the organizers of the competition, while remaining unique. I followed the naming convention of the training sets, i.e. the ArticleIDs starting with “a1” and building up to “an” for “n” regions. The points that didn’t fall into any mask received their unique ArticleID. This procedure ensured that a single baseline point will not fall into two categories at the same time. To set the ArticleIDs and save them in pageXML format, I used the [handy tool](https://github.com/CITlabRostock/citlab-python-util/tree/master/citlab_python_util/parser/xml/page) provided by the organizers.



[^1]: Cinnamon AI
[^2]: Ho Chi Minh City University of Technology (HCMC University of Technology)
[^3]: École des Hautes Études commerciales Montreal (HEC Montréal)
[^4]: Lenovo Research
[^5]: South China University of Technology (SCUT)
