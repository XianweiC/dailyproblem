# 记一次大意

2020/12/10

## 在今天通过`ubuntu`远程commit了众多代码的情况下，却没能在github产生记录，经过一番排除，发现问题的原因

### 1.需要github的邮箱与本机git邮箱地址一致

```shell
git config --global user.email "2432510513@qq.com"
//一开始设置成了Outlook邮箱，需要设置为申请github账户的邮箱
```

### 2.需要github的用户名和本机设置的用户名一致

```shell
git config --global user.name "Monster-c"
//一开始设置成了电脑user，需设置为github账户昵称
```

## **总之**，记住这次错误。如果按照之前的方式提交，github会默认不是同一个用户在进行操作，自然commit记录里不会出现。