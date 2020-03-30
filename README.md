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
