A feature-rich dictionary lookup program, supporting multiple dictionary formats (StarDict/Babylon/Lingvo/Dictd) and online dictionaries, featuring perfect article rendering with the complete markup, illustrations and other content retained, and allowing you to type in words without any accents or correct case. 

---

## 1. Insatll

安装

```
┌──(nemo@debian)-[~]
└─$ sudo apt install -y goldendict
```

导入字典, 并移除多余的源

> Edit/Dictionaries/Sources/Files/Add

```
┌──(nemo@debian)-[~]
└─$ curl -LO https://github.com/skywind3000/ECDICT/releases/download/1.0.28/ecdict-mdx-28.zip \
&& unzip ./ecdict-mdx-28.zip -d ./dict \
&& mv ~/dict/*.mdx ~/dict/ecdict-mdx-28.mdx \
&& trash ./ecdict-mdx-28.zip
```



---

References

- [goldendict](https://github.com/goldendict/goldendict)
- [goldendict](https://github.com/skywind3000/ECDICT)
