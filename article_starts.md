# gif的压缩策略以及代码实践

- 图像的压缩过程中的色彩变化
- dpi 像素点

## 图像的压缩过程中的色彩变化
  在执行网络代码时，出现了一个这样的情况， 全彩的gif图经压缩变化后，色彩出现了重大变故，尚不知具体原因。

代码如下:

```
def compressImg(ImgName):
    im = Image.open(ImgName)
    im.convert('RGB')
    if max(im.size[0], im.size[1]) > 128:
        im.thumbnail((128, 128))
    im.save('f-' + ImgName, quality=50)
    return 'OK'
```
  采用Image库中 covert方法直接转化图片的色彩属性，然后用thumbnail方法裁剪图片大小，最后储存
  可以看出这是一个比较简单的压缩转化过程，并未涉及到具体的原子层面的改造细节。
> 知其然，而不知其所以然

对此，要探讨的范围
如果过广， 超出已有的知识面，精力受限，难以为继<br>
如果过深， 则超出自己的理解程度，学识有限，同样难以为继

所以，应当限定在：
1. 仅就Image库的个别函数方法开始研究
2. 对单个知识点进行渗透


