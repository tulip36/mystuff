## Vim 常用编辑操作

> . 代表光标所在位置

| 序列 | 命令 | 代表的命令 | 前                         | 后      | 说明                                         | 模式变化 |
| ---- | ---- | ---------- | -------------------------- | ------- | -------------------------------------------- | -------- |
| 1    | x    | d1         | vi.m                       | vi      | 删除光标处的字符                             | normal   |
| 2    | X    | dh         | vi.m                       | vm      | 删除光标左边的字符                           | normal   |
| 3    | D    | d$         | vim. right                 | vim     | 从当前光标删除到行尾                         | normal   |
| 4    | C    | c$         | vim. right                 | vim.    | 从当前光标删除到行尾                         | insert   |
| 5    | s    | c1         | vi.m                       | v.m     | 删除光标处的字符                             | insert   |
| 6    | S    | cc         | __vim.                     | __.     | 删除整行，但保留前面的缩进                   | insert   |
| 7    |      | dd         | __vim.                     | .       | 删除整行，但光标在行首                       | normal   |
| 8    |      | d2w        | v. m r h p                 | v .h p  | 删除光标右边的两个单词，<br />光标在单词前面 | normal   |
| 9    |      | d2e        | v. m r h p                 | v h. p  | 删除光标右边的两个单词，<br />光标在单词后面 | normal   |
| 10   |      | c2w        | v. m r h p                 | v .h p  | 删除光标右边的两个单词，<br />光标在单词前面 | insert   |
| 11   |      | c2e        | v. m r h p                 | v h. p  | 删除光标右边的两个单词，<br />光标在单词后面 | insert   |
| 12   |      | da[        | [.vim] m r<br />[vim]. m r | .m r    | 删除整个[vim]                                | normal   |
| 13   |      | di[        | [.vim] m r                 | [.] m r | 删除vim, 保留[]                              | normal   |
| 14   |      | 2dj        |                            |         | 向下删除两行                                 | normal   |
| 15   |      | 2dk        |                            |         | 向上删除两行                                 | normal   |
| 16   | r    |            |                            |         | 修改当前光标处的字符                         | normal   |
| 17   | R    |            |                            |         | 将光标移到前面一个字符                       | insert   |
| 18   | v    |            |                            |         | 开始选择模式                                 | visual   |
| 19   |      | ve         |                            |         | 选择一个单词                                 | visual   |
| 20   | V    |            |                            |         | 选择一行                                     | visual   |
| 21   | y    |            |                            |         | 复制所选择的内容                             | visual   |
| 22   | Y    |            |                            |         | 从光标处开始复制到行尾                       | normal   |
| 23   | yy   |            |                            |         | 复制当前行                                   | normal   |

### 2. Selecting Blocks

If you want to work on a rectangular block of characters, use **Ctrl-V** to start Visual mode. This is very useful when working on tables.

```
name		Q1	Q2	Q3
pierre		123	455	234
john		0	90	39
steve		392	63	334
```

To delete the middle "**Q2**" column, move the cursor to the "**Q**" of "**Q2**". Press **Ctrl-V** to start blockwise Visual mode. Now move the cursor three lines down with "**3j**" and to the next word with "**w**". You can see the first character of the last column is included. To exclude it, use "**h**". Now press "**d**" and the middle column is gone.



