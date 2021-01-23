# 心得：**此代码可以很好地体现了自己数据的分类，既有自训练模型，也有预训练模型，resnet18和resnet101可以随时换着预训练**

## Dependencies:
* Windows10
* python==3.6.10
* > GeForce GTX 1660TI
* pytorch==1.0.0
* torchvision==0.2.1
* cuda100
* numpy==1.19.5

## Visualization Results

* resnet101 训练结果 1

![img1](https://github.com/xiaoxiaokaiyan/Protch_Transfer_learning_Pokmon/blob/main/resnet101%20test.PNG)

* resnet101 训练结果 2

![img1](https://github.com/xiaoxiaokaiyan/Protch_Transfer_learning_Pokmon/blob/main/resnet101%20test%20loss%20and%20acc.PNG)

* resnet101 训练结果 3

![img1](https://github.com/xiaoxiaokaiyan/Protch_Transfer_learning_Pokmon/blob/main/batch.jpg)





## Public Datasets:

* 五种pokemon




## References:
* 深度学习与PyTorch入门实战---龙曲良


## Emphasize:
* pokemon图片在“宝可梦数据集.pdf”百度云盘，下载后文件夹解压出来直接运行程序即可，具体位置看“预训练模型放的位置.PNG”
* train_scratch.py文件是自己训练，train_transfer.py是使用resnet预训练模型
* transfer所使用的预训练模型可以随时更换，具体看“transfer所使用的预训练模型可以随时更换，具体看本图片.PNG”

## Experience：
* 1.device = torch.device('cuda')  x,y = x.to(device), y.to(device)   的效果等同于  x,y = x.cuda(), y.cuda()，而且可以混用
* 2.参数置于cuda和参数置于cpu的两种变量是不能放在一起运算的
* 3.generate_image(D, G, xr.cpu(), epoch)，当xr被置于GPU之后，输出时应该将其.cpu()，重新回到cpu上
* 4.注意加载预训练模型 `resnet18` 和 `resnet101` 的区别！！！！！！！！！！！！！！！！！
```

    model = nn.Sequential(*list(trained_model.children())[:-1], #[b, 512, 1, 1]
                          Flatten(), # [b, 512, 1, 1] => [b, 512]                          ----------------->resnet18(pretrained=True)
                          nn.Linear(512, 5)
                          ).to(device)
                          
    model = nn.Sequential(*list(trained_model.children())[:-1], #[b, 512, 1, 1]
                          Flatten(), # [b, 512, 1, 1] => [b, 512]                          ----------------->resnet101(pretrained=True)
                          nn.Linear(1024, 512)
                          nn.Linear(512, 5)
                          ).to(device)
 

```


