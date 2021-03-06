# struct nameidata

一个主要操作是根据给定的文件名查找inode，这使得我们首先需要了解有关查找该信息的机制。
nameidata结构用来向查找函数传递参数，并保存查找结果。

## path

path: fs/namei.c
```
#define EMBEDDED_LEVELS 2
struct nameidata {
    struct path    path;
```

查找完成后，path包含了找到的文件系统项的数据。

https://github.com/novelinux/linux-4.x.y/tree/master/include/linux/path.h/struct_path.md

## last

```
    struct qstr    last;
```

last包含了需要查找的名称。它是一个快速字符串（quickstring），如前文所述，不仅包含字符串本身，
还包括字符串的长度和一个散列值。

## root

```
    struct path    root;
```

存储文件所在文件系统根目录

## inode

```
    struct inode  *inode; /* path.dentry.d_inode */
```

## flags

```
    unsigned int   flags;
```

flags保存了标志，用于微调查找操作。在我讲述查找算法时，会返回来讲解这些标志。

## seq, m_seq

```
    unsigned    seq, m_seq;
```

## last_type

```
    int        last_type;
```

路径最后的文件类型

## depth

```
    unsigned    depth;
```

递归深度

## total_link_count

```
    int        total_link_count;
```

## stack, internal

```
    struct saved {
        struct path link;
        void *cookie;
        const char *name;
        struct inode *inode;
        unsigned seq;
    } *stack, internal[EMBEDDED_LEVELS];
```

## name

```
    struct filename    *name;
```

https://github.com/novelinux/linux-4.x.y/blob/master/include/linux/fs.h/struct_filename.md

## saved

```
    struct nameidata *saved;
    unsigned    root_seq;
    int        dfd;
};
```