字典生成。

# 1 使用

生成 1-8 位密码字典，字符集合为小写字母，从 a 开始到 zzzzzzzz 结束

```shell
┌──(root㉿a-kali-23)-[~]
└─# crunch 1 8
```

生成 1-6 位的密码字典，字符集合为 abcdefg ，从 a 开始到 gggggg 结束

```shell
┌──(root㉿a-kali-23)-[~]
└─# crunch 1 6 abcdefg
```

生成指定字符串，比如生日的日期（%代表数字）

```shell
┌──(root㉿a-kali-23)-[~]
└─# crunch 8 8 -t 199307%% -e 19930730
```

生成元素的组合，比如 123.com

```shell
┌──(root㉿a-kali-23)-[~]
└─# crunch 7 7 -t %%%.com -s 111.com -e 123.com
```

在字典中输出特殊字符

```shell
┌──(root㉿a-kali-23)-[~]
└─# crunch 3 3  abc -t @@@ -l @aa
```

以元素组合生成字典 zhangsan 1993 0701

```shell
┌──(root㉿a-kali-23)-[~]
└─# crunch 4 4 -p zhangsan 1992 0701
```

**自定义字符集合**

创建自定义字符集合

```shell
┌──(root㉿a-kali-23)-[~]
└─# vim /usr/share/crunch/charset.lst
```

```
# charset configuration file for winrtgen v1.2 by Massimiliano Montoro (mao@oxid.it)
# compatible with rainbowcrack 1.1 and later by Zhu Shuanglei <shuanglei@hotmail.com>

test                          = [123abc]

hex-lower                     = [0123456789abcdef]
hex-upper                     = [0123456789ABCDEF]

numeric                       = [0123456789]
numeric-space                 = [0123456789 ]
```

使用 test 字符集生成 *.com 文件

```shell
┌──(root㉿a-kali-23)-[~]
└─# crunch 5 5 -f /usr/share/crunch/charset.lst test -t @.com
```

# 2 帮助

查看帮助

```shell
┌──(root㉿a-kali-23)-[~]
└─# crunch -h
```

```
crunch 版本 3.6

Crunch 可以根据您指定的标准创建词表。crunch 的输出可以发送到屏幕，文件，或其它程序。

Usage: crunch <min> <max> [options]
其中 min 和 max 是数字

有关如何使用 crunch 的说明和示例，请参阅手册页面。
```

查看手册

```shell
┌──(root㉿a-kali-23)-[~]
└─# man crunch > crunch.txt && cat crunch.txt
```

```
CRUNCH(1)         General Commands Manual         CRUNCH(1)

NAME
       crunch - 根据字符集生成字表

SYNOPSIS
       crunch  <min-len>  <max-len> [<charset string>] [op‐
       tions]

DESCRIPTION
       crunch 可以根据您指定的标准创建词表。
       crunch 的输出可以发送到屏幕，文件，或其它程序。
       
       所需参数为：

       min-len
              设定最小字符串长度（必选）。

       max-len
              设定最大字符串长度（必选）。

       charset string
              您可以使用的字符集。
              若留空，将使用默认的字符集。
              顺序必须是小写字母、大写字母、数字，然后是符号。
			  如果不按此顺序操作，就无法获得想要的结果。
			  必须指定字符类型的值或正号。
			  注意: 如果您想在字符集中包含空格字符，则必须使用 \ 或用引号将字符集括起来，例如 "abc "。
			  参见示例 3、11、12 和 13。

OPTIONS

       -b number[type]
              指定输出文件的大小，仅在使用 -o START 时才有效。
              输出文件的格式为开头字母-结尾字母，例如：crunch 4 5 -b 20mib -o START 将生成 4 个文件：aaaa-gvfed.txt, gvfee-ombqy.txt, ombqz-wcydt.txt, wcydu-zzzzz.txt 单位是 kb, mb, gb, kib, mib,和 gib。
              前三种单位基于 1000 字节，后三种则基于 1024 字节。
              注意：数字和单位之间没有空格。
              例如：500mb 是正确的，500 mb 是不正确。

       -c number
              指定向输出文件写入的行数,仅在使用 -o START 时有效。
              输出文件的格式为起始字母-结束字母 例如：crunch 1 1 -c 60 -o START 将产生 2 个文件：a-7.txt 和 8-\  .txt。
              在第二个文件名中使用斜线的原因是，结尾字符是空格，ls 必须将其转义才能打印出来。
              是的，指定文件名时，您需要输入 \ ，因为最后一个 字符是空格。

       -d numbersymbol
              限制重复字符的数量。
              -d 2@ 限制小写字母的输出，如 aab 和 aac。
              不会生成 aaa，因为这是 3 个连续的字母 a。
              格式为先数字后符号，其中数字是最大连续字符数，symbol 是要限制的符号。
              例如：@,%^。
              参见示例 17-19

       -e string
              指定何时停止生成

       -f /path/to/charset.lst charset-name
              指定 charset.lst 中的字符集

       -i     倒置输出结果，因此输出结果不再是 aaa,aab,aac,aad 等，而是 aaa,baa,caa,daa,aba,bba, 等。

       -l     使用 -t 时，会告诉 crunch 应将哪些符号视为字面意义。
              这样您就可以将占位符作为字母。
              -l 选项的长度应与 -t 选项的长度相同。
              参见示例 15。

       -m     与 -p 合并。请使用 -p 代替。

       -o wordlist.txt
              指定输出结果的文件，
              例如：wordlist.txt

       -p charset OR -p word1 word2 ...
              告诉 crunch 生成没有重复字符的单词。
              默认情况下，crunch 会生成一个大小为字符集中的字符数^最大长度。
              该选项将生成字符集中的字符数
              ! 代表阶乘。
              例如，字符集为 abc，最大长度为 4。
              Crunch 默认会生成 3^4 = 81 个单词。
              该选项将生成 3 = 3x2x1 = 6 words (abc,acb,bac,bca,cab,cba).
              这一定是最后一个选项！
              该选项不能与 -s 一起使用，而且会忽略最小和最大长度，但仍必须指定两个数字。

       -q filename.txt
              告诉 crunch 读取 filename.txt，并对读取的内容进行置换。
              该选项与 -p 选项类似，但它从 filename.txt 获取输入信息。

       -r     告诉 crunch 从中断的地方继续生成单词。
              只有使用 -o 时，-r 才起作用。
              您必须使用与原始命令相同的命令。
              唯一的例外是 -s 选项。
              如果原始命令中使用了 -s 选项，则必须在恢复会话前将其删除。
              只需在原命令末尾添加 -r。

       -s startblock
              指定起始字符串，例如：03god22fs

       -t @,%^
              指定一个模式，例如 @@god@@@@ 其中只有 @'s, ,'s, %'s, 和 ^'s 会发生变化。
              @ 将插入小写字母
              , 将插入大写字母
              % 将插入数字
              ^ 将插入符号

       -u
              选项 -u 会禁用 printpercentage 线程。
              这应该是最后一个选项。

       -z gzip, bzip2, lzma, and 7z
              压缩-o 选项的输出结果。
              有效参数为 gzip、bzip2、lzma 和 7z。
              gzip 的速度最快，但压缩效果很小。
              bzip2 比 gzip 稍慢，但压缩效果更好。
              7z 的速度最慢，但压缩效果最好。

EXAMPLES
       Example 1
       crunch 1 8
       crunch will display a wordlist that starts at a  and
       ends at zzzzzzzz

       Example 2
       crunch 1 6 abcdefg
       crunch  will  display a wordlist using the character
       set abcdefg that starts at a and ends at gggggg

       Example 3
       crunch 1 6 abcdefg\
       there is a space at the end of the character string.
       In order for crunch to use the space you  will  need
       to escape it using the \ character.  In this example
       you could also put quotes around the letters and not
       need  the \, i.e. "abcdefg ".  Crunch will display a
       wordlist  using  the  character  set  abcdefg   that
       starts at a and ends at (6 spaces)

       Example 4
       crunch 1 8 -f charset.lst mixalpha-numeric-all-space
       -o wordlist.txt
       crunch will use the mixalpha-numeric-all-space char‐
       acter  set  from  charset.lst  and  will  write  the
       wordlist to a file  named  wordlist.txt.   The  file
       will start with a and end with "        "

       Example 5
       crunch 8 8 -f charset.lst mixalpha-numeric-all-space
       -o wordlist.txt -t @@dog@@@ -s cbdogaaa
       crunch  should generate a 8 character wordlist using
       the  mixalpha-number-all-space  character  set  from
       charset.lst  and  will  write the wordlist to a file
       named wordlist.txt.  The file will start at cbdogaaa
       and end at "  dog   "

       Example 6
       crunch 2 3 -f charset.lst ualpha -s BB
       crunch with start generating a wordlist  at  BB  and
       end  with  ZZZ.   This is useful if you have to stop
       generating a wordlist in the middle.  Just do a tail
       wordlist.txt and set the -s parameter  to  the  next
       word  in the sequence.  Be sure to rename the origi‐
       nal wordlist BEFORE you begin as crunch  will  over‐
       write the existing wordlist.

       Example 7
       crunch 4 5 -p abc
       The numbers aren't processed but are needed.
       crunch will generate abc, acb, bac, bca, cab, cba.

       Example 8
       crunch 4 5 -p dog cat bird
       The numbers aren't processed but are needed.
       crunch  will  generate  birdcatdog, birddogcat, cat‐
       birddog, catdogbird, dogbirdcat, dogcatbird.

       Example 9
       crunch 1 5 -o START -c 6000 -z bzip2
       crunch will generate  bzip2  compressed  files  with
       each  file  containing 6000 words.  The filenames of
       the   compressed   files   will    be    first_word-
       last_word.txt.bz2

       # time ./crunch 1 4 -o START -c 6000 -z gzip
       real    0m2.729s
       user    0m2.216s
       sys     0m0.360s

       # time ./crunch 1 4 -o START -c 6000 -z bzip2
       real    0m3.414s
       user    0m2.620s
       sys     0m0.580s

       # time ./crunch 1 4 -o START -c 6000 -z lzma
       real    0m43.060s
       user    0m9.965s
       sys     0m32.634s

       size  filename
       30K   aaaa-aiwt.txt
       12K   aaaa-aiwt.txt.gz
       3.8K  aaaa-aiwt.txt.bz2
       1.1K  aaaa-aiwt.txt.lzma

       Example 10
       crunch 4 5 -b 20mib -o START
       will  generate  4  files:  aaaa-gvfed.txt, gvfee-om‐
       bqy.txt, ombqz-wcydt.txt, wcydu-zzzzz.txt
       the first three files are 20MBs  (real  power  of  2
       MegaBytes) and the last file is 11MB.

       Example 11
       crunch 3 3 abc + 123 !@# -t @%^
       will generate a 3 character long word with a charac‐
       ter as the first character, and number as the second
       character,  and  a  symbol  for the third character.
       The order in which you specify  the  characters  you
       want  is  important.   You must specify the order as
       lower case character, upper case character,  number,
       and symbol.  If you aren't going to use a particular
       character  set you use a plus sign as a placeholder.
       As you can see I am not using the upper case charac‐
       ter set so I am using  the  plus  sign  placeholder.
       The above will start at a1! and end at c3#

       Example 12
       crunch 3 3 abc + 123 !@# -t ^%@
       will  generate  3  character words starting with !1a
       and ending with #3c

       Example 13
       crunch 4 4  + + 123 + -t %%@^
       the plus sign (+) is a place holder so you can spec‐
       ify a character set for the character type.   crunch
       will use the default character set for the character
       type  when  crunch encounters a + (plus sign) on the
       command line.  You must either  specify  values  for
       each  character  type or use the plus sign.  I.E. if
       you have two characters types you MUST either  spec‐
       ify  values for each type or use a plus sign.  So in
       this example the character sets will be:
       abcdefghijklmnopqrstuvwxyz
       ABCDEFGHIJKLMNOPQRSTUVWXYZ
       123
       !@#$%^&*()-_+=~`[]{}|\:;"'<>,.?/
       there is a space at the end of the above string
       the output will start at 11a! and  end  at  "33z  ".
       The quotes show the space at the end of the string.

       Example 14
       crunch 5 5 -t ddd@@ -o j -p dog cat bird
       any character other than one of the following: @,%^
       is  the  placeholder  for the words to permute.  The
       @,%^ symbols have the same function as -t.
       If you want to use @,%^ in your output you  can  use
       the  -l  option  to specify which character you want
       crunch to treat as a literal.
       So the results are
       birdcatdogaa
       birdcatdogab
       birdcatdogac
       <skipped>
       dogcatbirdzy
       dogcatbirdzz

       Example 15
       crunch 7 7 -t p@ss,%^ -l a@aaaaa
       crunch will now treat the  @  symbol  as  a  literal
       character  and  not replace the character with a up‐
       percase letter.
       this will generate
       p@ssA0!
       p@ssA0@
       p@ssA0#
       p@ssA0$
       <skipped>
       p@ssZ9

       Example 16
       crunch 5 5 -s @4#S2 -t @%^,2 -e @8 Q2  -l  @dddd  -b
       10KB -o START
       crunch  will  generate  5 character strings starting
       with @4#S2 and ending at @8 Q2.  The output will  be
       broken  into  10KB  sized  files named for the files
       starting and ending strings.

       Example 17
       crunch 5 5 -d 2@ -t @@@%%
       crunch will generate  5  character  strings  staring
       with aab00 and ending at zzy99.  Notice that aaa and
       zzz are not present.

       Example 18
       crunch  10  10  -t @@@^%%%%^^ -d 2@ -d 3% -b 20mb -o
       START
       crunch will generate 10 character  strings  starting
       with aab!0001!! and ending at zzy 9998    The output
       will be written to 20mb files.

       Example 19
       crunch 8 8 -d 2@
       crunch  will  generate  8  characters that limit the
       same number of lower case characters to  2.   Crunch
       will start at aabaabaa and end at zzyzzyzz.

       Example 20
       crunch  4  4 -f unicode_test.lst japanese -t @@%% -l
       @xdd
       crunch will load some Japanese characters  from  the
       unicode_test  character  set  file.  The output will
       start at @日00 and end at @語99.

REDIRECTION
       You can use crunch's output and pipe it  into  other
       programs.   The  two  most  popular programs to pipe
       crunch into are: aircrack-ng  and  airolib-ng.   The
       syntax is as follows:
       crunch  2 4 abcdefghijklmnopqrstuvwxyz | aircrack-ng
       /root/Mycapfile.cap -e MyESSID -w-
       crunch 10 10 12345 --stdout | airolib-ng testdb -im‐
       port passwd -

NOTES
       1. Starting in version 2.6 crunch will  display  how
       much  data is about to be generated.  In 2.7 it will
       also display  how  many  lines  will  be  generated.
       Crunch will now wait 3 seconds BEFORE it begins gen‐
       erating  data  to  give  you time to press Ctrl-C to
       abort crunch if you find the values  are  too  large
       for your application.

       2.  I  have  added  hex-lower (0123456789abcdef) and
       hex-upper (0123456789ABCDEF) to charset.lst.

       3. Several people have requested that I add  support
       for  the  space character to crunch.  crunch has al‐
       ways supported the space character  on  the  command
       line  and in the charset.lst.  To add a space on the
       command line you must escape it using the /  charac‐
       ter.  See example 3 for the syntax.  You may need to
       escape  other  characters  like  ! or # depending on
       your operating system.

       4. Starting in 2.7 if you are generating a file then
       every 10 seconds you will receive the % done.

       5. Starting in 3.0 I had to change the -t *  charac‐
       ter  to  a  , as the * is a reserved character.  You
       could still use it if you put a \ in front of the *.
       Yes it breaks crunch's syntax and I do  my  best  to
       avoid  doing that, but in this instance it is easier
       to make the change for long term support.

       6. Some output is missing.  A file didn't get gener‐
       ated.
       The mostly explanation is you ran out of disk space.
       If you have verified you have plenty of  disk  space
       then  the problem is most likely the filename begins
       with a period.  In Linux filenames that begin with a
       period are hidden.  To view them do a ls -l .*

       7. Crunch says The maximum and minimum length should
       be the same size as the pattern you specified,  how‐
       ever the length is set correctly.
       This usually means your pattern contains a character
       that needs to be escaped. In bash you need to escape
       the followings: &, *, space, \, (, ), |, ', ", ;, <,
       >.
       The  escape  character in bash is a \.  So a pattern
       that has a & and a * in it would look like this:
       crunch 4 4 -t \&\*d@
       An alternative to escaping  characters  is  to  wrap
       your string with quotes.  For example:
       crunch 4 4 -t "&*d@"
       If  you  want  to use the " in your pattern you will
       need to escape it like this: crunch 4 4 -t "&*\"@"
       Please note that different terminals have  different
       escape  characters and probably have different char‐
       acters that will need escaping.   Please  check  the
       manpage  of  your terminal for the escape characters
       and characters that need escaping.

       8. When using the -z 7z option, 7z does  not  delete
       the  original  file.   You will have to delete those
       files by hand.

AUTHOR
       This manual page was written by bofh28@gmail.com

       Crunch  version  1.0  was  written  by  mimayin@aci‐
       iid.ath.cx
       all  later  versions  of crunch have been updated by
       bofh28@gmail.com

FILES
       None.

BUGS
       If   you    find    any    please    email    bofh28
       <bofh28@gmail.com>  or post to http://www.backtrack-
       linux.org

COPYRIGHT
       Copyright (c) 2009-2013 bofh28 <bofh28@gmail.com>

       This file is a part of Crunch.

       Crunch is free software:  you  can  redistribute  it
       and/or  modify it under the terms of the GNU General
       Public License as published  by  the  Free  Software
       Foundation, version 2 only of the License.

       Crunch  is  distributed  in the hope that it will be
       useful, but WITHOUT ANY WARRANTY; without  even  the
       implied warranty of MERCHANTABILITY or FITNESS FOR A
       PARTICULAR  PURPOSE.  See the GNU General Public Li‐
       cense for more details.

       You should have received a copy of the  GNU  General
       Public  License  along  with  Crunch.   If  not, see
       <http://www.gnu.org/licenses/>.

Version 3.6               May 2014                CRUNCH(1)
```

---

参考链接

- [Crunch](https://www.kali.org/tools/crunch/)

