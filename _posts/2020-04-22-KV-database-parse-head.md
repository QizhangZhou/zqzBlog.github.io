---
title: KV数据库读写加head，解head
layout: post
post-image: "https://raw.githubusercontent.com/thedevslot/WhatATheme/master/assets/images/SamplePost.png?token=AHMQUEPC4IFADOF5VG4QVN26Z64GG"
description: KV数据库中，写入KV键值对，有的时候需要在key中增加head，表示key在某张表的唯一性。
tags:
- KV
- database
- tech
---

KV数据库中，写入KV键值对，有的时候需要在key中增加head，表示key在某张表的唯一性。
KV结构体为：
```c
typedef struct stKvInfo{
    char *key;
    char *value;
    int keyLen;
    int valLen;
}KvInfo;
```

在key的前面加入int类型头，标识key的类型，编码函数为：
```c
void EncodeKvInfo(KvInfo *kvSrc, int srvType)
{
    if (kvSrc == NULL || kvSrc->key == NULL) {
        printf("kvSrc or kvSrc->key is NULL");
        return;
    }
    int tmpKeyLen = kvSrc->keyLen * sizeof(char) + sizeof(int);
    char *tmpKey = (char* )malloc(tmpKeyLen);
    if (tmpKey == NULL) {
        printf("tmpKey is NULL");
        return;
    }
    memset(tmpKey, 0 , tmpKeyLen);
    memcpy(tmpKey, &srvType, sizeof(int));
    memcpy(tmpKey + sizeof(int), kvSrc->key, kvSrc->keyLen * sizeof(char));

    KvInfo kv = {0};
    kv.key = tmpKey;
    kv.value = kvSrc->value;
    kv.keyLen = kvSrc->keyLen + sizeof(int);
    kv.valLen = kvSrc->valLen;
    return ;
}
```
解码函数为，这个示例只是解出来了int类型的type：
```c
void DecodeKvInfo(KvInfo *kvdst, int *srvType)
{
    if (kvdst == NULL || kvdst->key == NULL) {
        printf("kvdst or kvdst->key is NULL");
        return;
    }

    int tmpKeySrvLen = sizeof(int);
    char *tmpKeySrv = (char* )malloc(tmpKeySrvLen);
    if (tmpKeySrv == NULL) {
        printf("tmpKey is NULL");
        return;
    }
    memset(tmpKeySrv, 0 , tmpKeySrvLen);
    memcpy(tmpKeySrv, kvdst->key, sizeof(int));
    union u{
        int v;
        char key[4];
    }uu;
    uu.key[0] = tmpKeySrv[0];
    uu.key[1] = tmpKeySrv[1];
    uu.key[2] = tmpKeySrv[2];
    uu.key[3] = tmpKeySrv[3];
    *srvType = uu.v;
    return;
}
```
调试打印函数：
```c
void KvInfoPrintf(KvInfo kvSrc)
{
    cout << "-----------------------------" << endl;
    cout << "KEY: " ;
    for (int i = 0; i < kvSrc.keyLen; i++) {
            cout << hex << int(kvSrc.key[i]) << " ";
    }
    cout << endl;
    cout << "VALUE: " << kvSrc.value << endl;
    cout << "KEY LEN: " << kvSrc.keyLen << endl;
    cout << "VALUE LEN: " << kvSrc.valLen << endl;
    cout << "-----------------------------" << endl;
}
```
```c
int main()
{
    KvInfo kv = {0};
    kv.key = (char*)"key1";
    kv.value = (char*)"value1";
    kv.keyLen = strlen(kv.key);
    kv.valLen = strlen(kv.value);
    KvInfoPrintf(kv);
    EncodeKvInfo(&kv, 123455);
    return 0;
}
```

调试打印输出为：
```language
cla@CalvinPC:/mnt/e/CodingPractice/C++/CPP_thread$ ./main
-----------------------------
KEY: 6b 65 79 31
VALUE: value1
KEY LEN: 4
VALUE LEN: 6
-----------------------------
Encode Kv Info:--------------
-----------------------------
KEY: 3f ffffffe2 1 0 6b 65 79 31
VALUE: value1
KEY LEN: 8
VALUE LEN: 6
-----------------------------
Decode Kv Info:--------------
srvType: 123455
```



