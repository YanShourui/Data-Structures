## 线性表的顺序储存
### 顺序表
1.线性表的顺序储存是指在内存中用地址连续的一块储存空间顺序存放线性表的各元素，用这种储存形式储存的线性表称为顺序表。  
2.设$a_1$的储存地址为$Loc(a_1)$，每个元素占d个存储单元，则第i个元素的地址  
$$Loca（a_i）=Loca(a_1)+(i-1)×d &emsp;&emsp;（1≤i≤n）$$
3.封装结构题作为顺序表类型

```
typedef struct
  {
    datatype data[MAXSIZE];
    int last;
  }SeqList;
  
```
4.定义一个顺序表：
```
SeqList L;
```
或者
```
SeqList *L;
```
5.可以通过```L=（SeqList *）malloc(sizeof(SeqList));```来获取顺序表的储存空间。
### 顺序表上基本运算的实现
1.顺序表的初始化。
```
SeqList *init_SeqList（）
  {
    SeqList *L;
    L=(SeqList*)malloc(sizeof(SeqList));
    L->last=-1;
    return L;
  }
```
2.顺序表的插入。
```
int Insert_SeqList(SeqList*L，int i,datatype x)//这个算法需要返回改变的顺序表所以是 SeqList * 类型。
  {
    int j;
    if(L->Last == MAXSIZE-1)//若last这个最后位置为MASIZE-1，则表示空间已经满了。
    {printf("表满");return(-1);}
    if(i<1||i>L->last+2)//因为插入可以在最后一个位置插入，所以i不能超过last+2.
    {printf("位置错");return(0);}
    for(j=L->last;j>=i-1;j--)
    {
      L->data[j+1]=L->data[j];//注意赋值是将等号右边的赋值给等号左边的。
    }
    L->data[i-1]=x;//新元素插入。
    L->last++;//last仍然指向最后元素。
    return (1);
  }
```
3.顺序表的删除。
```
int Delete_SeqList(SeqList*L，int i)//这个算法需要返回改变的顺序表所以是 SeqList * 类型。
  {
    int j;
    if(i<1||i>L->last+1)//检查空表以及删除位置的合法性。i不能超过last+1.
    {printf("不存在第i个元素");return(0);}
    for(j=i;j<=L->last;j++)
    {
      L->data[j-1]=L->data[j];//向上移动，注意赋值是将等号右边的赋值给等号左边的。
    }
    L->last--;//last仍然指向最后元素。
    return (1);//删除成功，返回代码1。
  }
```
4.顺序表中的查找。
```
int Location_SeqList(SeqList*L，datatype x)
{
  int i=0;//从第一个位置开始。
  while(i<=L->last&&L->data!=x)//直到不满足条件停止循环。
  i++;
  if(i>L->last)return -1;
  else return i;//查找成功，返回储存位置。
}
```
5.
6.