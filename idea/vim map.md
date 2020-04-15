## Vim的几种模式和按键映射

Map是Vim强大的一个重要原因，可以自定义各种快捷键，用起来自然得心应手。

### 1. vim里最基本的map用法也就是

```
:map c a
```

这里把c映射成了a，在map生效的情况下，按下c就等同于按下了a
当然，常用的Ctrl,Shift,Alt自然也是支持的。

- 令Ctrl+a对应到a

  `:map  <C-a> a`

- 令Alt+a对应到a

  `:map  <A-a> a`

- 令Ctrl+Alt+a对应到a

  `:map  <C-A-a> a`

到此，我们已经可以做很多事情了。

### 2. Vim的各种模式

但是map命令远不只这一种，在不同的模式下，同一组按键可以被映射到不同的组合上。
Vim的模式众多，但是一般被提及的也就是这么几种:

1. Normal Mode

   也就是最一般的普通模式，默认进入vim之后，处于这种模式。

2. Visual Mode

   一般译作可视模式，在这种模式下选定一些字符、行、多列。
   在普通模式下，可以按v进入。

3. Insert Mode

   插入模式，其实就是指处在编辑输入的状态。普通模式下，可以按i进入。

4. Select Mode

   在gvim下常用的模式，可以叫作选择模式吧。用鼠标拖选区域的时候，就进入了选择模式。
   和可视模式不同的是，在这个模式下，选择完了高亮区域后，敲任何按键就直接输入并替换选择的文本了。
   和windows下的编辑器选定编辑的效果一致。普通模式下，可以按gh进入。

5. Command-Line/Ex Mode

   就叫命令行模式和Ex模式吧。两者略有不同，普通模式下按冒号(:)进入Command-Line模式，可以输入各种命令，
   使用vim的各种强大功能。普通模式下按Q进入Ex模式，其实就是多行的Command-Line模式。

### 3. 对于Map，有几个基本的概念

- 命令的组合

  同Vim下的其他命令一样，命令的名字往往由好几段组成。前缀作为命令本身的修饰符，微调命令的效果。
  对于map而言，可能有这么几种前缀

  1. nore

     表示非递归，见下面的介绍

  2. n

     表示在普通模式下生效

  3. v

     表示在可视模式下生效

  4. i

     表示在插入模式下生效

  5. c

     表示在命令行模式下生效

     

     ```
      字 符     模 式   
      <Space>    普通、可视、选择和操作符等待
     	n       普通模式
     	v       可视和选择模式
     	s       选择模式
     	x       可视模式
     	o       操作符等待模式
     	!       插入和命令行模式
     	i       插入模式
     	l       插入、命令行和 Lang-Arg 模式的 ":lmap" 映射
     	c       命令行模式
     ```

     

- Recursive Mapping

  递归的映射。其实很好理解，也就是如果键a被映射成了b，c又被映射成了a，如果映射是递归的，那么c就被映射成了b。

  `:map a b `

  `:map c a`

  对于c效果等同于

  `:map c b`

  默认的map就是递归的。如果遇到[nore]这种前缀，比如:noremap，就表示这种map是非递归的。

- unmap

  unmap后面跟着一个按键组合，表示删除这个映射。

  `:unmap c`

  那么在map生效模式下，c不再被映射到a上。

  同样，unmap可以加各种前缀，表示影响到的模式。

- mapclear

  mapclear直接清除相关模式下的所有映射。
  同样，mapclear可以加各种前缀，表示影响到的模式。

### 4. 这里列出常用的一些map命令，默认map命令影响到普通模式和可视模式。

:map :noremap :unmap :mapclear
:nmap :nnoremap :nunmap :nmapclear
:vmap :vnoremap :vunmap :vmapclear
:imap :inoremap :iunmap :imapclear
:cmap :cnoremap :cunmap :cmapclear

可以试试这些命令

1. 命令行模式下建一个mapping

   ```
    nmap b a 
   ```

2. 现在普通模式下，按b，可以进入插入模式，随便输入一些字符

3. 命令行模式下建一个mapping

   ```
    vmap b d 
   ```

4. 现在普通模式下，按V，进入了可视模式，并且选定了一整行，按下b，可以删除整行

5. 命令行模式下建一个mapping

   ```
    imap b a 
   ```

6. 现在试着给正在编辑的这个文件输入一个字符"b"吧 :p

7. 命令行模式下建一个mapping

   ```
    cmap b c 
   ```

8. 命令行模式下， 按下b，会出来一个a

好了，到此vim的按键已经被你弄得乱七八糟了，试着用unmap和mapclear清除这些mapping吧。

### 5. 键表 
|key-notation|

- <k0> - <k9> 小键盘 0 到 9

- <S-字母> Shift＋字母键 , 例如 <S-a> 表  shift+a键

- <C-字母> Control＋字母键

- <M-字母> Alt＋字母键 或 meta＋字母键

- <A-字母> 同 <m-字母>

- <CR>  'CR-used-for-NL,即表示新行的意思，可以使用 CRTL-V CRTL-M（输入的是 <CR> 字符本身） 或者 '\r'，Vim 并不会在文件中直接输入 <CR> 字符，它会根据当前 ‘fileformat’ 的设置来决定使用<CR>（Mac），<NL>(\*nix) 还是 <CR><NL>(dos)。

### 6. 一些奇技

1. nnoremap j jzz 和 nnoremap k kzz 读代码就是方便，谁用谁知道   (guyue: 不错不错)
2. nnoremap <esc> :nohl<cr> 搜索完后按esc就可以去掉高亮啦，你还在傻傻得输入命令？   (guyue: 不错不错)
3. cc 有的童鞋不知道合理使用这个命令，绕了很多弯子，比如想在某个空行插入代码的时候，用a，然后手补缩进（vim默认会把空行的缩进去掉以保持整洁的），也有人用ddO来代替，更有因此想让vim保留空行缩进的童鞋。你们不知道cc可以清空一行并在合适的缩进位置进入插入模式么，这个命令虽简单，但必须值得科普一下！
4. 在~/.vimrc里放一句source path/to/real/vimrc然后就可以把vim配置放进Dropbox或者Git了
5. 如果你用Git管理你的vim配置并且用了Vundle管理插件的话，那么把vundle当作git submodule，那么以后你在别处clone下你的配置时就不用再手动装Vundle啦（别的插件管理工具也同理的）



### 7. 常用编辑命令

```text
i  光标前插入（进入插入模式）
a  光标后插入
I  行首插入
A  行尾插入
o  当前行下插入一行
O  当前行前插入一行

#注意：修改命令以c开头，表示change
cw  修改到词尾的内容
ciw 修改整词
caw 修改整词包括词尾空格
cW  修改到字串尾的内容
ciW 修改整字串
caW 修改整字串包括字串尾空格
C   修改到行尾的内容
cis  修改当前句
cas  修改当前句包括句尾空格
cip  修改当前段
cap  修改当前段包括段尾空行
Esc  退出插入模式，返回普通模式
ctrl+[  同Esc

#注意：删除命令以d开头，表示delete
dw  删除到词尾的内容
diw 删除整词
daw 删除整词包括词尾空格
dW  删除到字串尾的内容
diW 删除整字串
daW 删除整字串包括字串尾空格
D   删除到行尾的内容
dis  删除当前句
das  删除当前句包括句尾空格
dip  删除当前段
dap  删除当前段包括段尾空行

.   在当前位置重复上一次操作
u   撤销上一次操作
```