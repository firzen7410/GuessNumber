# GuessNumber

111-1暨南大學_資工系_邏輯設計與實驗_第二十組

使用verilog在FPGA上實作猜數字遊戲

## 輸入

指撥開關_紅1:reset

指撥開關_紅4:檢查

指撥開關_藍色:4bit的數字

輕觸開關:讀入相對應4bit的數字
![46721](https://user-images.githubusercontent.com/122252274/211468765-3e7bf629-037d-4e48-80ef-cf9f796d59d9.png)
## 輸出

蜂鳴器:當4位數猜對會發聲
![46719](https://user-images.githubusercontent.com/122252274/211470450-68dd5155-1b73-4fa2-a2ad-4744da6ce103.png)
7段顯示器:顯示使用者輸入的四位數字

LED_紅色:3bit/顯示多少個數字位置正確

LED_綠色:3bit/顯示多少個數字存在，但位置不正確
![46725](https://user-images.githubusercontent.com/122252274/211549241-c4d780d7-64bd-47e3-8a7a-f502748ca201.png)

## 使用說明

使用者必須先利用藍色指撥開關選擇想輸入的數字，再按相對應的輕觸開關將數字讀入，
當四個數字都讀入之後打開指撥開關_紅4，開始檢查，檢查完會在LED登上顯示多少個數
字位置正確及多少個數字存在但位置不正確，當4個數字的位置都正確，蜂鳴器會響一聲
，遊戲即結束。
![46723](https://user-images.githubusercontent.com/122252274/211468867-b94dd728-2f78-4695-a97c-7f2d947f179a.jpg)

## 影片連結

https://youtu.be/xxStJrnIMgs

