## 爬山演算法：往高的地方爬
#### 一維爬山演算法
如何找出 x^2+3x+5 圖形的最低點?

<img src='https://github.com/syuan0327/ai109b/blob/main/h1.JPG' width="500"  >

首先先乘(-1)

<img src='https://github.com/syuan0327/ai109b/blob/main/h2.JPG' width="500"  >

爬山演算法只能找到局部最佳解，因為爬到一個山頂後就會停止

#### 二維爬山演算法

如果有很多變數，就隨機取變數來做，設定失敗限數來決定是否要爬，例如：[(參考程式碼連結)]()
```
while (failCount < 10000):         #如果"連續失敗"一萬次離開
        fxy = f(x, y)              #目前高度
        dx = random.uniform(-h, h) #左右移動
        dy = random.uniform(-h, h) #前後移動
        if f(x+dx, y+dy) >= fxy:   #如果新點>舊點 
            x = x + dx             #變新x點
            y = y + dy             #變新y點
            print('x={0:.3f} y={1:.3f} f(x,y)={2:.3f}'.format(x, y, fxy))
            failCount = 0
        else:                      #若沒有更高
            failCount = failCount + 1
    return (x,y,fxy)               #結束回傳(已經爬到最高點)
```
#### 均點分布
```
random.uniform(-h,h)
```
<img src = 'https://github.com/syuan0327/ai109b/blob/main/h3.JPG' width="400"  >

優點：簡單

缺點：機率較圓形分布不均

<img src = 'https://github.com/syuan0327/ai109b/blob/main/h4.JPG' width="500"  >



#### solutionArray.py
```
class SolutionArray(Solution):
    def neighbor(self):    #  多變數解答的鄰居函數。
        nv = self.v.copy()                   #  nv=v.clone()=目前解答的複製品=3(x,y,z)
        i = randint(0, len(nv)-1) #  隨機選取一個變數 0~2之間選一個數改變
        if (random() > 0.5):                    #  擲骰子決定要往左或往右移
            nv[i] += self.step
        else:
            nv[i] -= self.step
        return SolutionArray(nv)                    #  傳回新建的鄰居解答。

    def energy(self):      #  能量函數
        x, y, z =self.v    #self.v=3(3個維度)
        return x*x+3*y*y+z*z-4*x-3*y-5*z+8         #  (x^2+3y^2+z^2-4x-3y-5z+8)

    def str(self):    #  將解答轉為字串的函數，以供列印用。
        return "energy({:s})={:f}".format(str(self.v), self.energy())
```

#### self之解釋
[參考網址](https://www.learncodewithmike.com/2020/01/python-class.html)
<img src='https://github.com/syuan0327/ai109b/blob/main/self.JPG' width="500">

## 模擬退火法

原子原來會停留在使內能有局部最小值的位置，加熱使能量變大，原子會離開原來位置，而隨機在其他位置中移動。退火冷卻時速度較慢，使得原子有較多可能可以找到比原先更低的位置。[參考網址](https://zh.wikipedia.org/wiki/%E6%A8%A1%E6%8B%9F%E9%80%80%E7%81%AB)

<img src='https://github.com/syuan0327/ai109b/blob/main/fire1.JPG' width="500">
可以爬出小窟巄

和爬山(次數)很像但是是用溫度及機率算