---
title: "Git - Behind Version Control"
date: "2021-04-18"
tags: ["Terminal"]
---

# Git - Behind Version Control
[这才是Git-Git内部原理揭秘](https://www.bilibili.com/video/av77252063)

## Git怎么存储我们的信息？？？
整个步骤

### 先初始化并且添加文件
```css
git init

echo '111' > a.txt
echo '222' > b.txt

git add *.txt
```
添加了两个文件
```css
tree .git/objects

.git/objects
|--58
|    --c9aklsfjalkuiue2jnklasnfkanskldad
|--c2
|    --009dhajksljdklasjdkljaklsjdklasjs
|--info
|--pack
```
读取.git/object发现多出了两个文件
```css
git cat-file -t 58c9
git cat-file -p 58c9

git cat-file -t c200
git cat-file -p c200
```
使用上面的t和p可以看文件的种类和内容
```css
blob
111

blub
222
```
可以看到上面两个文件的类型都是 blob，内容为echo内容\`
\`
### 然后使用提交命令
```css
git commit -m '[+] initialization [+]a.txt, b.txt'
tree .git/objects


.git/objects
|--58
|    --c9aklsfjalkuiue2jnklasnfkanskldad
|--c2
|    --009dhajksljdklasjdkljaklsjdklasjs

|--4c
|    --aa9dhajksljdklasjdkljaklsjdklasjs
|--0c
|    --96aklsfjalkuiue2jnklasnfkanskldad

|--info
|--pack
```
发现又多出来了俩文件
```css
git cat-file -t 4caa
git cat-file -p 4caa

git cat-file -t 0c96
git cat-file -p 0c96
```
使用同样的指令打开多的两个文件
```css
tree
100644 blob 58c9aklsfjalkuiue2jnklasn... a.txt
100644 blob 4c009dhajksljdklasjdkljak... b.txt

commit
tree 4caa9dhajksljdklasjdkljaklsjdklasjs
author lzane 胡所未 1573302343 +0800
commiter lzane 胡所未 1573302343 +0800
[+] init
```
第一个文件类型为tree，其内容有两个node，每个node从左往右分别是：文件的权限，文件类型，文件对应的哈希值，文件名称。（请参考Git Obj）
第二个文件类型为commit，其内容有三个node， 第一个node为其指向的tree及其哈希值，第二三个为提交者的信息，第四个为提交的信息（message -m）。
### 所以我们日常使用的分支和tag在哪里呢（HEAD）？？
```css
cat .git/HEAD
ref: refs/heads/master
```
Git将这些信息以明文的形式储存在`.git`文件夹下
（上面的这个HEAD指向的是`.git`下的一个master分支）
```css
cat .git/refs/heads/master
0caa9dhajksljdklasjdkljaklsjdklasjs
```
发现指向了一个哈希值
```css
git cat-file -t 0caa9dhajksljdkl
commit
```
发现这个指向的就是刚刚的commit object

----


## Git Object
在git里面所有创建的object都是immutable的，一旦创建就无法修改（除了tag不是object，而是指针，所以HEAD可以跟随每一次commit指向最新的commit obeject）
![2023.11.23 - 211348](2023.11.23%20-%20211348.jpg)


### Blob Object:
里面包含了文件的内容
![2023.11.23 - 211356](2023.11.23%20-%20211356.jpg)
Blob和一些meta信息通过SHA1哈希算法生成字符串（可以理解成： git object在git中的唯一身份证)
![2023.11.23 - 211403](2023.11.23%20-%20211403.jpg)

### Tree Object
每个tree object里面包含了文件的读取权限，文件类型，文件的哈希值，文件名称，（通过哈希值就可以找到在commit之前添加的的blob object，从而找到文件里面的内容）
![2023.11.23 - 211412](2023.11.23%20-%20211412.jpg)
（一个tree object指向俩blob object)

### Commit Object
每个commit object里面包含了这次commit的tree object，commit者和作者的相关信息，还有commit的message -m
![2023.11.23 - 211421](2023.11.23%20-%20211421.jpg)
（一个commit指向一个tree object，tree指向俩文件)

### Tag pointer （非Object ！！！！！！）
HEAD, 分支，普通的tad都可以理解成一个指针，指向对应的commit的SHA1值
![2023.11.23 - 211428](2023.11.23%20-%20211428.jpg)

----

## Git 三个分区以及历史
![2023.11.23 - 211438](2023.11.23%20-%20211438.jpg)
工作分区/暂存区
操作系统的文件系统，可以看作一个暂存区，所有你正在更改的文件都在本地有一个临时的object（正方形）
索引index
当你使用git add命令的时候就创建了指向这几个文件的索引（三角)
Git仓库
当你使用git commit命令的守候就使得工作branch指向了现在的索引

### 实际工作范例
#### 更改文件
通过`echo ‘333’ > a.txt`命令更改了文件`a.txt`这个时候除了工作目录区其他部分没有任何更改。
![2023.11.23 - 211447](2023.11.23%20-%20211447.jpg)

#### 添加文件
通过`git add a.txt`将文件添加到了git仓库，这个时候实际是在git仓库创建了更改文件对应的blob object，并且将索引区的原本指向老的`a.txt`文件的指针改成了指向新的`a.txt`.
![2023.11.23 - 211454](2023.11.23%20-%20211454.jpg)

#### Commit提交暂存区
Commit命令将会将暂存区的文件，提交到本地的版本库中去，具体为：
先在git仓库中按照 索引区的索引 创建tree object，然后新建一个commit object指向刚刚创建的tree object，最后将工作目录（HEAD / master）之类的指针指向 新的commit object


## Git 怎么保证记录无法篡改？？？
因为git和区块链类似，都是通过哈希树和分布式，在git里面，如果改动一个历史中的文件（改动一个bolb object），则其哈希值会变，导致指向他的tree object的哈希值改变，commit object哈希值改变，最后master指向的哈希值就会和原来的不一致。
![image-20191231172549339](https://tva1.sinaimg.cn/large/006tNbRwgy1gag16ikgkoj30oa0dagta.jpg)

## Git Ref-log
版本控制的版本控制
![2023.11.23 - 211504](2023.11.23%20-%20211504.jpg)
比如如果一不小心使用了`git reset -hard`不小心删除了所有的工作区的内容，那么可以先使用 `git reflog` 找到之前 本地工作区域 变更的哈希值，然后使用 `git reset -hard 6952e07`命令(6952e07只做范例，实际填返回的版本号)[详情可以看这个](https://www.jianshu.com/p/390b6861b8c7)

## 从git历史中删除文件
敏感信息，私钥，内网，超大文件，不需要备份的文件
![2023.11.23 - 211514](2023.11.23%20-%20211514.jpg)
把所有的branch都拿出来，执行`rm -f passwords.txt`命令，然后吧所有branch在放回去，就可以在git base删除文件

但是这个命令会把所有的commit节点的哈希值都变更，也就是说所有正在工作的工作区的git将无法再提交

### 所以为什么要把文件的权限信息和文件名称存在 tree object里呢？？？ 为什么不直接存在blob object里？？？？？

- 如果存在blob object里，则每次更改文件名称或者权限，git都需要新建一个blob object，然后再创建一个tree指向他
- 而如果存在tree object里，则每次更改文件名称只需要新建一个tree object，然后指向原来的blob
	因为blob储存的是文件具体内容，所以他比tree大很多，新建一个blob自然就更加浪费空间。


# Git Rebase-待阅-done

[你真的懂Git Rebase吗](https://www.jianshu.com/p/6960811ac89c)

\\#