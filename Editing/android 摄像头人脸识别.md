**搜索： android 摄像头人脸识别**
- [Android中的人脸检测（静态和动态）](https://blog.csdn.net/zhandoushi1982/article/details/8613916)。
  +  Google 于2006年8月收购Neven Vision 公司 （该公司拥有10多项应用于移动设备领域的图像识别的专利），以此获得了图像识别的技术，并加入到android中。
  + Android 中的人脸识别技术，用到的底层库：android/external/neven/，framework 层：frameworks/base/media/java/android/media/FaceDetector.java。
  + 引申：
    - [Android人脸检测类FaceDetector](https://www.cnblogs.com/feisky/archive/2010/09/12/1824320.html)。
      + 根据文档描述，输入图片必须为Bitmap RGB565格式。
      + 实际上，FaceDetector检测到的并不是人的全脸，而只是双眼。
      + 实际测试中，发现图片太小的话检测不到人脸，试验中使用小于100x100的图片检测不到人脸，但是由于Android内存有限，图片太大的话，会出现无法加载图片的异常。
  
- 无意发现：
  + [90后技术宅研发Magi一夜爆红，新一代知识化结构搜索新时代来了？](https://blog.csdn.net/dQCFKyQDXYm3F8rB0/article/details/102982005)。
    - [Magi](https://magi.com/)。
    - Magi 是由 Peak Labs 从无到有自研的基于机器学习的信息抽取和检索系统。
    - 将文本中的知识提取成结构化的数据，通过终身学习持续聚合和纠错，提供可解析、可检索、可溯源的知识体系。
    - 不仅收录互联网上的海量文本，还会去尝试理解并学习这些文本中蕴含的知识和数据。
    - 学习过程是在无人干预的情况下 7 x 24 小时不间断运行。
    - 互联网数据浩如烟海，质量参差不齐。
    

