
# CLOSURE
* 閉包  
> 在Function裡面再呼叫一個Function, 而內部Function可以使用外部Function"當下"的資料  
錯誤的程式：
``` bash
  for(var i = 0 ; i <= 3 ; i++){
    window.setTimeout(function(){
      console.log(i)
    }, i*1000);
  }
  // output: 4 4 4 4
```
## 使用閉包解決問題
> 迴圈每跑一次, 便會產生一個Function的執行環境, 此時的變數i會獨立在執行環境內, 不會被後續程式影響
``` bash
  for(var i = 0 ; i <= 3 ; i++){
    print(i)
  }

  function print(n){
    window.setTimeout(function(){
      console.log(n)
    }, n*1000);
  }

  // output: 0 1 2 3
```
> 簡化寫法, 直接在Timeout的Function內return一個Function, 此時內部Function會有自己的執行環境, 擁有當下傳入的變數, 因此變數i不會被後續程式影響
``` bash
  for(var i = 0 ; i <= 3 ; i++){
    window.setTimeout(function(n){
      return (n => { console.log(n) })(n)
    }, i*1000, i)
  }

  output: 0 1 2 3
```
直接用 ES6 let 代替 var
> var 與 let 的差異在於執行環境, let擁有自己的執行環境, 紀錄當下的變數值
``` bash
  for(let i = 0 ; i <= 3 ; i++){
    window.setTimeout(function(){
      console.log(i);
    })
  }
```
