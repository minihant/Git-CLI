# Git CLI command
## 新增、初始 Repository
  ```
  git init
  ```

## 把檔案交給 Git
  ```
  git add newfile
  ```
  
 ## 如果想要一口氣把全部的檔案加到暫存區，可直接使用 --all
 ```
 git add --all
 ```
 
 ### ”–all” 跟 “.” 參數有什麼不一樣？
 ```
 使用參數	新增檔案	修改檔案	刪除檔案
--all     O         O         O
.	        O         O         X
 ```
 
 ## 把暫存區的內容提交到倉庫裡存檔
 ```
 git commit -m "init commit"
 -m "init commit" 是指要要說明「你在這次的 Commit 做了什麼事」，只要使用簡單、清楚的文字說明就好，中、英文都可
 
 git commit --allow-empty -m "空的"
 git commit -a -m "update content"
 ```
 
 ## 檢視紀錄
 ```
 git log
 git log --oneline
 git log --oneline --graph
 git log --oneline --author="Sherly"   :【狀況題】我想要找某個人或某些人的 Commit…
 git log --oneline --grep="WTF"   :使用 --grep 參數，可以從 Commit 訊息裡面搜尋符合字樣的內容
 git log -S "Ruby" : 使用 -S 參數，可以搜尋在所有 Commit 的檔案中，哪些符合特定條件的
 git log --oneline --since="9am" --until="12am" --after="2017-01"  : 可以找出「今天早上 9 點到 12 點之間所有的 Commit」。還可以再加一個 after
 ```
 
 ## 刪除檔案
 ```
 git rm welcome.html
 git rm welcome.html --cached  : 不想讓這個檔案再被 Git 控管了」的話，可以加上 --cached 參數：
 ```
 
 ## 變更檔名
 ```
 git mv hello.html world.html
 ```
 
 ## 【狀況題】修改 Commit 紀錄
 ```
1.  把 .git 目錄整個刪除（誤）。
2.  使用 git rebase 來修改歷史。
3.  先把 Commit 用 git reset 拆掉，整理後再重新 Commit。
4.  使用 --amend 參數來修改最後一次的 Commit。

git commit --amend -m "Welcome To Facebook"
 ```
## 【狀況題】追加檔案到最近一次的 Commit
```
剛剛完成 Commit，但發現有一個檔案忘了加到，又不想為了這個檔案重新再發一次 Commit…
1.使用 git reset 把最後一次的 Commit 拆掉，加入新檔案後再重新 Commit。
2.使用 --amend 參數進行 Commit。
git commit --amend --no-edit   :--no-edit 參數的意思是指「我不要編輯 Commit 訊息」
```

## 該如何清除忽略的檔案？
```
git clean -fX
```

## 檢視特定檔案的 Commit 紀錄
```
如果想看這個檔案到底每次的 Commit 做了什麼修改，可以再給它一個 -p 參數
git log -p welcome.html

想要知道某個檔案的某一行是誰寫的嗎？
git blame index.html
```

## 狀況題】剛才的 Commit 後悔了，想要拆掉重做
```
git reset anySHA +^  : 這個 Commit 的「前一次」
git reset anySHA +^^ : 則是往前兩次
git reset master^
git reset HEAD^
```

## Reset 的模式
```
分別是 
--mixed :--mixed 是預設的參數
--soft :  工作目錄跟暫存區的檔案都不會被丟掉，所以看起來就只有 HEAD 的移動而已
--hard  :  不管是工作目錄以及暫存區的檔案都會丟掉 
模式	      mixed 模式	soft 模式	  hard 模式
工作目錄	  不變	      不變	      丟掉
暫存區	     丟掉	        不變	      丟掉
```

## 使用分支
```
git branch
git branch -m cat tiger   :想把 cat 分支改成 tiger 分支，使用的是 -m 參數：
git branch -d dog     :刪除分支 dog
git checkout cat  :切換分支to dog
```

## 合併分支
```
git checkout master
git merge cat   :master 分支合併 cat 分支
git merge cat --no-ff  :--no-ff 參數是「不要使用快轉模式合併」的意思
```

## 刪掉分支
```
git branch -d cat   :刪掉 cat 分支
```

## 另一種合併方式（使用 rebase）
```
「重新定義分支的參考基準」的意思, Rebase 合併分支跟一般的合併分支，第一個很明顯的差別，就是使用 Rebase 方式合併分支的話，
Git 不會特別做出一個專門用來合併的 Commit。
git rebase dog   :我，就是 cat 分支，我現在要重新定義我的參考基準，並且將使用 dog 分支當做我新的參考基準
```

## 使用 ORIG_HEAD
```
ORIG_HEAD 會記錄「危險操作」之前 HEAD 的位置。例如分支合併或是 Reset 之類的都算是所謂的「危險操作」。透過這個紀錄點來取消這次 Rebase 相對的更簡單：
git rebase dog
git reset ORIG_HEAD --hard   :可使用這個指令輕鬆的跳回 Rebase 前的狀態

使用 Rebase 時機？
通常在還沒有推（Push）出去但感覺得有點亂（或太瑣碎）的 Commit，會先使用 Rebase 分支來整理完再推出去。
Rebase 等於是修改歷史，修改已經推出去的歷史可能會對其它人帶來困擾，所以對於已經推出去的內容，非必要的話請盡量不要使用 Rebase

```

## 修改歷史訊息 互動模式，啟動！
```
git rebase -i bb0c9c2 
-i 參數是指要進入 Rebase 指令的「互動模式」，而後面的 bb0c9c2 是指這次的 Rebase 指令的應用範圍會「從現在到 bb0c9c2 這個 Commit」，也就是最一開始的那個 Commit
```

## 把多個 Commit 合併成一個 Commit
```
squash
```

## 使用 Revert 指令
```
git revert HEAD --no-edit  :--no-edit 參數，表示不編輯 Commit 訊息

什麼時候使用 Revert 指令？
如果是自己一個人做的專案，用 Revert 指令其實有點過於「禮貌」了，大部份都是直接使用 Reset 就好。但如果對於多人共同協作的專案，也許因為團隊開發的政策，你不一定有機會可以使用 Reset 指令，這時候就可以 Revert 指令來做出一個「取消」的 Commit，對其它人來說也不算是「修改歷史」，而是新增一個 Commit，只是剛好這個 Commit 是跟某個 Commit 反向的操作而已。
```

## Reset、Revert 跟 Rebase 指令有什麼差別？
```
指令	  改變歷史紀錄	說明
Reset	  是	          把目前的狀態設定成某個指定的 Commit 的狀態，通常適用於尚未推出去的 Commit。
Rebase	是	          不管是新增、修改、刪除 Commit 都相當方便，用來整理、編輯還沒有推出去的 Commit 相當方便，但通常也只適用於尚未推出去的 Commit。
Revert	否	           新增一個 Commit 來反轉（或說取消）另一個 Commit 的內容，原本的 Commit 依舊還是會保留在歷史紀錄中。
                      雖然會因此而增加 Commit 數，但通常比較適用於已經推出去的 Commit，或是不允許使用 Reset 或 Rebase 之修改歷史紀錄的指令的場合。
```
