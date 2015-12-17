---
title: win10上微信撤回图片恢复
---

#{{ page.title }}

    
    今天无意中看到同学利用网页版获得了撤回图片的缩略图（后来得知的）。然后我就非常好奇，如何能获取别人撤回的图片，在经过不断尝试在，确定文件目录为：C:\Users\xxx\Documents\WeChat Files。突然间发现，在yyy/Data下有着与图片大小类似的文件。于是在好奇之下，将他们拷贝了出来。再根据图片大小比对，发现那些文件基本可以断定为是图片，然后找到别人发送的原图进行比较，发现大小一模一样，但是我就是打不开！怀疑仅仅是通过xor加密。打开文件，对二者进行比对，发现00全部变为3f，基本可以断定为xor 3f加密。随即测试了另外一个数据，发现符合。
    最后使用C语言写了一个简易的xor解密程序进行解密, 成功得到原图。C语言代码如下：
#include<cstdio>
int main()
{
	char s[256];
	gets(s);
	freopen(s, "rb", stdin);
	freopen("a.jpg", "wb", stdout);
	char c;
	while (fread(&c, 1, 1, stdin)) 
{
		c = c ^ 0x3f;
		fwrite(&c, 1, 1, stdout);
	}
	fclose(stdin);
	fclose(stdout);
	return 0;	
}





{{ page.date|date_to_string }}
