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
<img src = 'https://github.com/syuan0327/ai109b/blob/main/h3.JPG' width="500"  >

優點：簡單

缺點：機率較圓形分布不均

<img src = 'https://github.com/syuan0327/ai109b/blob/main/h4.JPG' width="500"  >



