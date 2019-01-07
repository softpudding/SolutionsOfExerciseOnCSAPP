# 第9章：虚拟内存
## 练习题
### 9.6
请求 |块大小（十进制字节） |块头部（十六进制）
---|---|---
malloc(1)|8|0x9
malloc(5)|16|0x11
malloc(12)|16|0x11
malloc(13)|24|0x19

### 9.7
对其要求 |已分配的块 |空闲快 |最小块大小（字节）
---|---|---|----
单字 |头部和脚部 |头部和脚部 |8（空闲块至少是8）
单字 |头部，但是无脚部|同上 |8（空闲块至少是8，分配的块也至少是8）
双字 |头部和脚部 |同上 |16
双字 |头部，但是没有脚部| 同上|16（和上面一行一样，满足对齐要求就至少16） 

### 9.8
```c
static void * find_fit(size_t asize)
{
    void * searcher=mem_heap;
    while(searcher!=mem_brk)
        if(!GET_ALLOC(HDRP(searcher))&&GET_SIZE(HDRP(searcher)))
            return searcher;
    return NULL;
}
```
### 9.9
```c
static void place(void *bp, size_t size)
{
    size_t left=GET_SIZE(HDRP(bp))-size;
    if(left<2*DSIZE)
        size=left+size;
    PUT(HDRP(bp),PACK(size,0));
    PUT(FTRP(bp),PACK(size,0));
    if(left>=2*DSIZE)
    {
        PUT(HDRP(NEXT_BLKP(bp)),PACK(left,0));
        PUT(FTRP(NEXT_BLKP(bp)),PACK(left,0));
    }
}
```
