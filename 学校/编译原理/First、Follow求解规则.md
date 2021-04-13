# 编译原理之计算FIRST集合和FOLLOW集合

## FIRST集合的求解规则

计算各个文法符号X的FIRST(X)时，不断应用下列规则，直到再没有新的终结符号或者ε可以被加入到任何FIRST集合中为止。

1. **如果X是一个终结符号，那么FIRST(X) = X。**
2. **如果X是一个非终结符号，且X -> Y1Y2 …Yk是一个产生式，其中k ≥ 1，那么如果对于某个i , a 在FIRST(Yi)中且ε在所有的FIRST(Y1)、FIRST(Y2)、….、FIRST(Yi-1)中，就把a加入到FIRST(X)中。也就是说，Y1…Yi-1 =>* ε。如果多于所有的j = 1,2,3,..,k , ε在FIRST(Yj)中，那么将 ε 加入到FIRST(X)中。比如，FIRST(Y1)中的所有符号一定在FIRST(X)中。如果Y1 不能推导出 ε ，那么，我们就不会再向FIRST(X)中加入任何符号，但是如果Y1 =>* ε ，那么我们就加上FIRST(Y2)，以此类推。**
3. **如果X -> ε 是一个产生式，那么将ε 加入到FIRST(X)中。**



## FOLLOW集合的求解规则

计算所有非终结符号A的FOLLOW(A)集合时，不断应用下列规则，直到再没有新的终结符号可以被加入到任意FOLLOW集合中为止。

1. 将 $ 放到FOLLOW(S)中，其中S是开始符号，而 $ 是输入右端的结束标记。
2. 如果存在一个产生式 A -> αBβ ， 那么FIRST(β)中除 ε之外的所有符号都在FOLLOW(B)中。
3. 如果存在一个产生式A -> αB，或存在产生式 A -> αBβ 且 FIRST(β)包含 ε ，那么FOLLOW(A)中的所有符号都在FOLLOW(B)中。



上述的文字规则不免有些抽象和枯燥，不如直接举个栗子来看看吧~

## 例题

文法G[E]:
1. E -> TE’
2. E’-> +TE’
3. E’-> ε
4. T -> FT’
5. T’-> *FT’
6. T’-> ε
7. F -> (E)
8. F -> a

### (1) 求FIRST集合(这里只求非终结符号的FIRST集合)

#### 分析：

    FIRST(E): 由E -> TE’可得FIRST(E) = FIRST(T)
    FIRST(T): 由T -> FT’可得FIRST(T) = FIRST(F)
    FIRST(F): 由F -> (E)和F -> a可得FIRST(F) = { ( , a };
    FIRST(T’): 由T’-> *FT’和T’-> ε 可得FIRST(T’) = { * , ε };
    FIRST(E’): 由E’-> +TE’和E’-> ε可得FIRST(E’) = { + , ε };

#### 结果：

    FIRST(E) = { ( , a };
    FIRST(T) = { ( , a };
    FIRST(F) = { ( , a };
    FIRST(T’) = { * , ε };
    FIRST(E’) = { + , ε };

### (2) 求FOLLOW集合

#### 分析：

    FOLLOW(E): 由F -> (E)可得，FOLLOW(E) = { ) ，$}
    FOLLOW(E’): 由E -> TE’和E’-> +TE’可得，FOLLOW(E’) = FOLLOW(E)
    FOLLOW(T): 由E -> TE’、E’-> +TE’和E’-> ε 可得，FOLLOW(T) = FIRST(E’) / ε +FOLLOW(E) + FOLLOE(E’)
    FOLLOW(T’): 由T -> FT’和T’-> *FT’可得，FOLLOW(T’) = FOLLOW(T)
    FOLLOW(F): 由T -> FT’、T’-> *FT’和T’-> ε可得，FOLLOW(F) = FIRST(T’) / ε +FOLLOW(T) + FOLLOW(T’)

#### 结果：

    FOLLOW(E) = { ) ，$}
    FOLLOW(E’) = FOLLOW(E) = { ) ，$}
    FOLLOW(T) = FIRST(E’) / ε +FOLLOW(E) + FOLLOE(E’) = {+ , ) , $}
    FOLLOW(T’) = FOLLOW(T) = {+ , ) , $}
    FOLLOW(F) = FIRST(T’) / ε +FOLLOW(T) + FOLLOW(T’) = {* , + , ) , $}

## 小练习

文法G[E]:
1. E -> TE’
2. E’-> +E| ε
3. T -> FT’
4. T’-> T| ε
5. F -> PF’
6. F’ -> *F’| ε
7. P -> (E) | a | b | ∩
求非终结符号的FIRST集合和FOLLOW集合。

思考十分钟再往下看哦~ ~ ~ ~ ~

### (1) 求FIRST集合(这里只求非终结符号的FIRST集合)

#### 分析：

    FIRST(E): 由E -> TE’可得FIRST(E) = FIRST(T) = { ( , a , b , ∩ }
    FIRST(T): 由T -> FT’可得FIRST(T) = FIRST(F) = { ( , a , b , ∩ }
    FIRST(F): 由F -> PF’ 可得FIRST(F) = FIRST(P) = { ( , a , b , ∩ };
    FIRST(P): 由P -> (E) | a | b | ∩ 可得FIRST(P) = { ( , a , b , ∩ };
    FIRST(E’): 由E’-> +E’| ε 可得FIRST(E’) = { + , ε };
    FIRST(T’): 由T’-> T| ε 可得FIRST(T’) = FIRST(T) +{ ε };
    FIRST(F’): 由F’ -> *F’| ε 可得FIRST(F’) = { * , ε };

#### 结果：

    FIRST(E) = { ( , a , b , ∩ }
    FIRST(T) = { ( , a , b , ∩ }
    FIRST(F) = { ( , a , b , ∩ };
    FIRST(P) = { ( , a , b , ∩ };
    FIRST(E’) = { + , ε };
    FIRST(T’) = { ( , a , b , ∩ , ε };
    FIRST(F’) = { * , ε };

### (2) 求FOLLOW集合

#### 分析：

    FOLLOW(E): 由P -> (E) | a | b | ∩ 和E’-> +E| ε 可得，FOLLOW(E) = FOLLOW(E’) + { ) ，$}
    FOLLOW(E’): 由E -> TE’可得，FOLLOW(E’) = FOLLOW(E)
    FOLLOW(T): 由E -> TE’ 和 T’-> T| ε可得，FOLLOW(T) = FIRST(E’) / ε +FOLLOW(E’)
    FOLLOW(T’): 由T -> FT’可得，FOLLOW(T’) = FOLLOW(T)
    FOLLOW(F): 由T -> FT’和T’-> T| ε可得，FOLLOW(F) = FIRST(T’) / ε +FOLLOW(T)
    FOLLOW(F’): 由F -> PF’和F’ -> *F’| ε 可得，FOLLOW(F’) = FOLLOW(F)
    FOLLOW(P): 由F -> PF’ 和 F’ -> *F’| ε 可得，FOLLOW(P) = FIRST(F’) / ε + FOLLOW(F)

#### 结果：

    FOLLOW(E) = { ) ，$ }
    FOLLOW(E’) = FOLLOW(E) = { ) ，$ }
    FOLLOW(T) = FIRST(E’) / ε +FOLLOW(T’) = { + , ) , $ }
    FOLLOW(T’) = FOLLOW(T) = { + , ) , $ }
    FOLLOW(F) = FIRST(T’) / ε +FOLLOW(T) = { ( , a , b , ∩ , + , ) ,$ }
    FOLLOW(F’) = FOLLOW(F) = { ( , a , b , ∩ , + , ) ,$ }
    FOLLOW(P) = FIRST(F’) / ε + FOLLOW(F) = {* , ( , a , b , ∩ , + , ), $ }