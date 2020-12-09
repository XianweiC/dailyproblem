```
#include <stdio.h>
#include <stdlib.h>

#define LIST_INIT_SIZE 100
#define LISTINCREMENT 10

/*
定义用户类型结构体
*/
typedef struct
{
    int id;
    char name[20];
}User;

/*定义顺序表*/
typedef struct
{
    User* user;
    int length;
    int listsize;
}SqList;

//初始化
int Init_SqList(SqList* L);
//增删查改
int Insert_SqList(SqList* L, int i, User newUser);
User* Delete_SqList(SqList* L, int i);
User* Find_SqList(SqList* L, int i);
int Change_SqList(SqList* L, int i, User newUser);

int main()
{
    SqList list;
    User user = {1, "liming"};
    Init_SqList(&list);

    //list.user[0] = user;
    //list.length ++;
    Insert_SqList(&list, 1, user);
    Show_SqList(list);
    //printf("1111\n");
    //printf("%d\t%s\n", list.user[0].id, list.user[0].name);

    User newUser = {2, "xiaohong"};
    Insert_SqList(&list, 2, newUser);
    Show_SqList(list);
//    printf("%d\t%s\n", list.user[1].id, list.user[1].name);


    printf("Hello world!\n");
    return 0;
}

int Init_SqList(SqList* L)
{
    L->user = (User*)malloc(sizeof(User));
    if(!L->user)
    {
        printf("------SqList Init Failed!------\n");
    }
    L->length = 0;
    L->listsize = LIST_INIT_SIZE;
    printf("------SqList Init Successful!------\n");
    return 0;
}

int Insert_SqList(SqList* L, int i, User newUser)
{
    if(i < 1 || i > L->listsize)
    {
        printf("Insert failed!\n");
        return -1;
    }

    if(L->length >= L->listsize)//It means the SqList is full now.
    {
        User* newBase = (User*)realloc(L->user, (L->listsize + LISTINCREMENT)*sizeof(User));
        if(!newBase)
        {
            printf("newBase create failed!");
            return -1;
        }
        L->user = newBase;
        L->listsize += LISTINCREMENT;
    }

    //save the address of where you want to insert
    User* temp = &(L->user[i - 1]);
    //其余元素后移
    User* p = &(L->user[L->length - 1]);
    for(; p >=  temp; -- p)
    {
        *(p+1) = *p;
    }
    *temp = newUser;
    //the length of SqList plus one
    L->length ++;
    return 0;
}

User* Delete_SqList(SqList* L, int i)
{
    if(i <1 || i > L->length)
    {
        printf("Delete Error!");
        return (User*)NULL;
    }

    //save the infor that you want delete
    User* temp = &(L->user[i - 1]);

    User* p = &(L->user[i - 1]);
    User* last = &(L->user[L->length - 1]);
    for(; p< &(L->user); p ++)
    {
        *(p + 1) = *p;
    }

    L->length --;

    return temp;
}

User* Find_SqList(SqList* L, int i)
{
    if(i < 1 || i > L->length)
    {
        printf("Not Found");
        return (User*)NULL;
    }
    User* temp = &(L->user[i - 1]);
    return temp;
}

int Change_SqList(SqList* L, int i, User newUser)
{
    if(i < 1 || i > L->length)
    {
        printf("Change Error!");
        return -1;
    }
    L->user[i - 1] = newUser;
    return 0;
}

int Show_SqList(SqList L)
{
    int i =0;
    for(;i < L.length;i ++)
    {
        printf("%d           \n", i);
        printf("Length of SqList now:%d\n", L.length);
        printf("User ID:%d\t User Name:%s\n", L.user[i].id, L.user[i].name);
    }
    return 0;
}

```

